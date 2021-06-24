# gfw-pipeline

Docker image with all the components needed for build a GFW pipeline

## Repositories
The GFW-pipeline Docker Image is hosted on [Container Registry](https://gcr.io/world-fishing-827/gfw-pipeline).

The full repository name for Container Registry is `gcr.io/world-fishing-827/github.com/globalfishingwatch/gfw-pipeline:latest`.

## Supported tags

* `:latest`: Has the current python version (3.7) that are using all the pipeline steps.
* `:latest-python3.7`: Has the current python version (3.7) that are using all the pipeline steps.
* `:latest-python3.8`: Has the new python version (3.8) that are using the pipeline steps that requires python3.8.
All these version has the last Google SDK version and are being generated weekly.

## Usage

To use this image, pull from [Container Registry](https://gcr.io/google.com/cloudsdktool/cloud-sdk) and then run the following command:

```
docker pull gcr.io/world-fishing-827/gfw-pipeline:latest
```
