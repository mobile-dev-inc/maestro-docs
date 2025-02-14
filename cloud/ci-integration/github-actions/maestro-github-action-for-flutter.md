# Maestro GitHub Action for Flutter

## Android

```yaml
name: Build and upload to Robin (Flutter Android)

on:
  workflow_dispatch:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  upload:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
        with:
          channel: "stable"
      - run: flutter build apk --debug
      - uses: mobile-dev-inc/action-maestro-cloud@v1
        with:
          api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
          # note that you can supply the project id any way you like, it is not secret
          project-id: ${{ secrets.ROBIN_PROJECT_ID }}
          app-file: build/app/outputs/flutter-apk/app-debug.apk
```

## iOS

```yaml
name: Build and upload to Robin (Flutter iOS)

on:
  workflow_dispatch:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  ios:
    runs-on: macos-13
    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
        with:
          channel: "stable"
      - run: flutter build ios --debug --simulator
      - uses: mobile-dev-inc/action-maestro-cloud@v1
        with:
          api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
          # note that you can supply the project id any way you like, it is not secret
          project-id: ${{ secrets.ROBIN_PROJECT_ID }}
          app-file: build/ios/iphonesimulator/Runner.app # replace `Runner` with your app name
```
