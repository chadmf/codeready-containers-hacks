# Red Hat CodeReady Containers Collection

-------

Use Ansible to deploy Red Hat CodeReady Containers with HACKS

CodeReady Containers brings a minimal, preconfigured OpenShift 4.1 or newer cluster to your local laptop or desktop computer for development and testing purposes. CodeReady Containers is delivered as a Red Hat Enterprise Linux virtual machine that supports native hypervisors for Linux, macOS, and Windows 10.

## Requirements

-------

* Ansible
* Fedora or RHEL 8.x
* IF using RHEL make sure it is registered
* OpenShift CodeReady WorkSpaces  pull secret
  * <https://cloud.redhat.com/openshift/install/crc/installer-provisioned>
* Anisble post fix module
  * `ansible-galaxy collection install ansible.posix`

## Inspriation

[Accessing CodeReady Containers on a Remote Server](https://www.openshift.com/blog/accessing-codeready-containers-on-a-remote-server/) by Jason Dobies  
[Overview: running crc on a remote server](https://gist.github.com/tmckayus/8e843f90c44ac841d0673434c7de0c6a) by [Trevor McKay](https://gist.github.com/tmckayus)  
[Deploy Bare-Metal Clusters with CRC](https://gist.github.com/v1k0d3n/9ceec7589b5bab0b61b85c2a1e1c463c) by Brandon B. Jozsa

## Features

-------

* CodeReady Containers Remote Server Access
* CodeReady Containers on local host

## Role Variables

-------

Type  | Description  | Default Value
--|-----|--
crc_version  | Target CRC version  | latest
crc_url      |  CRC download URL | <https://mirror.openshift.com/pub/openshift-v4/clients/crc/>
crc_file_name  | CRC filename  | crc-linux-amd64.tar.xz
use_all_in_one_haproxy | Use current machine as haproxy LB | true
haproxy_ip             | Set ha proxy ip if above is set to flase **NOT TESTED**| ""
log_level              | Change log level of crc start command | info
crc_ip_address | Default CRC ip address| 192.168.130.11
ocp4_release  | OCP release folder for cli | latest
ocp4_version   | OCP cli version | latest
ocp4_release_url | OCP release url | "<https://mirror.openshift.com/pub/openshift-v4/clients/ocp/>{{ ocp4_release }}/"
ocp4_client | OCP cli filename | "openshift-client-linux-{{ ocp4_version }}.tar.gz"
remove_oc_tool | remove oc cli  | false
delete_crc_deployment | delete CodeReady Containers deployment  | false
forward_server | Server to manage external requests | 1.1.1.1

## Dependencies

-------

### Home drive should have 50 Gig or better

### On RHEL 8.x

* Register system
* Follow system requirements from the code ready containers documentation

### On Fedora

* Follow system requirements from the code ready containers documentation
* enable and start sshd

### Download pull-secret

-------

Download pull-secret to your Downloads folder [here](https://cloud.redhat.com/openshift/install/pull-secret). Ansible will look for it in ~/Downloads/pull-secret or change the pull secret variable "{{ pull_secret_path }}"

### Deployment Flags

-------

You can use any of these flags individually to run just that part of the playbook.

* download_crc
* extract_crc
* configure_oc_cli
* setup_crc
* start_crc_deployment
* configure_ha_proxy


## Start a full deployment for localhost

```shell
ansible-playbook localhost.yml --tags download_crc,extract_crc,configure_oc_cli,setup_crc,start_crc_deployment
```

## Get crc url and login info

```shell
ansible-playbook localhost.yml --tags get_codeready_info
```

## Delete deployment

```shell
ansible-playbook localhost.yml --extra-vars "delete_crc_deployment=true" 
```

### License

-------

GPL-3.0

### Author Information

-------

* Tosin Akinosho - [tosin2013](https://github.com/tosin2013)
* Chad Ferman - [chadmf](https://github.com/chadmf)
