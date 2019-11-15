# FunDev TAS

FunDev Rancher Kubernetes for TAS.

## Introduction

This FunDev is used for experimenting with Kubernetes on Rancher.
You need Virtual Box and Vagrant for the installation of the virtual machines


## Installing the Boxes

To install the boxes, do the following`my-release`:

```console
vagrant box add centos/7
==> box: Loading metadata for box 'centos/7'
    box: URL: https://vagrantcloud.com/centos/7
This box can work with multiple providers! The providers that it
can work with are listed below. Please review the list and choose
the provider you will be working with.

1) hyperv
2) libvirt
3) virtualbox
4) vmware_desktop

Enter your choice: 3
==> box: Adding box 'centos/7' (v1902.01) for provider: virtualbox
    box: Downloading: https://vagrantcloud.com/centos/boxes/7/versions/1902.01/providers/virtualbox.box
    box: Download redirected to host: cloud.centos.org
==> box: Successfully added box 'centos/7' (v1902.01) for 'virtualbox'!

git clone https://github.com/DennisVermeulen/kubernetes.git

cd rancher01
vagrant up
cd ..
cd rancher02
vagrant up


```

The command deploys AWX on the Kubernetes cluster in the default configuration.
The [configuration](#configuration) section lists the parameters that can be configured
during installation.

This charts embeds chart dependencies specified in the requirements.yaml file:

- postgresql
- memcached
- rabbitmq

**Note**: Currently, this chart is not ready to be used with external postgresql,
memcached or rabbitmq. PR welcomed.

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart
and deletes the release.

## Configuration

The following table lists the configurable parameters of the
awx chart and their default values.
Postgresql, memcached, rabbitmq charts values can be overridden in
awx/values.yaml

Parameter | Description | Default
--------- | ----------- | -------
`replicaCount` | Pod replica count | `1`
`awx_web.image.repository` |  | `ansible/awx_web`
`awx_web.image.tag` |  | `2.1.2`
`awx_web.image.pullPolicy` |  | `IfNotPresent`
`awx_task.image.repository` |  | `ansible/awx_task`
`awx_task.image.tag` |  | `2.1.2`
`awx_task.image.pullPolicy` |  | `IfNotPresent`
`awx_secret_key` |  | `awxsecret`
`default_admin_user` |  | `admin`
`default_admin_password` |  | `password`
`deployment.annotations` |  | `{}`
`service.internalPort` |  | `8052`
`service.externalPort` |  | `8052`
`ingress.enabled` |  | `false`
`memcached.install` | Install memcached chart | `true`
`rabbitmq.install` | Install rabbitmq chart | `true`
`rabbitmq.rabbitmq.username` | Rabbitmq username | `awx`
`rabbitmq.rabbitmq.password` | Rabbitmq password| `awx`
`rabbitmq.rabbitmq.configuration` | Rabbitmq configuration file| cf values.yaml
`postgresql.install` | Install postgresql chart | `true`
`postgresql.postgresqlUsername` | postgresql username | `postgres`
`postgresql.postgresqlPassword` | postgresql password | `awx`
`postgresql.postgresqlDatabase` | postgresql database | `awx`
`postgresql.persistence.enabled` | postgresql persistence | `true`

