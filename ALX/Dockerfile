# ---> Description <---
#
# Docker file to spin up an ubuntu box for ALX coding projects
#

FROM gr00ti3/ubuntu_template:latest
LABEL maintainer "iAmG-r00t @th3_gr00t 😀"

# add d3v user to sudoer's
RUN usermod -aG sudo d3v

# install mysql-server, nodejs
RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y mysql-server nodejs --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

# install puppet and puppet-lint the right way in ubuntu focal
RUN wget https://apt.puppet.com/puppet7-release-focal.deb && \
    dpkg -i puppet7-release-focal.deb && \
    apt-get update && \
    apt-get install puppet-agent puppet-lint -y && \
    rm -rf /var/lib/apt/lists/*

# fix some error with mysql on docker container
RUN sudo service mysql stop && \
    usermod -d /var/lib/mysql/ mysql


USER d3v
SHELL ["/bin/bash","-c","-l"]
WORKDIR /home/d3v
RUN echo "source /etc/profile.d/puppet-agent.sh" >> /tmp/puppet-path
RUN /bin/bash -C "/tmp/puppet-path"
RUN rm -f /tmp/puppet-path
