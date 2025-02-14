# Configuring device locale

`maestro cloud` supports testing different app locales by changing a device locale for a given upload automatically by setting `--device-locale` parameter. The parameter `--device-locale` is a combination of [`ISO-639-1`](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) `+` [`ISO-3166-1`](https://en.wikipedia.org/wiki/ISO_3166-1) with using underscore `_` symbol in between them. If the parameter is omitted default `en_US` locale will be used. Here are some example usages:

```
// sets device locale to German(Germany)
maestro cloud --device-locale de_DE <app_file_path> <workspace_path>
// sets device locale to Japanese(Japan)
maestro cloud --device-locale ja_JP <app_file_path> <workspace_path>
```

Full list of supported locales can be found [here](../../advanced/testing-in-different-locales.md).
