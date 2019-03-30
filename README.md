# NetApp Ansible Demo

Forked from https://github.com/pixelchrome/technologie-forum-ansible which was forked from https://github.com/schmots1/insight-ansible

You can use this Docker container to test these playbooks https://hub.docker.com/r/pixelchrome/ntap-ansible-container

# Example Playbooks how to setup a new ONTAP Cluster

## Clone this repository

```sh
$ git clone https://github.com/texanerinbayern/technologie-forum-ansible.git
```

## `01_setup_cluster.yml`

Basic setup of a new ONTAP Cluster

### Tasks

* Add Licenses
* Assign unowned disks
* Create Aggregates

This playbook asks for the password of the ONTAP system. Just to show how a user prompt works.

```sh
$ ansible-playbook 01_setup_cluster.yml
```

![Setup the cluster](https://github.com/pixelchrome/files/raw/master/images/ntap_ansible_demo/03_setup_cluster.gif)

## Add `passwords.yml` with `ansible-vault`

NetApp uses *http* or *https* communication. This requires a username and password combination to run each task of a playbook. This can be set with variable prompt, but thats not very useful for automation. 

```sh
$ echo 'password: NetApp01234' > vars/password.yml
$ ansible-vault encrypt vars/password.yml
$ cat vars/password.yml 
$ANSIBLE_VAULT;1.1;AES256
64633334303139343730323062323663343035663736643538356638313862353332386166353439
3537376237323831393838356430386464346533366362360a396561373133336166616637396336
37356263373031666636363339393766656663376564383330356632616630363062383762373064
3739643266346136350a323261323565346330306661373165316539613430386564623536353532
61373361343936663932626266363438656437653066323933393066626538646264
```

![Create passwords.yml with ansible-vault](https://github.com/pixelchrome/files/raw/master/images/ntap_ansible_demo/04_create_password.gif)

## `02_setup_svm.yml`

Create a NFS SVM

### Tasks

* Create SVM
* Create the Network Interface
* Setup NFS
* Create default export policy

Run this playbook. Provide the encryption password of the `password.yml` file via prompt.

```sh
$ ansible-playbook --vault-id @prompt 02_setup_svm.yml
```

![Setup the SVM](https://github.com/pixelchrome/files/raw/master/images/ntap_ansible_demo/05_setup_svm.gif)

## `03_setup_export_volume.yml`

Export a Volume

### Tasks

* Create Volume
* Create export policy
* Setup export rules

Write the password into the file `decrypt` and run the playbook without any further input

```sh
$ echo demo > decrypt
$ ansible-playbook --vault-id decrypt 03_setup_export_volume.yml
```

![Create and export a volume](https://github.com/pixelchrome/files/raw/master/images/ntap_ansible_demo/06_create_and_export_volume.gif)

## `04_host.yml`

Mount on a Server/Host the NFS Share

### Tasks

* Install `nfs-utils`
* Mount the NFS Share and add to `/etc/fstab`

Run the playbook with a comma separated host list. **Therefore you must add the comma at the end!**

```sh
$ ansible-playbook 04_setup_host.yml -i 192.168.11.225,
```

# Bonus :)

## Cleanup of the above `9*_cleanup_*.yml`

# Links and Notes

* This demo is inspired and forked from https://github.com/schmots1/insight-ansible
* [netapp.io - Ansible](https://netapp.io/tag/ansible/)
* [Getting Started with NetApp and Ansible](https://netapp.io/2018/10/08/getting-started-with-netapp-and-ansible-install-ansible/)
* [Can you keep a secret](https://netapp.io/2018/12/14/can-you-keep-a-secret/)
