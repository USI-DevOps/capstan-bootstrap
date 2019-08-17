# capstan-bootstrap

Get started faster with [Kenzan Labs / Capstan](https://github.com/kenzanlabs/capstan).

Provides a docker container that automates setup steps described in the Getting Started READMEs.

## Limitations

* Currently automates setup steps for Capstan for GCP ([see here](https://github.com/kenzanlabs/capstan/tree/master/gcp)).

## Requirements

* Git 2.20.1 or later
* Docker 18.06.1 or later
* Google Cloud Platform account with admin access (i.e setting up a trial account is recommended)
* Browser capable of a [private browsing mode](https://www.howtogeek.com/269265/how-to-enable-private-browsing-on-any-web-browser/)

## Get Started

1. Review the environment defaults

```
$ make debug
CONTAINER_NAME       = kenzan/capstan-bootstrap
CONTAINER_VERSION    = 0.0.x
CONTAINER_ROOT       = .container.root
GIT_AUTHOR_NAME      = Firstname Lastname
GIT_AUTHOR_EMAIL     = username@domain.tld
CAPSTAN_REPO         = https://github.com/kenzanlabs/capstan.git
CAPSTAN_TAG          = master
GCP_ACCOUNT          = your.capstan.demo.account@gmail.com
GCP_ZONE             = us-central1-a
GCP_SERVICE_ACCOUNT  = terraform-admin
```
Note: GIT_AUTHOR_NAME and GIT_AUTHOR_EMAIL should reflect previously exported values.

2. Edit the Makefile, set GCP_ACCOUNT to the value of the Gmail account associated to your GCP account. Optionally, set any of the other values, then save.

```
$ vi Makefile
```

3. Build the bootstrap container and container root:

```
$ make container
$ make container.root
```

Note: At this point, you may move additional files into the resulting .container.root directory for use once inside the container.

4. Go inside the container and look around

```
$ make shell
bash-4.4# env | sort
bash-4.4# make debug
```

5. While inside the container...

...start the bootstrap process...

```
bash-4.4# make cdenv
```

Note: Before you walk away, wait for and satisfy the prompts that require you to auth gcloud and specify a billing project.

...then, finish the bootstrap process...

```
bash-4.4# make hal.deploy.connect
bash-4.4# make is.hal.connected
bash-4.4# make spin.setup
bash-4.4# make external.tunnel.command
bash-4.4# exit
```

Note: Yes, we know, if hal.deploy.connect could be run successfully without hanging up the terminal, then this section could be made more optimal. We'll try again later...

7. Access Spinnaker

Outside the container...

```
$ make external.tunnel    # ssh with port forwarding to halyard-tunnel
$ make external.shell     # ssh without port forwarding to halyard-tunnel (use in another terminal to maintain Spinnaker)
```

In private browsing mode...

* Goto http://localhost:9000

