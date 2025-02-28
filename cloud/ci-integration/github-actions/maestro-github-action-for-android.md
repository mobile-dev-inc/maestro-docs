# Maestro GitHub Action for Android

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://www.maestro.dev/)
{% endhint %}

```
name: Build and run Maestro tests (Native Android)

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  maestro-cloud:
    runs-on: ubuntu-latest
    outputs:
      app: app/build/outputs/apk/debug
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v3
        with:
          java-version: 11
          distribution: 'temurin'
      - run: ./gradlew assembleDebug
      - uses: mobile-dev-inc/action-maestro-cloud@v1
        with:
          api-key: ${{ secrets.MAESTRO_API_KEY }}
          # note that you can supply the project id any way you like, it is not secret
          project-id: ${{ secrets.MAESTRO_PROJECT_ID }}
          app-file: app/build/outputs/apk/debug/app-debug.apk
```
