FROM centos:latest

ADD node-v6.9.1-linux-x64.tar.xz /opt/

WORKDIR /opt/

RUN ln -sf /opt/node-v6.9.1-linux-x64/bin/node /usr/bin/node && mkdir /opt/m-app/

ADD server.js /opt/m-app/

EXPOSE 80

CMD node /opt/m-app/server.js


