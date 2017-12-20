#
# Install cling into a pre-cooked jupyter notebook service.
#

FROM jupyter/datascience-notebook
USER root

# install cling and cling kernel
RUN  mkdir /cling                                   && \
     cd /cling                                      && \
     apt-get update                                 && \
     apt-get install -y cmake                       && \
     apt-get install -y libxml2-dev                 && \
     git clone http://root.cern.ch/git/llvm.git src && \
     cd src                                         && \
     git checkout cling-patches                     && \
     cd tools                                       && \
     git clone http://root.cern.ch/git/cling.git    && \
     git clone http://root.cern.ch/git/clang.git    && \
     cd clang                                       && \
     git checkout cling-patches                     && \
     cd ../../..                                    && \
     mkdir build                                    && \
     cd build                                       && \
     cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DCMAKE_BUILD_TYPE=Release ../src && \
     cmake --build . -- -j4                         && \
     cmake --build . --target install               && \
     cd /usr/local/share/cling/Jupyter/kernel       && \
     chmod -R 777 /home/jovyan/.cache               && \
     pip install -e .                               && \
     jupyter-kernelspec install cling-cpp17         && \
     jupyter-kernelspec install cling-cpp1z         && \
     jupyter-kernelspec install cling-cpp14         && \
     jupyter-kernelspec install cling-cpp11         && \
     chmod -R 775 /home/jovyan/.cache               && \
     chown -R jovyan.users /home/jovyan/.cache      && \
     rm -rf /cling

USER jovyan
     

