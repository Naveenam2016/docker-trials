#### git prompt
```
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

export PS1="\u@\h [\W]\[\033[32m\]\$(parse_git_branch)\[\033[00m\] $ "
```



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

First, create a directory for drop-in configuration for docker:

mkdir /etc/systemd/system/docker.service.d

Now, create a file called /etc/systemd/system/docker.service.d/http-proxy.conf that adds the environment variable:

[Service]
Environment=”HTTP_PROXY=http://my-proxy:80″

To apply the change, reload the unit and restart docker:
systemctl daemon-reload
systemctl restart docker
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

#### Update linux kernel from 3 to 4
```
yum list --showduplicates kernel
on /etc/yum.conf, add exclude=kernel so that the current kernel is not updated
update the /etc/yum.repos.d/*.repo
make enabled=1 for the required kernel
yum update -y
yum install kernel-<complete-version>
```
