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

|         Parameter           |               Description                                   |                         Default                         |
|-----------------------------|-------------------------------------------------------------|---------------------------------------------------------|
| `image.repository`          | SemanticMediaWiki image registry | `wirehead/semantic-mediawiki-docker` |
| `image.tag`                 | SemanticMediaWiki Image tag | `latest` |
| `image.pullPolicy`          | Image pull policy | `IfNotPresent` |
| `nameOverride`              | String to partially override semanticmediawiki.fullname template with a string (will prepend the release name) | `nil` |
| `fullnameOverride`          | String to fully override semanticmediawiki.fullname template with a string | `nil` |
| `wiki.path`                 | Root for SemanticMediaWiki to generate paths against | `http://127.0.0.1:8080` |
| `wiki.semanticRoot`         | Root for SemanticMediaWiki to use as a root for the RDF properties | `http://www.example.com/` |
| `wiki.user`                 | Admin user of the application | `admin` |
| `wiki.password`             | Application password | `password` |
| `wiki.name`                 | Name for the wiki | `tst` |
| `wiki.lang`                 | Language code for the wiki | `en` |
| `service.type`              | Kubernetes Service type | `ClusterIP` |
| `service.port`              | Service HTTP Port | `80` |
| `ingress.enabled`           | Enable ingress controller resource | `false` |
| `ingress.annotations`       | Annotations for this host's ingress record | `[]` |
| `ingress.hosts[0].name`     | Hostname to your SemanticMediawiki installation | `mediawiki.local` |
| `ingress.hosts[0].paths`    | Path within the url structure | `/` |
| `ingress.tls[0].secretName` | TLS Secret Name | `nil` |
| `ingress.tls[0].hosts`      | TLS Secret hostnames | `nil` |
| `web.resources`             | Resources used by the web container | `nil` |
| `cron.resources`            | Resources used by the cron container | `nil` |
| `affinity`                  | Map of node/pod affinities | `{}` |
| `nodeSelector`              | Map of node selectors | `{}` |
| `tolerations`               | Map of node tolerations | `{}` |


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