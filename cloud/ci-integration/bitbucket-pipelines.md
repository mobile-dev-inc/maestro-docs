# Bitbucket Pipelines

## Setup

In order to use the Maestro Cloud Pipe to upload to Robin, you'll need to add the API key and project IDs as secret environment variables in your Bitbucket repository.

1. Go to your Repository -> Repository settings -> Repository Variables
2. Save your API Key and project id as a secured env variables

## Commit your Maestro Flows to your repository

Create a `.maestro/` directory at the root of your repository and commit your Flows there:

```
<root>
├── .maestro/
│   ├── Login.yaml
│   ├── Add to Cart.yaml
│   └── Search.yaml
```

It’s common to have some Flow files that are only meant to be executed as part of another Flow via the `runFlow` command. These "subflows" can be nested under a subdirectory to prevent them from running as a top-level Flow.

```
<root>
├── .maestro/
│   ├── subflows/
│   │   └── MySubflow.yaml
│   ├── Login.yaml
│   ├── Add to Cart.yaml
│   └── Search.yaml
```



## Add Maestro Cloud Pipe

Once everything is setup, you can integrate the [Maestro Cloud Upload Pipe](https://bitbucket.org/product/features/pipelines/integrations?search=maestro\&p=mobiledevinc/maestro-cloud-upload) in your Pipeline build process.&#x20;

Edit your `bitbucket-pipelines.yml` and add an extra step after your app has finished building.

_Note: All file paths are relative to the repository source root._

### Android

```yaml
script:
  - pipe: mobiledevinc/maestro-cloud-upload:1.0.0
    variables:
      MDEV_API_KEY: $MDEV_API_KEY
      MDEV_PROJECT_ID: $MDEV_PROJECT_ID
      MDEV_APP_FILE: app/build/outputs/apk/debug/app-debug.apk
```

### iOS

```yaml
script:
  - pipe: mobiledevinc/maestro-cloud-upload:1.0.0
    variables:
      MDEV_API_KEY: $MDEV_API_KEY
      MDEV_PROJECT_ID: $MDEV_PROJECT_ID
      MDEV_APP_FILE: <app_name>.app
```



The pipe will:

* Upload your app and flows to Maestro Cloud
* Wait for flows to complete (can be configured)
* Complete with fail/pass depending on flow results

## That's it!

For more information and configurations, checkout [Maestro Cloud Upload Pipe](https://bitbucket.org/product/features/pipelines/integrations?search=maestro\&p=mobiledevinc/maestro-cloud-upload).
