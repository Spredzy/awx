FROM centos:7

ARG NPMRC_FILE

RUN yum -y update && yum -y install epel-release && yum -y install https://centos7.iuscommunity.org/ius-release.rpm

RUN yum install -y \
    bzip2 \
    gcc-c++ \
    git2u \
    git2u-core \
    make \
    nodejs \
    npm

WORKDIR /awx

COPY awx/ui/package.json awx/ui/package.json
COPY VERSION ${NPMRC_FILE}* /root/

RUN npm config list

RUN npm --prefix=awx/ui install

COPY awx/ui/test/e2e awx/ui/test/e2e

ENTRYPOINT ["npm", "--prefix=awx/ui", "run", "e2e", "--", "--env=cluster"]
