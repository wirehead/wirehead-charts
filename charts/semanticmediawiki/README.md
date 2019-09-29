# Semantic MediaWiki as a docker container

![Logo](https://raw.githubusercontent.com/wirehead/semantic-mediawiki-docker/master/icons/favicon-202x202.png)

A nice Helm chart designed for running [Semantic MediaWiki](https://www.semantic-mediawiki.org/) with a set of useful modules already installed.

**WORK IN PROGRESS WARNING**: I'm totally not finished messing with this.

## Introduction

This chart bootstraps a [SemanticMediaWiki](https://www.semantic-mediawiki.org/) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

**By default, this runs with persistance turned off using the SQLite engine.**  If you want to configure persistance you probably want to set up a separate external database instance.  Most cloud providers (AWS, GCP, Azure, DigitalOcean, et al) these days have a managed SQL database service that is arguably less trouble than running one inside of Kubernetes.  

## Prerequisites

- Kubernetes 1.13+ (It may work on older versions?)
- PV provisioner support in the underlying infrastructure


## Installing the Chart


## Uninstalling the Chart

## Configuration

The following table lists the configurable parameters of the SemanticMediaWiki chart and their default values.

|              Parameter               |               Description                                   |                         Default                         |
|--------------------------------------|-------------------------------------------------------------|---------------------------------------------------------|


## Persistence

## Upgrading

## Changelog

## Todo:

- [x] Works in basic mode
- [ ] Readme files
- [x] Cron
- [ ] Persistance flag
- [ ] Config variables
- [ ] Figure out that helm repo build thingie