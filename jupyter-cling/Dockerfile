#
# create a cling-jupyter notebook service
#
# for more information, see these sources:
# https://blog.jupyter.org/interactive-workflows-for-c-with-jupyter-fe9b54227d92
# https://docs.anaconda.com/anaconda/user-guide/tasks/integration/docker
# https://github.com/QuantStack/xeus-cling
#
#

ARG BOOST_VERSION="1.89.0"
ARG BOOST_VERSION_FILE="1_89_0"

FROM continuumio/miniconda3

# install boost
ARG BOOST_VERSION
ARG BOOST_VERSION_FILE
RUN apt-get update                  && \
    apt-get install -y curl gcc g++ && \
    mkdir /boost                    && \
    cd /boost                       && \
    curl -L https://archives.boost.io/release/${BOOST_VERSION}/source/boost_${BOOST_VERSION_FILE}.tar.gz --output boost_${BOOST_VERSION_FILE}.tar.gz && \
    tar -xzf boost_${BOOST_VERSION_FILE}.tar.gz    && \
    cd /boost/boost_${BOOST_VERSION_FILE}          && \
    ./bootstrap.sh                  && \
    ./b2 install -d0 --without-wave --without-python && \
    cd /                            && \
    rm -rf boost                    && \
    apt-get -qq -y remove curl      && \
    apt-get -qq -y autoremove       && \
    apt-get autoclean               && \
    rm -rf /var/lib/apt/lists/* /var/log/dpkg.log

RUN conda install cling -c QuantStack -c conda-forge -y      && \
    conda install xeus-cling -c QuantStack -c conda-forge -y && \
    conda install notebook -c conda-forge -y                 && \
    conda clean --all --yes

# set up user and environment
ENV     PATH /opt/conda/bin:$PATH
RUN     useradd -ms /bin/bash notebooker
COPY    start-notebook.sh /usr/local/bin
USER    notebooker
WORKDIR /home/notebooker
CMD     start-notebook.sh
