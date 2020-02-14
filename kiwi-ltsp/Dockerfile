FROM opensuse/leap:42.3
MAINTAINER Michael Chang <mchang@suse.com>

ENV container docker

RUN zypper ar --repo http://download.opensuse.org/repositories/server:/ltsp/openSUSE_Leap_42.3/server:ltsp.repo

RUN zypper -n --gpg-auto-import-keys install kiwi-ltsp kiwi-image-ltsp kiwi-image-ltsp-boot

# https://github.com/openSUSE/docker-containers/tree/master/derived_images/systemd
RUN zypper -n install systemd; zypper clean ; \
(cd /usr/lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /usr/lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /usr/lib/systemd/system/local-fs.target.wants/*; \
rm -f /usr/lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /usr/lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /usr/lib/systemd/system/basic.target.wants/*;\
rm -f /usr/lib/systemd/system/anaconda.target.wants/*;

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/lib/systemd/systemd", "--system"]
