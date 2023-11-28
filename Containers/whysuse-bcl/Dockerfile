FROM registry.suse.com/bci/bci-base:15.5
LABEL maintainer="Anthony Tortola <atortola@suse.com>"

ARG repo
ARG cert

RUN echo "$cert" > /etc/pki/trust/anchors/RHN-ORG-TRUSTED-SSL-CERT.pem
RUN update-ca-certificates
RUN echo "$repo" > /etc/zypp/repos.d/susemanager:dockerbuild.repo

ADD add_packages.sh /root/add_packages.sh
RUN /root/add_packages.sh

RUN zypper up -y

ADD pub.conf /etc/apache2/conf.d/pub.conf
COPY _site /srv/www/htdocs/

CMD /usr/sbin/start_apache2 -DFOREGROUND -k start