# Hosted Gems

As octo is a collection of gems, we maintain our own hosted gem. This guide shows how to build a gem server and use it.

# Setup

## Clone the gems-server repo

This will start a gems server.

- Clone the gems-server repo. [http://phab.octo.ai/diffusion/GEMSSERVER/](http://phab.octo.ai/diffusion/GEMSSERVER/)
- start the server by `rackup`

## Private URL

The URL at which above server is hosted should be accessible like **gems.octo.ai**. 

### Security

We can have either

- HTTP Basic authentication
- URL behind a vpn (recommended)

## Continuous Integration

Right now, we can use server's upload gem feature to upload gems. This would later on be integrated with `arc land` so that whenever there is a new version deployed, this should be mirroring it.

# Usage

Any application that uses one of the octo's gem need to have following added in their Gemfile

```ruby
source 'http://gems.octo.ai'
```

Or the following (given HTTP Basic Auth)

```ruby
source http://username:password@gems.octo.ai/
```

# RDoc server

In addition to the gem server, we can (optionally, recommended) set up a Yard server which serves the documentation. The way to do it would be

```
lang=bash
yard server -g
```

This will host the documentation for **all** the gems installed on that machine.

## Private URL

This should also be accessible via a url like **http: //rdoc.octo.ai** or something similar.
