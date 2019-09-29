# Semantic MediaWiki as a docker container

![Logo](https://raw.githubusercontent.com/wirehead/semantic-mediawiki-docker/master/icons/favicon-202x202.png)

A nice Helm chart designed for running [Semantic MediaWiki](https://www.semantic-mediawiki.org/) with a set of useful modules already installed.

**WORK IN PROGRESS WARNING**: I'm totally not finished messing with this.

## TL;DR;

```console
$ helm repo add wirehead https://wirehead.github.io/wirehead-charts
$ helm install wirehead/semanticmediawiki
```

## Introduction

This chart bootstraps a [SemanticMediaWiki](https://www.semantic-mediawiki.org/) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

**By default, this runs with persistance turned off using the SQLite engine.**  If you want to configure persistance you probably want to set up a separate external database instance.  Most cloud providers (AWS, GCP, Azure, DigitalOcean, et al) these days have a managed SQL database service that is arguably less trouble than running one inside of Kubernetes.  

## Prerequisites

- Kubernetes 1.13+ (It may work on older versions?)
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install --name my-release semanticmediawiki
```
This will deploy a SemanticMediaWiki instance on the Kubernetes cluster in the default configuration.  See the [configuration](#configuration) section to determine how to configure your instance.

**Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```
This will remove all components running on Kubernetes associated with this install.  

Note that it will not de-provision the database data if that's been configured.

## Configuration

The following table lists the configurable parameters of the SemanticMediaWiki chart and their default values.

|         Parameter           |               Description                                   |                         Default                         |
|-----------------------------|-------------------------------------------------------------|---------------------------------------------------------|
| `image.repository`          | SemanticMediaWiki image registry | `wirehead/semantic-mediawiki-docker` |
| `image.tag`                 | SemanticMediaWiki Image tag | `latest` |
| `image.pullPolicy`          | Image pull policy | `IfNotPresent` |
| `nameOverride`              | String to partially override semanticmediawiki.fullname template with a string (will prepend the release name) | `nil` |
| `fullnameOverride`          | String to fully override semanticmediawiki.fullname template with a string | `nil` |
| `provisionEnabled`          | Set this to true to trigger a database provision | `false` |
| `wiki.path`                 | Root for SemanticMediaWiki to generate paths against | `http://127.0.0.1:8080` |
| `wiki.semanticRoot`         | Path for SemanticMediaWiki to use as a root for the RDF properties | `http://www.example.com/` |
| `wiki.user`                 | Admin user of the application | `admin` |
| `wiki.password`             | Application password | `password` |
| `wiki.name`                 | Name for the wiki | `tst` |
| `wiki.lang`                 | Language code for the wiki | `en` |
| `wiki.uploads`              | Set to true value to enable uploads | `false` |
| `wiki.secretKey`            | Secret and session key for MediaWiki | randomly generated string |
| `database.type`             | Type of the database (sqlite, postgres, or mysql) | `sqlite` |
| `database.host`             | Host of the external database | `nil` |
| `database.user`             | Username in the external db | `nil` |
| `database.password`         | Password for the above username | `nil` |
| `database.name`             | Name of the external database | `nil` |
| `database.port`             | Port for the external database (only necessary for postgres) | `nil` |
| `database.schema`           | Schema of the external database (only necessary for postgres) | `nil` |
| `persistence.enabled`       | Use a PVC to persist data | `false` |
| `persistence.existingClaim` | Provide an existing PersistentVolumeClaim | `nil` |
| `persistence.storageClass`  | Storage class of backing PVC | `nil` (uses alpha storage class annotation) |
| `persistence.accessMode`    | Use volume as ReadOnly or ReadWrite | `ReadWriteOnce` |
| `persistence.annotations`   | Persistent Volume annotations | `{}` |
| `persistence.size`          | Size of data volume | `8Gi` |
| `persistence.resourcePolicy` | set resource-policy Helm annotation on PVC. Can be nil or "keep" | `nil` |
| `existingSecret`            | Use an existing secret for database.password and wiki.secretKey | `nil` |
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

### Database

Primary wiki content is stored in a database

 * Set `provisionEnabled` to true once to trigger the database provisioner process

### Uploads

Images and the state of the SemanticMediaWiki migrations are stored in a mapped volume.

## Upgrading

No upgrades yet.

## Changelog

Still on dev-ish

## Inspired by:

 * https://github.com/helm/charts/tree/master/stable/mediawiki