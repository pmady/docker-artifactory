FROM baselibrary/java:8
MAINTAINER ShawnMa <qsma@thoughtworks.com>

## Version
ENV ARTIFACTORY_MAJOR   4
ENV ARTIFACTORY_VERSION 4.13.0

## Repository
RUN \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys D7639232 &&\
  echo "deb https://jfrog.bintray.com/artifactory-pro-debs trusty main" > /etc/apt/sources.list.d/artifactory.list

## Packages
RUN \
  apt-get update &&\
  apt-get install -y jfrog-artifactory-pro=$ARTIFACTORY_VERSION &&\
  mkdir -p /etc/opt/jfrog/artifactory /var/opt/jfrog/artifactory/{data,logs,backup} &&\
  chown -R artifactory: /etc/opt/jfrog/artifactory /var/opt/jfrog/artifactory/{data,logs,backup} &&\
  mkdir -p /var/opt/jfrog/artifactory/defaults/etc &&\
  cp -rp /etc/opt/jfrog/artifactory/* /var/opt/jfrog/artifactory/defaults/etc/ &&\
  rm -rf /var/lib/apt/lists/*

## Scripts
ADD docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod a+x            /docker-entrypoint.sh

ENV ARTIFACTORY_HOME /var/opt/jfrog/artifactory

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 8081

VOLUME ["/var/lib/artifactory"]
