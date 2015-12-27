FROM ubuntu:15.04

RUN echo "nameserver 8.8.8.8" >> /etc/resolv.conf
RUN apt-get update && \
    apt-get install --no-install-recommends -y software-properties-common && \
    apt-add-repository ppa:ansible/ansible && \
    apt-get update && \
    apt-get install -y ansible

RUN echo '[local]\nlocalhost\n' > /etc/ansible/hosts

ADD provisioning /srv/provisioning
WORKDIR /srv/provisioning

RUN ansible-playbook playbook.yml -c local

CMD [ "php", "-a" ]
