FROM ubuntu:14.04

MAINTAINER Dirk Hessenmueller <dirk.hessenmueller@deutschebahn.com>

# Install Ansible from source (master)
RUN apt-get -y update && \
    apt-get install -y software-properties-common openssh-server sudo curl git python-pip mysql-client  && \
    apt-add-repository ppa:ansible/ansible && \
    apt-get -y update && \
    apt-get -y install ansible && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# Install semaphore
RUN mkdir /playbooks
ADD semaphore /opt/semaphore
ADD semaphore_config.template /playbooks/semaphore_config.template
ADD semaphore.sql /playbooks/semaphore.sql
ADD semaphore_init /opt/semaphore_init
RUN chmod 755 /opt/semaphore
RUN chmod 755 /opt/semaphore_init

# set timezone
ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

EXPOSE 3000
# CMD ["/opt/semaphore", "-config", "/playbooks/semaphore_config.json"]
CMD ["/opt/semaphore_init"]

