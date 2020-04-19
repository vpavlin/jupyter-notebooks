#Ignore the FROM, it is overriden by OpenShift build
FROM centos7
ENV ENV=/opt/app-root/bin/activate

USER 0
RUN yum -y install llvm-toolset* llvm-devel*

USER 1001

ADD environment.yaml /tmp/environment.yaml

RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-ppc64le.sh &&\
    bash Miniconda3-latest-Linux-ppc64le.sh -b -p /opt/app-root/miniconda3 &&\
    source /opt/app-root/miniconda3/etc/profile.d/conda.sh &&\
    conda update -y conda &&\
    conda env create --file /tmp/environment.yaml

ADD activate.add /tmp/activate.add

RUN cat /tmp/activate.add >> /opt/app-root/bin/activate

RUN chown -R 1001:0 ${APP_ROOT} &&\
    fix-permissions ${APP_ROOT}