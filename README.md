# JupyterHub

JupyterHub image with jupyter and the R kernel.

- base image: jupyterhub/jupyterhub:0.9.4
- R 3.5

Build with:

```bash
cd Docker
docker build --tag jupyterhub .
```

## Run JupyterHub and create users

```bash

cd jupyterhub-base # (this folder)

CONF_ABS_PATH=$PWD/conf # configurations on host
HOME_HOST_ABS_PATH=$PWD/home_host # homes on host
SHARED_DATA_ABS_PATH=$PWD/shared # read-only shared

# run jupyterhub
docker run -d -p 80:8000 \
    -v "$CONF_ABS_PATH":/conf \
    -v "$HOME_HOST_ABS_PATH":/home_host \
    -v "$SHARED_DATA_ABS_PATH":/shared:ro \
    --name jhi \
    jupyterhub \
    jupyterhub --config /conf/jupyterhub_config.py

# add users
docker exec jhi newusers /conf/users.txt
```

## (Optional) create a new template configuration file

```bash
docker run --rm \
    -v "$CONF_ABS_PATH":/conf \
    -w /conf \
    jupyterhub \
    jupyterhub --generate-config
```

## Execute an interactive bash shell on the container

```bash
docker exec -it jhi bash
```
