FROM centos:centos7
MAINTAINER liz <rick.lizhan@gmail.com>

RUN yum -y update &&\
    yum -y install kde-l10n-Chinese telnet &&\
    yum -y reinstall glibc-common &&\
    yum -y install openssh-server openssh-clients passwd sudo &&\
    yum -y install net-tools &&\
    yum clean all &&\
    rm -rf /tmp/* rm -rf /var/cache/yum/* &&\
    localedef -i en_US -f UTF-8 en_US.UTF-8 &&\
    localedef -c -f UTF-8 -i zh_CN zh_CN.utf8

RUN mkdir /var/run/sshd &&\
    ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''

RUN useradd --create-home -s /bin/bash vagrant &&\
    echo -e "vagrant\nvagrant" | (passwd --stdin vagrant) &&\
    echo 'vagrant ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/vagrant &&\
    chmod 440 /etc/sudoers.d/vagrant

RUN mkdir -p /home/vagrant/.ssh &&\
    chmod 700 /home/vagrant/.ssh &&\
    echo "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA6NF8iallvQVp22WDkTkyrtvp9eWW6A8YVr+kz4TjGYe7gHzIw+niNltGEFHzD8+v1I2YJ6oXevct1YeS0o9HZyN1Q9qgCgzUFtdOKLv6IedplqoPkcmF0aYet2PkEDo3MlTBckFXPITAMzF8dJSIFo9D8HfdOV0IAdx4O7PtixWKn5y2hMNG0zQPyUecp4pzC6kivAIhyfHilFR61RGL+GPXQ2MWZWFYbAGjyiYJnAmCP3NOTd0jMZEnDkbUvxhMmBYSdETk1rRgm+R4LOzFUGaHqHDLKLX+FIPKcF96hrucXzcWyLbIbEgE98OHlnVYCzRdK8jlqm8tehUc9c9WhQ==" > /home/vagrant/.ssh/authorized_keys &&\
    chmod 600 /home/vagrant/.ssh/authorized_keys &&\
    chown -R vagrant:vagrant /home/vagrant/.ssh

EXPOSE 22

ENTRYPOINT ["/usr/sbin/sshd", "-D"]
