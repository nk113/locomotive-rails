# -*- mode: ruby -*-
# vi: set ft=ruby :
require 'open-uri'
require 'openssl'


PROJECT_NAME = File.basename(File.dirname(__FILE__))

BOX = 'precise64'
BOX_URL = 'http://files.vagrantup.com/precise64.box'
CHEF_REPO_PATH = '../chef-repo'
COOKBOOKS_PATH = ["#{CHEF_REPO_PATH}/cookbooks", 'site-cookbooks',]
ROLES_PATH = "#{CHEF_REPO_PATH}/roles"
DEPLOY_USER = 'deploy'
INSECURE_PUBLIC_KEY = open('https://raw.github.com/mitchellh/vagrant/master/keys/vagrant.pub',
                           :ssl_verify_mode => OpenSSL::SSL::VERIFY_NONE).read

# chef later than 11.0.0 is required to get apt cookbook to work in vagrant
# 28-08-2013:
#   chef 11.6.0 has an error (like https://gist.github.com/stormerider/6085044)
#   as well as 11.4.4 so use stable version here
CHEF_UPDATE = 'gem install chef --version 11.4.2 --no-rdoc --no-ri --conservative'

RBENV_RUBIES = ['2.0.0-p195',]
RBENV_GLOBAL = '2.0.0-p195'
RBENV_GEMS = {
  '2.0.0-p195' => [
    {'name' => 'bundler'},
  ],
}


Vagrant.configure('2') do |config|
  config.vm.box = BOX
  config.vm.box_url = BOX_URL

  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.network :forwarded_port, guest: 3306, host: 3306
  config.vm.network :private_network, ip: '10.10.0.1'

  # update chef
  config.vm.provision :shell, :inline => CHEF_UPDATE

  # provision
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = COOKBOOKS_PATH
    chef.roles_path = ROLES_PATH

    chef.add_role 'vagrant'
    chef.add_role 'mysql'
    chef.add_role 'rails'

    chef.add_recipe 'rbenv::user'

    chef.json = {
      :rbenv => {
        :user_installs => [
          {
            :user => DEPLOY_USER,
            :rubies => RBENV_RUBIES,
            :global => RBENV_GLOBAL,
            :gems => RBENV_GEMS,
          },
        ],
      },
      :vagrant => { # chef will fail if this won't be provided
      },
      :mysql => {
        :server_root_password => '',
        :server_repl_password => '',
        :server_debian_password => '',
        :allow_remote_root => true,
      },
      :authorization => {
        :sudo => {
          :users => ['vagrant', DEPLOY_USER,],
          :passwordless => true,
          :include_sudoers_d => true,
        }
      },
      :ssh_deploy_keys => [INSECURE_PUBLIC_KEY,],
      :deploy_users => [DEPLOY_USER,],
      :active_applications => {
        "#{PROJECT_NAME}_vagrant" => {
          :domain_names => ['localhost',],
          :packages => ['libpq-dev', 'nodejs',],
          :rails_env => 'vagrant',
          :deploy_user => DEPLOY_USER,
          :database_info => {
            :adapter => 'mysql2',
            :username => 'vagrant',
            :password => '',
            :database => "#{PROJECT_NAME}_vagrant",
            :client_addresses => ['10.10.*',],
          }
        }
      },
    }
  end
end
