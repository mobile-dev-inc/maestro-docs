# Maestro GitHub Action for iOS

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://www.maestro.dev/)
{% endhint %}

## Full Example

```
name: Build and run Maestro tests (Native iOS)

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: macOS-latest
    steps:
      - uses: actions/checkout@v2
      - run: xcodebuild build -scheme 'MyApp' -configuration Debug -project 'MyApp.xcodeproj' -destination 'generic/platform=iOS Simulator' CONFIGURATION_BUILD_DIR=$PWD/build
      - uses: mobile-dev-inc/action-maestro-cloud@v1
        with:
          api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
          # note that you can supply the project id any way you like, it is not secret
          project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
          app-file: build/MyApp.app
```


`app-file` should point to an .app build (x86 or ARM), either directly to the file or a glob pattern matching the file name. When using a pattern, the first matched file will be used.

### .dSYM file

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: <app_name>.app
    mapping-file: <app_name>.app.dSYM
```

`mapping-file` should point to generated .dSYM file (unique per build). more info [here](https://developer.apple.com/documentation/xcode/building-your-app-to-include-debugging-information).


## Specifying iOS version and device

You can specify which iOS Version to use when running in Maestro Cloud using the `device-os` parameter.

On Maestro Cloud, the default iOS version is 16. [Refer to Maestro Cloud docs](https://docs.maestro.dev/cloud/reference/configuring-os-version) for available iOS simulator versions. On Maestro Cloud, the default iOS version is 16.

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: app.zip
    device-model: iPhone-16
    device-os: iOS-18-2
```