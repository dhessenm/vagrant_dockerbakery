FROM ubuntu:14.04

# Install Ansible from source (master)
RUN apt-get -y update && \
    apt-get install -y software-properties-common openssh-server sudo git && \
    apt-add-repository ppa:ansible/ansible && \
    apt-get -y update && \
    apt-get -y install ansible && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# sshd
RUN mkdir /var/run/sshd

# create ansible user
RUN groupadd -g 1001 ansible && \
    mkdir /app && \
    useradd -u 1001 -g 1001 -s /bin/bash -c "ansible user" -d /app/ansible -m ansible && \
    echo "ansible:ansible" | chpasswd

# setup ssh directory
RUN mkdir /app/ansible/.ssh && \
    chown ansible:ansible /app/ansible/.ssh && \
    chmod 700 /app/ansible/.ssh

# ADD ansible_id_rsa /app/ansible/.ssh/id_rsa
# ADD ansible_id_rsa.pub /app/ansible/.ssh/id_rsa.pub

ADD ansible.cfg /app/ansible/.ansible.cfg
ADD hosts /app/ansible/hosts

# RUN chown ansible:ansible /app/ansible/.ssh/id_rsa && \
    # chown ansible:ansible /app/ansible/.ssh/id_rsa.pub && \
    # chmod 600 /app/ansible/.ssh/id_rsa && \
    # chmod 644 /app/ansible/.ssh/id_rsa.pub && \

RUN chown ansible:ansible /app/ansible/.ansible.cfg && \
    chown ansible:ansible /app/ansible/hosts

# set sudo for user ansible
RUN echo '%ansible ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

