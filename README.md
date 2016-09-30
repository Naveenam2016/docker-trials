

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
sudo HTTP_PROXY=http://my-proxy:80/ /usr/bin/docker -d &  -- obsolete now with 1.12

$ mkdir /etc/systemd/system/docker.service.d
$ vim /etc/systemd/system/docker.service.d/http-proxy.conf
[Service]
Environment=”HTTP_PROXY=http://my-proxy:80″
...
EnvironmentFile=/etc/default/docker


***** OR *****

$ vim /lib/systemd/system/docker.service
...
[Service]
Environment="HTTP_PROXY=http://my-proxy:80/ HTTPS_PROXY=http://my-proxy:80/"
ExecStart=/usr/bin/docker -d -H fd:// $DOCKER_OPTS
...
EnvironmentFile=-/etc/default/docker
...

***** FINALLY *****

$ systemctl daemon-reload
$ systemctl restart docker


```

#### Disable SELinux settings
```
$ vi /etc/sysconfig/docker.rpmsave

# Remove --selinux-enabled from OPTIONS
OPTIONS='--selinux-enabled --log-driver=journald'

# uncomment following line
setsebool -P docker_transition_unconfined
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

#### Mount volume from host with disabling SELinux
```
Temporary solution : su -c "setenforce 0" 
Permenant soln     : chcon -Rt svirt_sandbox_file_t /path/to/volume
```

#### Start service from dockerfile
```
ENTRYPOINT service nginx start && bash
```
#### Add /etc/hosts to Dockerfile
```

Create a writable copy of /etc/hosts somewhere where the path will be the same length. I used /tmp/hosts:

RUN cp /etc/hosts /tmp/hosts
Then you need to make a copy of libnss_files.so that you can edit:

RUN mkdir -p -- /lib-override && cp /lib/x86_64-linux-gnu/libnss_files.so.2 /lib-override
Now edit the binary to replace /etc/hosts with the path to the writable hosts file (ex. /tmp/hosts):

RUN perl -pi -e 's:/etc/hosts:/tmp/hosts:g' /lib-override/libnss_files.so.2
Finish up by letting the system know where to find the edited binary:

ENV LD_LIBRARY_PATH /lib-override
```

