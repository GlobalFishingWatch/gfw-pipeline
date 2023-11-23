FROM python:3.8-alpine
# The base image chosen comes from https://hub.docker.com/_/python
# The version 3.8 is equals to `3.8.<last>-buster` version

# Configure the working directory
RUN mkdir -p /opt/project
WORKDIR /opt/project

RUN  \
  export CLOUD_SDK_APK_DEPS="curl gcc py-setuptools lsb-release openssh-client git" && \
  export CLOUD_SDK_PIP_DEPS="crcmod" && \
  apk update && \
  apk add $CLOUD_SDK_APK_DEPS && \
  pip install --upgrade pip \
  pip install -U $CLOUD_SDK_PIP_DEPS && \
  export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)"

# Downloading gcloud package
RUN curl https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz > /tmp/google-cloud-sdk.tar.gz

# Installing the package
RUN \
  mkdir -p /usr/local/gcloud \
  && tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz \
  && /usr/local/gcloud/google-cloud-sdk/install.sh

# Adding the package path to local
ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin

# gcloud config
RUN \
  gcloud config set core/disable_usage_reporting true && \
  gcloud config set component_manager/disable_update_check true && \
  gcloud config set metrics/environment github_docker_image


# Setup a volume for configuration and auth data
VOLUME ["/root/.config"]
