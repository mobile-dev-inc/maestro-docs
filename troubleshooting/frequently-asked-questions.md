# Frequently asked questions

### How can I use the same flow when my apps have different app IDs?

If you want to run the same flow for apps with different app IDs, you can use an [external parameter](../advanced/parameters-and-constants) for `appId`.
Pass the parameter `APP_ID` to Maestro:

```
maestro test -e APP_ID=your.app.id file.yaml
```

And then refer to it in your flow using `${APP_ID}`:

```yaml
appId: ${APP_ID}
---
- launchApp
```
