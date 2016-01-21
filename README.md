
#### Update resolv.conf
```
echo "nameserver 172.18.20.13" >> /etc/resolv.conf
echo "nameserver 172.20.100.29" >> /etc/resolv.conf
echo "nameserver 8.8.8.8" >> /etc/resolv.conf
```

#### Setting DOCKER_OPTS
```
touch /etc/default/docker
echo 'DOCKER_OPTS="--dns 172.18.20.13 --dns 172.20.100.29 --dns 8.8.8.8"' >> /etc/default/docker
```

#### Run behind a proxy
```
sudo HTTP_PROXY=http://my-proxy:80/ /usr/bin/docker -d &
```

#### Partition information
```
sudo fdisk -l
sudo sfdisk -l -uM
cfdisk 
sudo parted -l
df -h
df -h | grep ^/dev
pydf
lsblk
blkid
hwinfo --block --short
```

#### Update linux kernel
```
yum list --showduplicates kernel
on /etc/yum.conf, add exclude=kernel so that the current kernel is not updated
update the /etc/yum.repos.d/*.repo
make enabled=1 for the required kernel
yum update -y
yum install kernel-<complete-version>
```
