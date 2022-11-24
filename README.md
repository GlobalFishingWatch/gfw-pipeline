# gfw-pipeline

Docker image with all the components needed for build a GFW pipeline

## Repositories
The GFW-pipeline Docker Image is hosted on [Container Registry](https://gcr.io/world-fishing-827/gfw-pipeline).

The full repository name for Container Registry is `gcr.io/world-fishing-827/github.com/globalfishingwatch/gfw-pipeline:latest`.

## Supported tags

* `:latest`: Has the current python version (3.7) that are using all the pipeline steps.
* `:latest-python3.7`: Has the current python version (3.7) that are using all the pipeline steps.
* `:latest-python3.8`: Has the new python version (3.8) that are using the pipeline steps that requires python3.8.
* `:latest-python3.9`: Has the new python version (3.9) that are using the pipeline steps that requires python3.9.
* `:latest-python3.10`: Has the new python version (3.10) that are using the pipeline steps that requires python3.10.
* `:latest-python3.11`: Has the new python version (3.11) that are using the pipeline steps that requires python3.11.
All these version has the last Google SDK version and are being generated weekly.

## Usage

To use one of the images, pull from [Container Registry](https://gcr.io/google.com/cloudsdktool/cloud-sdk) and then run the following command:
Ex using the latest image.

```
docker pull gcr.io/world-fishing-827/github.com/globalfishingwatch/gfw-pipeline:latest
```

To indicate in other Dockerfile use it:
```
FROM gcr.io/world-fishing-827/github.com/globalfishingwatch/gfw-pipeline:latest

```
## Maintenance

If you want to upgrade the Google SDK version that is using this image, you could do it replacing the subsitution in the `cloudbuild.yaml`

```
substitutions:
  _CLOUD_SDK_VERSION=<VERSION_UPGRATED>
```
