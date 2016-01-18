
echo "nameserver 172.18.20.13" >> /etc/resolv.conf
echo "nameserver 172.20.100.29" >> /etc/resolv.conf
echo "nameserver 8.8.8.8" >> /etc/resolv.conf


touch /etc/default/docker
echo 'DOCKER_OPTS="--dns 172.18.20.13 --dns 172.20.100.29 --dns 8.8.8.8"' >> /etc/default/docker

sudo HTTP_PROXY=http://my-proxy:80/ /usr/bin/docker -d &


