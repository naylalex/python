# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.203.0/containers/python-3-miniconda/.devcontainer/base.Dockerfile

FROM mcr.microsoft.com/vscode/devcontainers/miniconda:0-3

# [Choice] Node.js version: none, lts/*, 16, 14, 12, 10
ARG NODE_VERSION="none"
RUN if [ "${NODE_VERSION}" != "none" ]; then su vscode -c "umask 0002 && . /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi

# Copy environment.yml (if found) to a temp location so we update the environment. Also
# copy "noop.txt" so the COPY instruction does not fail if no environment.yml exists.
COPY environment.yml* .devcontainer/noop.txt /tmp/conda-tmp/
RUN if [ -f "/tmp/conda-tmp/environment.yml" ]; then umask 0002 && /opt/conda/bin/conda env update -n base -f /tmp/conda-tmp/environment.yml; fi \
    && rm -rf /tmp/conda-tmp

# [Optional] Uncomment to install a different version of Python than the default
# RUN conda install -y python=3.6 \
#     && pip install --no-cache-dir pipx \
#     && pipx reinstall-all
# TODO: Confirm if it needed to install notebook and ipykernel
#Per https://pythonspeed.com/articles/activate-conda-dockerfile/
SHELL ["/bin/bash", "--login", "-c"]

#RUN conda init bash
RUN conda create --name pyclass python=3.8
# conda activate pyclass fails as the shell has not been activated
# check if RUN activate pyclass fixes the issue
RUN conda init bash
RUN echo "conda activate pyclass" > ~/.bashrc
RUN conda activate pyclass
RUN conda install --name pyclass ipykernel
RUN conda install --name pyclass notebook
RUN conda install --name pyclass numpy
RUN conda install --name pyclass pandas
RUN conda install --name pyclass matplotlib
RUN conda install --name pyclass scikit-learn

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
