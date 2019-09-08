# jupinger
Docker files for a docker image with jupyter and cling. The main docker image is in subdirectory jupyter-cling.

This image is simply an installation of [xeus-cling](https://github.com/QuantStack/xeus-cling) on top 
of a [miniconda3](https://docs.anaconda.com/anaconda/user-guide/tasks/integration/docker) docker layer.

Example invocation:
```
docker run -it --rm --mount type=bind,source="$(pwd)"/work,target=/work -p 8888:8888 dhavenith/jupyter-cling
```
