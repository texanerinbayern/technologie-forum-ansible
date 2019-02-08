# NetApp Ansible Demo

Forked from https://github.com/schmots1/insight-ansible

You can use this Docker container to test these playbooks https://hub.docker.com/r/pixelchrome/ntap-ansible-container

# Example Playbooks how to setup a new ONTAP Cluster

## `01_setup_cluster.yml`

Basic setup of a new ONTAP Cluster

### Tasks

* Add Licenses
* Assign unowned disks
* Create Aggregates

## `02_setup_svm.yml`

Create a NFS SVM

### Tasks

* Create SVM
* Create the Network Interface
* Setup NFS
* Create default export policy

## `03_setup_export_volume.yml`

Export a Volume

### Tasks

* Create Volume
* Create export policy
* Setup export rules

## `04_host.yml``

Mount on a Server/Host the NFS Share

### Tasks

* Install `nfs-utils`
* Mount the NFS Share and add to `/etc/fstab`

# Bonus :)

## Cleanup of the above `9*_cleanup_*.yml`