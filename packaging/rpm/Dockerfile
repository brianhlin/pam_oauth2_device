# Default to EL8 builds
ARG IMAGE_BASE=quay.io/almalinux/almalinux:8

FROM $IMAGE_BASE

# "ARG IMAGE_BASE" needs to be here again because the previous instance has gone out of scope.
ARG IMAGE_BASE=quay.io/almalinux/almalinux:8
ARG TARBALL_URL=https://github.com/CHTC/pam_oauth2_device/archive/v0.1.3.chtc.tar.gz

RUN yum install -y \
    gcc \
    gcc-c++ \
    libcurl-devel \
    make \
    openldap-devel \
    pam-devel \
    rpm-build \
 && yum clean all

RUN groupadd builder \
 && useradd --create-home -u 1000 -g 1000 builder

USER builder

WORKDIR /home/builder

RUN mkdir -p rpmbuild/SOURCES \
 && cd rpmbuild/SOURCES \
 && curl -L -O $TARBALL_URL

COPY pamoauth2device.spec .

USER root

RUN chown builder:builder pamoauth2device.spec

USER builder

RUN rpmbuild -ba pamoauth2device.spec
