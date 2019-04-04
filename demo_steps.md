# Tech Forum Ansible Demo

## Before running any playbooks:

Run this on ONTAP
```sh
aggr show
```

```sh
disk show -container-type spare
```

```sh
vserver show
```

```sh
volume show
```

Run this on the Linux Guest

```sh
mount
```

```sh
df
```


## Run ansible-playbook 01_setup_cluster.yml

On the Ansible Host
```sh
ansible-playbook 01_setup_cluster.yml
```
Run this on ONTAP
```sh
aggr show
```
```sh
disk show -container-type spare
```

## Run ansible-playbook 02_setup_svm.yml

```sh
ansible-playbook 02_setup_svm.yml
```
Run this on ONTAP

```sh
vserver show
```

```sh
volume show
```


## Run ansible-playbook 03_setup_export_volume.yml

```sh
ansible-playbook 03_setup_export_volume.yml
```
Run this on ONTAP

```sh
volume show
```

## Run ansible-playbook 04_setup_host.yml
Run this on the Linux Guest

```sh
mount
```

```sh
df
```


```sh
ansible-playbook 04_setup_host.yml
```

Run this on the Linux Guest

```sh
mount
```

```sh
df
```
