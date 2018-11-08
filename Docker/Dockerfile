# Base image (Ubuntu 18.04) of JupyterHub with jupyter and the R kernel.

FROM jupyterhub/jupyterhub:0.9.4
MAINTAINER Davide Albanese <davide.albanese@gmail.com>

RUN apt-get update && apt-get install -y \
    gnupg

# Add R 3.5 CRAN Repo for Ubuntu 18.04
RUN echo "deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9

RUN apt-get update && apt-get install -y \
    r-base r-base-dev \
    # for R devtools
    libcurl4-gnutls-dev libssl-dev libssh2-1-dev \
    # for jupyter notebook PDF export
    pandoc texlive-xetex \
  && rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip \
  && pip install setuptools jupyter

# R kernel
RUN R -e "install.packages('devtools', repos = 'http://cran.us.r-project.org')"
RUN R -e "devtools::install_github('IRkernel/IRkernel')"
# register the kernel system-wide
RUN R -e "IRkernel::installspec(user = FALSE)" 
