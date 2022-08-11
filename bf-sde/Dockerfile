FROM stratumproject/build:21.06

ENV BLD_HOME=/root
ENV SDE_TAR=bf-sde-9.9.0.tgz
ENV SDE_PREFIX=bf-sde-9.9.0
ENV SDE_VERSION=9.9.0
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:${BLD_HOME}/install/bin

ADD ${SDE_TAR} ${BLD_HOME}/

WORKDIR ${BLD_HOME}/${SDE_PREFIX}

RUN find p4studio -type f -name "*.py" -exec sed -i "s/wget/wget --no-check-certificate /g" {} \;

RUN cd p4studio && ./install-p4studio-dependencies.sh && ./p4studio profile apply ./profiles/all-tofino.yaml

RUN mv install ../ && cd ..

WORKDIR ${BLD_HOME}

#RUN apt install -y python3-packaging

ENTRYPOINT ["tail"]
CMD ["-f","/dev/null"]

#ENTRYPOINT []
#CMD ["/bin/bash"]
