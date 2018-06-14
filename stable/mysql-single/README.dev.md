# MySQL

[MySQL](https://MySQL.org) is one of the most popular database servers in the world. Notable users include Wikipedia, Facebook and Google.

## Introduction

This chart bootstraps a single MySQL deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Oracle mysql operator
- Kubernetes 1.6+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release banzaicloud-catalog/mysql-single
```

The command deploys MySQL on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

By default a random password will be generated for the root user. If you'd like to set your own password change the mysqlRootPassword
in the values.yaml.

You can retrieve your root password by running the following command. Make sure to replace [YOUR_RELEASE_NAME]:

    printf $(printf '\%o' `kubectl get secret [YOUR_RELEASE_NAME]-mysql -o jsonpath="{.data.mysql-root-password[*]}"`)

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the MySQL chart and their default values.

| Parameter                            | Description                               | Default                                              |
| ------------------------------------ | ----------------------------------------- | ---------------------------------------------------- |
| `mysql.database.name`                | Name for new database to create.          | `nil`                                                |
| `mysql.database.username`            | Username of new user to create.           | `nil`                                                |
| `mysql.database.password`            | Password for the new user.                | `nil`                                                |
| `mysql.cluster.root_password`        | Password for the `root` user.             | Generated                                            |
| `mysql.cluster.version       `       | Mysql version.                            | 5.7                                                  |

TBD

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set mysql.catalog.root_password=secretpassword,mysql.database.username=my-user,mysql.database.password=my-password,mysql.database.nam=my-database \
    banzaicloud-catalog/mysql-single
```

The above command sets the MySQL `root` account password to `secretpassword`. Additionally it creates a standard database user named `my-user`, with the password `my-password`, who has access to a database named `my-database`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f your-values.yaml banzaicloud-catalog/mysql-single
```

> **Tip**: You can use the default [values.yaml](values.yaml)

