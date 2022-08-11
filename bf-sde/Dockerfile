#first stage build code
FROM stratumproject/build:21.06 as builder

ENV BLD_HOME=/root
ENV SDE_TAR=bf-sde-9.9.0.tgz
ENV SDE_PREFIX=bf-sde-9.9.0
ENV SDE_VERSION=9.9.0

ADD ${SDE_TAR} ${BLD_HOME}/

WORKDIR ${BLD_HOME}/${SDE_PREFIX}

RUN find p4studio -type f -name "*.py" -exec sed -i "s/wget/wget --no-check-certificate /g" {} \;

RUN cd p4studio && ./install-p4studio-dependencies.sh && ./p4studio profile apply ./profiles/all-tofino.yaml

#RUN mv install /usr/local/p4 && chown -Rf root:staff /usr/local/p4 && cd ..

#WORKDIR ${BLD_HOME}

#RUN rm -rf ${SDE_PREFIX}


#second stage copy build result
FROM stratumproject/build:21.06

ENV BLD_HOME=/root
ENV SDE_PREFIX=bf-sde-9.9.0

COPY --from=builder ${BLD_HOME}/${SDE_PREFIX}/install /usr/local/p4
RUN chown -Rf root:root /usr/local/p4

ENV PATH="$PATH:/usr/local/p4/bin"

RUN apt-get update && apt-get install -y python3-packaging
