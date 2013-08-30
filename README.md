Readme
======

Great [locomotive-chef-repo](https://github.com/intercity/locomotive-chef-repo) + basic rails 4.0 application with easy vagrant setup. You can also run this application locally as usual sharing percona-mysql database runs on vagrant - develop locally with webrick and test the app on vagrant with production environment settings -- nginx + unicorn -- deploying using capistrano.

## Getting started

Clone [locomotive-chef-repo](https://github.com/intercity/locomotive-chef-repo) with destination name ```chef-repo```.

```sh
git@github.com:intercity/locomotive-chef-repo.git
```

In the same directory clone **locomotive-rails** with destination name whatever you like but with no special character like '-'. Here I specify ```railsapp``` as an example.

**Rails Application Name**

You might need to update Rackfile if you change the destination name -- rails application name -- to what you want.

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

Launch webrick to run the application locally.

```ssh
rails server
```

That's it!
