FROM rhel7

MAINTAINER docker@softwarecollections.org

RUN yum install -y --setopt=tsflags=nodocs yum-utils && \
    yum-config-manager --enable rhel-server-rhscl-7-rpms && \
    yum-config-manager --enable rhel-7-server-optional-rpms && \
    yum clean all

RUN yum install -y --setopt=tsflags=nodocs devtoolset-4-gcc devtoolset-4-gcc-c++ devtoolset-4-gcc-gfortran devtoolset-4-gdb && yum clean all



ENV	BASH_ENV=/etc/profile.d/cont-env.sh


ADD ./enabledevtoolset-4.sh /usr/share/cont-layer/common/env/enabledevtoolset-4.sh
ADD ./usr /usr
ADD ./etc /etc
ADD ./root /root

ENV HOME /home/default
RUN     groupadd -r default -f -g 1001 && \
        useradd -u 1001 -r -g default -d ${HOME} -s /sbin/nologin \
                        -c "Default Application User" default

USER 1001

ENTRYPOINT ["/usr/bin/container-entrypoint"]

CMD ["container-usage"]
