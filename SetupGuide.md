All the generic guidelines for setting up the octo a.i. environment.

# Basic Setup

## System

A standard *ix system with admin privilages. Tested and verified on

- OS X 10.11.4 (El Capitan)
- Ubuntu

## Kong

**Version 0.6.1** 

## Kafka

**Version**: 0.8.2.2

Any other version will cause conflicts with the system and introduces unstability.

## Cassandra

**Version** : 2.2.4

## Redis

**Version** : 3.0.5

## Zookeeper

**Version** : 3.4.7

## Ruby

Preferred way: [rvm](http://rvm.io)   
**Version** : 2.1.5

# Repos

Before proceeding any further, make sure all the above mentioned systems are up and running.

## Gems first

- Clone the [gems repo](http://phab.octo.ai/diffusion/GEMS/)
- Build and install all the gems by running the provided `build.sh` script.

### Creating Database

Once you have installed the `octocore` gem, you should be able to create the db schema depending on the environment. The way to do it is

```
lang=bash
cd gems/octo-core/
rake --tasks # See all the possible tasks
rake octo:init # Initialize the db schema
rake octo:reset # Resets the db schema
```

## APIHandler

- This repo handles all the API calls and pushes them to kafka
- Clone [APIHandler repo](http://phab.octo.ai/diffusion/APIHANDLER/)
- Make sure you have your kong setup at this moment. If you have not, use the provided `bin/kong_setup.rb` file in this repo alongwith the `bin/kong_config.yaml` to setup kong. Review the contents of yaml config file before.
- Follow the instructions in provided README to setup APIHandlers.

# Clone APIConsumer

- This repo handles all the kafka messages pushed by APIHandler and takes actions and triggers various hooks
- Clone [APIConsumer repo](http://phab.octo.ai/diffusion/APICONSUMER/)
- Follow the README instructions to get it working.

# Clone recurring jobs

- This repo is the hearbeat. It triggers various time based jobs.
- Clone the [Recurring Jobs repo](http://phab.octo.ai/diffusion/RECURR/)
- Follow the instructions on provided README to start scheduler and workers.

# Clone Enterprise Dashboard

- This is where business comes into picture. This is our end product that businesses use.
- Clone the [Enterprise Dashboard repo](http://phab.octo.ai/diffusion/DASHE/)
- As usual, follow the README

# Newsfeed Webservice

- Newsfeed as a webservice repo
- [http://phab.octo.ai/diffusion/WSNEWSFEED/](http://phab.octo.ai/diffusion/WSNEWSFEED/)

# HEAVEN

- This repo contain all the [GOD](http://godrb.com) scripts.
- [http://phab.octo.ai/diffusion/HEAVEN/](http://phab.octo.ai/diffusion/HEAVEN/)
- README

At this stage your development environment should be ready to serve the bare minimum of Octomatic platform.

You can use the `fakestream` command to create fake stream of data. To know more about this refer to [http://phab.octo.ai/diffusion/GEMS/browse/master/octo-core/bin/fakestream](http://phab.octo.ai/diffusion/GEMS/browse/master/octo-core/bin/fakestream)

