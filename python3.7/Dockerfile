FROM python:3.7
# The base image chosen comes from https://hub.docker.com/_/python
# The version 3.7 is equals to `3.7.<last>-buster` version

# Configure the working directory
RUN mkdir -p /opt/project
WORKDIR /opt/project


ARG CLOUD_SDK_VERSION=349.0.0
ENV CLOUD_SDK_VERSION=$CLOUD_SDK_VERSION
RUN  \
  export CLOUD_SDK_APT_DEPS="curl gcc apt-transport-https lsb-release openssh-client git" && \
  export CLOUD_SDK_PIP_DEPS="crcmod" && \
  apt-get -qqy update && \
  apt-get -qqy dist-upgrade && \
  apt-get install -qqy $CLOUD_SDK_APT_DEPS && \
  pip install -U $CLOUD_SDK_PIP_DEPS && \
  pip install -U "setuptools" && \
  export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
  echo "deb https://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" > /etc/apt/sources.list.d/google-cloud-sdk.list && \
  curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
  apt-get update && \
  apt-get install -y google-cloud-sdk=${CLOUD_SDK_VERSION}-0 && \
  gcloud config set core/disable_usage_reporting true && \
  gcloud config set component_manager/disable_update_check true && \
  gcloud config set metrics/environment github_docker_image

# Setup a volume for configuration and auth data
VOLUME ["/root/.config"]
