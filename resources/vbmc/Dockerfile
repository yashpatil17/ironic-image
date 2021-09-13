ARG BASE_IMAGE=docker.io/centos:centos8

FROM $BASE_IMAGE



RUN dnf install -y python3 python3-requests python3-pip && \
     curl https://raw.githubusercontent.com/openstack/tripleo-repos/master/plugins/module_utils/tripleo_repos/main.py | python3 - -b master current-tripleo --no-stream && \
     dnf upgrade -y && \
     dnf install -y python3-virtualbmc && \
     dnf clean all && \
     rm -rf /var/cache/{yum,dnf}/*

RUN mkdir -p /etc/pf9/certs/libvirt 
RUN wget https://artifactory.platform9.horse/artifactory/pf9-bins/ironic/df-us-mpt1-kvm/certs/v2/ca/cert.pem -o /etc/pf9/certs/libvirt/cacert.pem 
RUN wget https://artifactory.platform9.horse/artifactory/pf9-bins/ironic/df-us-mpt1-kvm/certs/v2/hostagent/key.pem -o /etc/pf9/certs/libvirt/clientkey.pem
RUN wget https://artifactory.platform9.horse/artifactory/pf9-bins/ironic/df-us-mpt1-kvm/certs/v2/hostagent/cert.pem -o /etc/pf9/certs/libvirt/clientcert.pem
CMD /usr/bin/vbmcd --foreground

