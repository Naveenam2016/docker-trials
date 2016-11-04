FROM centos:latest

ENV http_proxy http://103.27.171.34:9480
ENV https_proxy http://103.27.171.34:9480

ADD nginx.repo /etc/yum.repos.d/

RUN yum install -y nginx

ADD nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]

# CMD systemctl start nginx && bash 
