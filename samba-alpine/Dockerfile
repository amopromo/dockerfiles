FROM centos:7
MAINTAINER anakinpendragon - anakinpendragon@gmail.com 
ENV SAMBA_VERSION samba-4.11.4
RUN yum -y groupinstall "Development Tools" && \
yum -y install epel-release && \
yum -y install cups-devel wget python3-devel attr bind-utils docbook-style-xsl gcc gdb krb5-workstation libsemanage-python libxslt perl perl-ExtUtils-MakeMaker \
perl-Parse-Yapp perl-Test-Base pkgconfig policycoreutils-python \
python2-crypto gnutls-devel libattr-devel keyutils-libs-devel libacl-devel libaio-devel libblkid-devel libxml2-devel openldap-devel \
pam-devel popt-devel python-devel readline-devel zlib-devel systemd-devel \
lmdb-devel jansson-devel gpgme-devel pygpgme libarchive-devel autoconf automake gcc gdb krb5-devel krb5-workstation \
openldap-devel make pam-devel python-devel docbook-style-xsl libacl-devel libattr-devel libxslt libtasn1-devel.x86_64 libtasn1.x86_64  libtasn1-tools && \
mkdir -p /tmp/src && \
cd /tmp/src && \
wget https://download.samba.org/pub/samba/${SAMBA_VERSION}.tar.gz && \
tar -zxvf ${SAMBA_VERSION}.tar.gz && \
cd /tmp/src/${SAMBA_VERSION} && \
./configure   && \
make install && \
yum remove cups-devel wget gcc gnutls-devel libattr-devel keyutils-libs-devel python-devel && \
rm -rf /tmp/src && \
yum clean all && \ 
# forward request and error logs to docker log collector
#    ln -sf /dev/stdout  /usr/local/samba/var/log.samba && \
#    ln -sf /dev/stderr /usr/local/samba/var/log.smbd
#WORKDIR /
#COPY nginx.conf /etc/nginx
EXPOSE 37/udp 53 88 135/tcp 137/udp 138/udp 139 389 445 464 636/tcp 1024-5000/tcp 3268/tcp 3269/tcp
CMD ["samba", "-D"] 
