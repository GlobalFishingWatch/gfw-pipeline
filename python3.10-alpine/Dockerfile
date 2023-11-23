FROM busybox as cloudsdk

ARG CLOUD_SDK_VERSION=349.0.0
ENV CLOUD_SDK_VERSION=$CLOUD_SDK_VERSION

# Download gcloud cli package to install
RUN wget \
  -O /tmp/google-cloud-sdk.tar.gz \
  https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-$CLOUD_SDK_VERSION-linux-$(arch).tar.gz


# Base python image
FROM python:3.10-alpine as base

COPY --from=cloudsdk /tmp/google-cloud-sdk.tar.gz /tmp/google-cloud-sdk.tar.gz

# Configure the working directory
RUN mkdir -p /opt/project
WORKDIR /opt/project

ENV CLOUD_SDK_APK_DEPS "gcc py-setuptools lsb-release openssh-client"
ENV APK_DEPS "curl openssh-client git"
ENV CLOUD_SDK_PIP_DEPS "crcmod"

# Update and upgrade alpine packages
RUN  \
  apk update && \
  apk upgrade --no-cache && \
  pip install --upgrade pip

# Image used
FROM base as build 

# Install gcloud required dependencies
RUN \
  apk add $CLOUD_SDK_APK_DEPS $APK_DEPS && \
  pip install -U $CLOUD_SDK_PIP_DEPS

# Downloading gcloud package]
# RUN curl https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-$CLOUD_SDK_VERSION-linux-$(arch).tar.gz > /tmp/google-cloud-sdk.tar.gz

# Installing the package
RUN \
  mkdir -p /usr/local/gcloud \
  && tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz \
  && /usr/local/gcloud/google-cloud-sdk/install.sh

FROM base

RUN \
  apk add $APK_DEPS

COPY --from=build /usr/local/gcloud /usr/local/gcloud

# Adding the package path to local
ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin

# gcloud config
RUN \
  gcloud config set core/disable_usage_reporting true && \
  gcloud config set component_manager/disable_update_check true && \
  gcloud config set metrics/environment github_docker_image

# Remove gcloud package file
RUN rm /tmp/google-cloud-sdk.tar.gz

# Setup a volume for configuration and auth data
VOLUME ["/root/.config"]
