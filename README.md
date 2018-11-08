# JupyterHub - CompBio fmach

JupyterHub image with jupyter and the R kernel.

- base image: jupyterhub/jupyterhub:0.9.4
- R 3.5

Build with:
    
`docker build --tag jupyterhub .`


## Run JupyterHub and create the users

```bash
CONF_ABS_PATH=$PWD/conf # configurations on host
HOME_HOST_ABS_PATH=$PWD/home_host # homes on host
SHARED_DATA_ABS_PATH=$PWD/shared # read-only shared

docker run -d -p 80:8000 \
    -v "$CONF_ABS_PATH":/conf \
    -v "$HOME_HOST_ABS_PATH":/home_host \
    -v "$SHARED_DATA_ABS_PATH":/shared:ro \
    --name jhinstance jupyterhub \
    jupyterhub --config /conf/jupyterhub_config.py

# add users
docker exec -it jhinstance bash
root@de3e2265ba73: newusers /conf/users
root@de3e2265ba73: exit
```

## (Optional) create a new template configuration file

```bash
docker run --rm -it \
    -v "$CONF_ABS_PATH":/conf \
    --name jhinstance \
    jupyterhub /bin/bash
root@de3e2265ba73: jupyterhub --generate-config
root@de3e2265ba73: exit
```
