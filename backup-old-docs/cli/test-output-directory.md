# Test Output Directory

Maestro stores test artifacts such as screenshots, logs, and AI reports during test execution. You can configure where these artifacts are stored using either command-line options or workspace configuration.

## Command Line Option

Use the `--test-output-dir` option to specify the output directory for a specific test run:

```bash
maestro test workspace --test-output-dir=test_output_directory
```

{% hint style="info" %}
The path specified in `--test-output-dir` is relative to the Maestro workspace directory, not to the individual flow file.
{% endhint %}

## Workspace Configuration

Add the `testOutputDir` field to your `config.yaml` file for persistent configuration:

```yaml
# .maestro/config.yaml
testOutputDir: test_output_directory
```

{% hint style="info" %}
The path specified in `testOutputDir` is relative to the Maestro workspace directory, not to the individual flow file.
{% endhint %}

## Default Behavior

If no custom directory is specified, Maestro stores test artifacts in:

```
~/.maestro/tests/<datetime>/
```

## Priority Order

Configuration is applied in the following priority order:

1. **Command line flag** (`--test-output-dir`)
2. **Workspace configuration** (`testOutputDir` in `config.yaml`)
3. **Default behavior** (`~/.maestro/tests/<datetime>/`)

## What Gets Stored

The configured directory will contain:

- Screenshots taken on test failures
- `maestro.log` files with Maestro-related logs
- `commands-*.json` files with command metadata
- AI analysis reports (when using `--analyze`)

{% hint style="info" %}
The directory will be created automatically if it doesn't exist.
{% endhint %}
