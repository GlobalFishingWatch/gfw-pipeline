ARG PYTHON_VERSION=3.7

FROM python:${PYTHON_VERSION}
# The base image chosen comes from https://hub.docker.com/_/python
# The version ${PYTHON_VERSION} is equals to `${PYTHON_VERSION}.<last>-buster` version

# Configure the working directory
RUN mkdir -p /opt/project
WORKDIR /opt/project


ARG CLOUD_SDK_VERSION=435.0.1
ENV CLOUD_SDK_VERSION=$CLOUD_SDK_VERSION
RUN  \
  export CLOUD_SDK_APT_DEPS="curl apt-transport-https ca-certificates gnupg" && \
  export BACKWARDS_COMPAT_TOOLS="lsb-release git gcc openssh-client" && \
  export CLOUD_SDK_PIP_DEPS="crcmod" && \
  apt-get -qqy update && \
  apt-get -qqy dist-upgrade && \
  apt-get install -qqy $CLOUD_SDK_APT_DEPS $BACKWARDS_COMPAT_TOOLS && \
  pip install --no-cache-dir -U pip && \
  pip install --no-cache-dir -U $CLOUD_SDK_PIP_DEPS && \
  pip install --no-cache-dir -U "setuptools" && \
  curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg && \
  echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" > /etc/apt/sources.list.d/google-cloud-sdk.list && \
  apt-get update && \
  apt-get install -y google-cloud-cli=${CLOUD_SDK_VERSION}-0 && \
  gcloud config set core/disable_usage_reporting true && \
  gcloud config set component_manager/disable_update_check true && \
  gcloud config set metrics/environment github_docker_image

# Setup a volume for configuration and auth data
VOLUME ["/root/.config"]
