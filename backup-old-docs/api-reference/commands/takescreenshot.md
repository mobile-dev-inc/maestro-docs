# takeScreenshot

`takeScreenshot` saves a screenshot as a PNG file in the Maestro workspace.

```yaml
- takeScreenshot:
    path: LoginScreen # screenshot will be stored as LoginScreen.png
```

It can also be written in the short form:

```yaml
- takeScreenshot: MainScreen # screenshot will be stored as MainScreen.png
```

### Path

Screenshots are saved to a `.maestro` folder inside your workspace by default. You can override that location by using the `--test-output-dir` flag when running `maestro test`. For more details, see [Test Output Directory](../../cli/test-output-directory.md).

The path is relative to the Maestro workspace directory, not to the flow file.
