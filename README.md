# FunDev TAS

FunDev Rancher Kubernetes for TAS.

## Introduction

This FunDev is used for experimenting with Kubernetes on Rancher.
You need Virtual Box and Vagrant for the installation of the virtual machines
https://www.vagrantup.com/downloads.html
https://www.virtualbox.org/wiki/Downloads

## Installing the Boxes

To install the boxes, do the following:

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

cd kubernetes/rancher01
vagrant up
cd ../..
cd kubernetes/rancher02
vagrant up
cd ../rancher01
vagrant ssh
sudo su -
docker run --name rancher -d --restart=unless-stopped -p 8080:80 -p 8443:443 -v /opt/rancher:/var/lib/rancher rancher/rancher:latest
```
