# Current state of dnstwister/please read before suggesting changes

__dnstwister__ was created four years ago, on the Google App Engine PaaS which
(from memory) only supported Python 2.x at the time.

Since then __dnstwister__ has moved to Heroku and the world has thoroughly
moved to Python 3. On [January 1 2020](https://www.python.org/doc/sunset-python-2/)
Python 2 will no longer be supported by the Python Software Foundation.

__dnstwister__ has generally kept up with the releases of Python 2.x but it is
well and truly time to move the codebase to Python 3.

As such, until January 2020 I will __not__ be performing any feature
development in __dnstwister__, the only changes made will be security patches
and fixes to functionality-critical bugs. This will give me the stable
platform needed to cut over the codebase and ensure it can be rigorously
tested before going live very early in 2020.

Upon that release going live __dnstwister__ will no longer by able to be ran
in Python 2 but I will leave a link to the last Python 2 commit on this README
for a reasonable period of time.

I will also take the opportunity at that point to more clearly differentiate
__dnstwister__ the Flask web application you can download here and the
[dnstwister.report](https://dnstwister.report) service (that uses this
codebase as its core) but also relies on other FaaS and PaaS offerings
including CloudFlare Workers. This split will allow this codebase and
[dnstwister.report](https://dnstwister.report) independently evolve to suit
the needs of their user bases, whilst still sharing relevant improvements.

# dnstwister

A Heroku-hosted version of the very excellent
[dnstwist](https://github.com/elceef/dnstwist).

|production|development|
|:--------:|:---------:|
|[![Production Branch Build Status](https://travis-ci.org/thisismyrobot/dnstwister.svg?branch=heroku-deploy)](https://travis-ci.org/thisismyrobot/dnstwister)|[![Development Branch Build Status](https://travis-ci.org/thisismyrobot/dnstwister.svg?branch=master)](https://travis-ci.org/thisismyrobot/dnstwister)|
|[![Production Branch Coverage Status](https://coveralls.io/repos/github/thisismyrobot/dnstwister/badge.svg?branch=heroku-deploy)](https://coveralls.io/github/thisismyrobot/dnstwister?branch=heroku-deploy)|[![Development Branch Coverage Status](https://coveralls.io/repos/github/thisismyrobot/dnstwister/badge.svg?branch=master)](https://coveralls.io/github/thisismyrobot/dnstwister?branch=master)|

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/thisismyrobot/dnstwister/tree/heroku-deploy)

## dnstwist vs. dnstwister

In [the author's](https://github.com/elceef) words, dnstwist helps you
["...find similar-looking domains that adversaries can use to attack
you..."](https://github.com/elceef/dnstwist/blob/master/docs/README.md)

This project, __dnstwister__, gives you access to the power of dnstwist via a
convenient web interface and offers csv/json reports and a fully featured
RESTful API.

And it's 100% free.

__dnstwister__ is hosted at
[dnstwister.report](https://dnstwister.report).

## dnstwist module

This project currently uses a modified version of dnstwist, in
[dnstwister/dnstwist](dnstwister/dnstwist).

I have kept the original dnstwist README and LICENCE but I have applied an
"Unlicense" to __dnstwister__.

Though the licences are different (dnstwist 
[uses](https://github.com/elceef/dnstwist/blob/master/docs/LICENSE) an
Apache licence),
[this is an acceptable](http://opensource.stackexchange.com/a/963/3236) use of
dnstwist in my project.

## Contributors

 * [@elceef](https://github.com/elceef) (dnstwist itself)
 * [@peterwallhead](http://github.com/peterwallhead) (mobile UI assistance)
 * [@prashant-shahi](https://github.com/prashant-shahi) (docker configuration)
 * [@wesinator](https://github.com/wesinator) (file export improvements)

## A note on running dnstwister yourself

Some of the more advanced functionality of
[dnstwister.report](https://dnstwister.report) (email subscriptions,
asynchronous web UI, "noisy" domain filtering etc) is built off infrastructure
beyond the core Python Flask stack behind __dnstwister__ - for instance
PostgreSQL & REDIS databases and CloudFlare Workers. Some of the code that
supports this functionality is not available in this repository as it forms
the core of the [dnstwister.report](https://dnstwister.report) service.

The fundamental functionality supporting the generation of a web-based report
on a domain via the web interface will always remain available in this
repository.

## Developing dnstwister

Once-off setup:

```sh
pip install pipenv
pipenv install --dev
```

Running:

```sh
pipenv run python local_server.py
```

And browse via http://localhost:5000

## Running dnstwister using Docker

If you don't have [Docker](https://hub.docker.com/) installed, you can click
[here](https://www.docker.com/community-edition/ "Docker : Community Edition")
for **Docker CE**, and follow the installation steps.

### Building and Running locally

```sh
# Cloning latest source code
git clone https://github.com/thisismyrobot/dnstwister

# Changing directory
cd dnstwister

# Checkout to the stable branch i.e. heroku-deploy
git checkout heroku-deploy

# Building dnstwister image using Dockerfile
docker build -t dnstwister .

# Running the application inside a container
docker run -td -p 5000:5000 --name myapp dnstwister
```

Now, go to `http://localhost:5000` using any browser to use dnstwister.

### Fetching pre-built image

Alternatively, you can pull the pre-built image from DockerHub, and run
locally. This way, you wouldn't have to wait for the build time. The image
present in docker hub is from the stable branch **heroku-deploy**.

```sh
docker pull dnstwister/dnstwister:2.9.3
docker run -td -p 5000:5000 --name myapp dnstwister/dnstwister:2.9.3
```

Now, go to `http://localhost:5000` using any browser to use dnstwister.

## Tests

Running:

```sh
pipenv run py.test
```

## Say hello

I'd love to hear your feedback so [email me](mailto:hello@dnstwister.report),
fire off a [tweet](https://twitter.com/dnstwister) in my general direction or
you can just [say thanks](https://saythanks.io/to/thisismyrobot)!... :)
