Readme
======

Great [locomotive-chef-repo](https://github.com/intercity/locomotive-chef-repo) + basic rails application with easy vagrant setup. You can run this application locally as usual too sharing database runs on vagrant - develop locally with webrick and test the app on vagrant with nginx + unicorn environment deploying using capistrano.

## Getting started

Clone [locomotive-chef-repo](https://github.com/intercity/locomotive-chef-repo) with destination name ```chef-repo```.

```sh
git@github.com:intercity/locomotive-chef-repo.git
```

In the same directory clone **locomotive-rails** with destination name whatever you like but with no special character like '-'. Here I specify ```railsapp``` as an example.

```sh
git clone git@github.com:nk113/locomotive-rails.git railsapp
```

Directory structure looks like below:

```
(parent)
   |
   |-- chef-repo  (locomotive-chef-repo)
   |
   |-- railsapp   (locomotive-rails)
```

Then in ```railsapp``` directory, 

```ssh
bundle install
vagrant up
vagrant provision
cap deploy
```

You should be able to see something cool accessing ```http://localhost:8080``` with your browser.

Run webrick to run the application locally.

```ssh
rails server
```

That's it!

## Sharing database

You need to update ```config/database.yml``` to use mysql as the database and to share the database between host and vagrant instance. Database settings can be found in ```Vagrantfile```.