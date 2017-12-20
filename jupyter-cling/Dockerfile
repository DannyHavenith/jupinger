#
# create a cling-jupyter notebook service
# 
# for more information, see these sources:
# https://blog.jupyter.org/interactive-workflows-for-c-with-jupyter-fe9b54227d92
# https://docs.anaconda.com/anaconda/user-guide/tasks/integration/docker
# https://github.com/QuantStack/xeus-cling
# 
FROM continuumio/miniconda3

RUN apt-get install -y gcc
RUN conda install cling -c QuantStack -c conda-forge -y      && \
    conda install xeus-cling -c QuantStack -c conda-forge -y && \
    conda install notebook -c conda-forge -y
RUN useradd -ms /bin/bash notebooker

USER       notebooker
WORKDIR    /home/notebooker
ENV        PATH "/opt/conda/bin/jupyter:$PATH"
ENTRYPOINT jupyter notebook --ip='*' --port=8888 --no-browser
