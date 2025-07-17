# Maestro GitHub Action for Android

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://signin.maestro.dev/sign-up)
{% endhint %}

## Full Example

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

`app-file` should point to an x86 compatible APK file, either directly to the file or a glob pattern matching the file name. When using a pattern, the first matched file will be used.

### ProGuard Deobfuscation

Include the ProGuard mapping file to deobfuscate Android performance traces:

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: app/build/outputs/apk/release/app-release.apk
    mapping-file: app/build/outputs/mapping/release/mapping.txt
```

## Specifying Android API Level

You can specify which Android API level to use when running using the `android-api-level` parameter.

On Maestro Cloud, the default API level is 33 (Android 13). [Refer to Maestro Cloud docs](https://docs.maestro.dev/cloud/reference/configuring-os-version) for available Android emulator API levels.

```yaml
- uses: mobile-dev-inc/action-maestro-cloud@v1.9.8
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: 'proj_01example0example1example2'
    app-file: app.apk
    android-api-level: 29
```
