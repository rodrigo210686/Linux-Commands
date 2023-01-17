Comandos dia a dia


## Extend a existent LVM disk

```shell

#### Resize an existent LVM disk
###Steps

1 - Take Snapshot of disk
2 - Increase disk in AWS console
3 - Run the commands below:

## get the pv with
pvs 

## resize pv
pvresize /dev/sdb

## Get lvm that you need increase
lvdisplay

lvextend -l +100%FREE /dev/vg01/lv01


resize2fs /dev/vg01/lv01

/dev/vg02/lv02




```

### Create a new LVM volume
```shell
#### Create a new LVM volume

fdisk -l

## Get partition path in this case  /dev/xvdf

pvcreate /dev/xvdf


## Rode um pvscan
[root@ip-172-31-90-200 ~]# pvscan
  PV /dev/sdb   VG vg01            lvm2 [<40.00 GiB / 0    free]
  PV /dev/sdf                      lvm2 [10.00 GiB]
  Total: 2 [<50.00 GiB] / in use: 1 [<40.00 GiB] / in no VG: 1 [10.00 GiB]

### Get de new PV and create LVM

vgcreate vg02 /dev/sdf

lvcreate -l 100%FREE -n lv02 vg02

lvdisplay


mkfs.ext4 /dev/vg02/lv02

### mount lvm to a partition

mkdir /logs

mount /dev/vg02/lv02 /logs


```


### Compactar arquivos em partes

Teste utilizado no EFS estruturantes
```sh
######## Estratégia

### Compress

tar -cf - --ignore-failed-read -C upload2/ . | gzip | split -b 100M - migrate-data/_upload-dir.tar.gz.

#### Extract

cat migrate-data/_upload-dir.tar.gz.* | gunzip | (cd /opt/citsmart/extract-data && tar xf -)

#### Teste realizado

Volume de upload de 1.6GB
Reduziu para 1.4 GB depois de zipado e dividido.

```
