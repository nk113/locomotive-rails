Readme
======

Great [locomotive-chef-repo](https://github.com/intercity/locomotive-chef-repo) + basic rails 4.0 application with easy vagrant setup. You can also run this application locally as usual sharing percona-mysql database runs on vagrant - develop locally with webrick and test the app on vagrant with production environment settings -- nginx + unicorn -- deploying using capistrano.

## Getting started

Clone [locomotive-chef-repo](https://github.com/intercity/locomotive-chef-repo) with destination name ```chef-repo```.

```sh
git@github.com:intercity/locomotive-chef-repo.git chef-repo
```

In the same directory clone **locomotive-rails** with destination name whatever you like.

```sh
git clone git@github.com:nk113/locomotive-rails.git
```

**Rails Application Name**

You might need to update some files to change your rails application name. Since there is no convenient way to do so with rails 4 at the moment, grep like ```grep -ri 'locomotiverails' .``` and replace **LocomotiveRails** appers in lines with the name you like.

Directory structure shuold look like below:

```
(parent)
   |
   |-- chef-repo        (locomotive-chef-repo)
   |
   |-- locomotive-rails (locomotive-rails)
```

Then in ```locomotive-rails``` directory, 

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
