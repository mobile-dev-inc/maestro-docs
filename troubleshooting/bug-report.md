# Bug Report

### How to report an issue

If an issue / bug encountered while using **maestro**, we encourage you to report it in either our public [maestro slack channel](https://mobile-dev-inc.slack.com/ssb/redirect) or [create a github issue](https://github.com/mobile-dev-inc/maestro/issues/new) (please make sure that one doesn't already exist).

### bugreport command

To provide more context if something hasn't worked as expected with **maestro** there is a command:

```
maestro bugreport
```

This command collects some data about maestro usage locally on a user's machine. This data includes maestro process logs, system info (maestro version, OS version, device CPU architecture) and idb-companion logs (only for iOS).

When creating a new issue / bug report in one of our channels please attach the .zip files generated in the folder specified after running `maestro bugreport` command.
