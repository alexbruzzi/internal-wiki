# Migrating to new config

As of today, we are migrating to a new config system. 

## So what are config files?

Octomatic connects to a lot of servers. It also reads from a lot of custom places and writes logfiles and other things to other places. All these things which can be configured are placed in a YAML File. These files are config files.

## So, where are they placed?

Till 20 June 2016, we had each repo having its own `config` directory which contained YAML files describing all the options.

## Sounds good, right?

Well, it worked until we started to have a lot of repos and lots of components that all need to connect to same infrastructure (or different, depending on environment). So as you can image, there was a lot of redundancy.

## So, what did we do?

Observing the configs, we found that there are two types of configs:
 # central: Like server ip addresses
 # local: like logfile location

We needed a solution where we can bundle all the central configs together while keeping the scope for local configs as well.

So, we created a new repo for containing all central config files. 

## All welcome `config` repo

Its located at https://phab.octo.ai/diffusion/CONFIG/repository/master/ and go ahead check out and make sure you go through the readme and see the branches.

## So, how does all of this impact me?

In most of the cases, the changes would not result in any "breakdown" or "conflict" with your local commits. So feel free to do a `git pull` on **all the repositories**. However, you may also choose to finish working on your local branch and then pull the changes. In either case, whenever you perform this operation, you would have to do the following

### Clone the config repo

Clone config repo at a path. We will call the path `/path/to/config` everywhere.

### Make sure you use "local" branch.

The configurations for local development environment are placed in "local" branch. Make sure you use this branch. Perform the following

```
git checkout local
```

### For each repo you have, perform the following


 # `cd ` into the repo
 # Perform a symlink of `/path/to/config` (source) to the config directory inside the repo (destination). In most of the cases, you would need to do the following

```
ln -s /path/to/config config/
```

However, in certain repos like gems, or recurring-jobs the config files (destination) are not placed at top level. In that case you need to update the destination. For example for gems repo the command would be

```
ln -s /path/to/config octo-core/lib/octocore/config/
```

Don't miss any repo that connects

## What about `fakestream` and `./create_kong_config.rb` ?

You need to specify the `/path/to/config` as the first parameter to them. So now, your fakestream would be

```
fakestream /path/to/config
```


## Sometimes I get phab session key error

We have updated the access points to secure channel. So, just do `arc install-certificate` and follow the steps.

## Looks good on local, how is all of this handled on production?

We have scripts that automate all of this specific to production environment.

## So, if I have a new config to put, where do I put it?

Refer to the section about local and central configs and choose accordingly. 
