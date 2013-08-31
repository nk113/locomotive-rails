Readme
======

Easy vagrant setup for great [locomotive-chef-repo](https://github.com/intercity/locomotive-chef-repo). You can develop your rails application locally with webrick and test the app on vagrant with production environment setting sharing database between host and guest vagrant box. Capistrano also works well with vagrant box.

## Getting started

Clone [locomotive-chef-repo](https://github.com/intercity/locomotive-chef-repo) with destination name ```chef-repo```.

```sh
git@github.com:intercity/locomotive-chef-repo.git chef-repo
```

In the same directory create rails app.

```sh
rails new <name>
```

Directory structure shuold look like below:

```
(parent)
   |
   |-- chef-repo (locomotive-chef-repo)
   |
   |-- <name>    (your rails application)
```

Copy all files in this repository to your rails application directory updating repository parameter in ```config/deploy.rb``` then run following commands. Update ```config/deploy/vagrant.rb``` appropriately if you have multiple vagrant instances in your local.

```ssh
bundle install
vagrant up
vagrant provision
cap deploy
```

You should be able to see something cool accessing ```http://localhost:8080``` with your browser.

Launch webrick to run the application locally.

```ssh
rails server
```

That's it!
