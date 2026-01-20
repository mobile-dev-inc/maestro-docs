# Tags

You can add tags to your Flows files to later filter them in `maestro cloud` and `maestro test` commands. There is a couple of different use cases for this, but this is especially useful when you want to run some Flows at Pull Request time, and other Flows before a version release, for example.

### Adding Tags

You can provide a list of tags in the `tags` field at the root of your Flow file. Like this:

```
appId: com.example.App
tags:
  - nightly-build
  - pull-request
---
- launchApp
```

### Filtering

In `maestro cloud` and `maestro test` commands, you can specify either `--include-tags` or `--exclude-tags` parameters to filter them.

The `--include-tags` will look for all flows containing the provided tag; it doesn't matter if those Flows also have other tags. On the other hand, the `--exclude-tags` parameter will remove from the list of Flows run any Flow that contains the provided tags. These options can be used together and they perform an `AND` operation.

**Example**

Let's say a user has two flows:

```
# flowA.yaml
appId: com.example.app
tags: 
  - dev
  - pull-request
```

```
# flowB.yaml
appId: com.example.app
tags: 
  - dev
```

In the scenario above:

* If they use `--include-tags=dev` , flowA and flowB will run.
* If they use `--include-tags=dev,pull-request` , both flows will run.
* If they use `--exclude-tags=pull-request` , only flowB will run.
* If they use `--exclude-tags=dev` none Flow will run.
* If they use `--include-tags=dev --exclude-tags=pull-request` , only flowB will run.

### Global tags

Instead of passing tags with each `test` or `cloud` command, you can also define default tags to be applied to each run. To do so, add the following to your `config.yaml` file (or create it if it is missing):

```yaml
includeTags:
  - tagNameToInclude
excludeTags:
  - tagNameToExclude
```

Now, whenever you run a test folder the following will happen:

* Only flows with a `tagNameToInclude` are going to run
* Flows with a `tagNameToExclude` are not going to run (even if they have `tagNameToInclude` assigned to them)

When used in combination with `--include-tags` and `--exclude-tags`, global tags behaving as a _union_ and will not be overwritten. Consider the following example:

```
maestro test --include-tags=tagA --exclude-tags=tagB workspaceFolder/
```

The following behaviour should be expected:

* Only flows that have _both_ `tagA` **and** `tagNameToInclude` are going to run
* Flows that have _either_ `tagB` _**or**_ `tagNameToExclude` are not going to run (regardless of whether they have both `tagA` and `tagNameToInclude`)
