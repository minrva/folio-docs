# Introduction

[The Future of Libraries is Open](https://www.folio.org/). This is an overview of the software.

## FOLIO Demo Platform v4.1.0

The module development tutorial was made using the `FOLIO demo platform v4.1.0`, released at the end of Aug. 2017. The software was tested on a `macOS High Sierra`.

The [demo platform v4.1.0](https://app.vagrantup.com/folio/boxes/stable) can be run in a virtual machine by following the instructions on the [folio-ansible repository](https://github.com/folio-org/folio-ansible).

## Source Code

FOLIO source code is hosted on [github](https://github.com/folio-org). A good description of the main repositories can be found at <http://dev.folio.org/source-code/>. The demo platform is built from:

- `debian jessie` operating system
- `26` modular code repositories
- `1` postgres database
- configuration scripts (e.g. ansible, jenkins, bash, etc.)

## Repositories

The source code is packaged and uploaded to various repositories during the [build, test, and deploy process](http://dev.folio.org/doc/automation.html):

- [Docker Hub](https://hub.docker.com/r/folioci/)
- [Nexus Repository](https://repository.folio.org/)
- [HashiCorp Vagrant Cloud](https://app.vagrantup.com/folio)

## References

Complete developer resources can be found on the [FOLIO website](http://dev.folio.org/).
