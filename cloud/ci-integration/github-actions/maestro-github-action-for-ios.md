# Maestro GitHub Action for iOS

```
name: Build and upload to Robin (Native iOS)

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
          project-id: ${{ secrets.ROBIN_PROJECT_ID }}
          app-file: build/MyApp.app
```
