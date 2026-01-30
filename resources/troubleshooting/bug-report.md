# Bug report

This page explains how to report a bug in Maestro and how to attach context so the team can triage your issue quickly. Use it when you hit a problem that is not covered in Known issues.

***

### How to report an issue

If you encounter an issue or bug while using Maestro, report it by opening a GitHub issue.

1. Go to [Create a GitHub issue](https://github.com/mobile-dev-inc/maestro/issues/new/choose).
2. Choose the issue type that best matches your report.
3. Follow the instructions in the issue template. Filling out the template helps the team triage your report faster.

***

### Collecting context with `maestro bugreport`

To give the Maestro team more context about your environment, run the `bugreport` subcommand before creating the issue. It collects data from your machine and writes it to a folder; you then attach the generated `.zip` files to your GitHub issue.

#### What the command does

Run in a terminal:

```bash
maestro bugreport
```

The command collects data about Maestro usage on your machine. The data includes:

* Maestro process logs
* System info (Maestro version, OS version, device CPU architecture)

After the command finishes, it prints the path to the folder where the data was written.

#### Attach the output to your issue

When you create a new issue or bug report, attach the `.zip` files generated in that folder. This helps the team reproduce and diagnose the problem.

***

### Related content

* [Known issues](known-issues.md): Known limitations and workarounds.
* [FAQ](faq.md): Common questions and answers.
