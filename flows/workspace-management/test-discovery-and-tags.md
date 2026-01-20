# Test discovery and tags

As your test suite grows from a few files to hundreds of Flows, managing which tests to run and where they are located becomes critical. Maestro uses a combination of Inclusion patterns and metadata tagging to give you precise control over your execution.

### Test discovery via patterns

By default, when you point the Maestro CLI at a folder, it only executes Flow files located at the top level of that directory. It ignores subfolders to prevent accidental execution of nested or utility Flows.

To change this behavior and organize your repository into subdirectories (like `/auth`, `/checkout`, or `/journeys`), you must define Inclusion Patterns in your `config.yaml`.

The `flows` key uses glob syntax to define which files should be included in a test suite run.

```yaml
# config.yaml
appId: com.example.app
flows:
  - "*"            # Default: Includes all Flows in the root folder only
  - "auth/*"       # Includes all Flows in the auth subfolder
  - "tests/**"     # Recursive: Includes all Flows in tests and its subfolders
```

### Filter test via tags

Tags allow you to categorize your Flows based on their purpose, priority, or execution environment without changing your folder structure.

To add tags to a Flow, you need to define them  in the configuration block at the top of your individual Flow files:

```yaml
# flows/login_smoke.yaml
appId: com.example.app
tags:
  - smoke
  - registration
---
- launchApp
# ... rest of the flow
```

When running your tests using the [Maestro CLI](https://app.gitbook.com/s/kq23kwiAeAnHkGJYMGDk/), you can use the `--include-tags` or `--exclude-tags` flags to filter the execution on the fly. Consider the example above, you can:

* **Include**: `maestro test . --include-tags=smoke` (Runs only smoke tests).
* **Exclude**: `maestro test . --exclude-tags=wip` (Runs everything _except_ work-in-progress tests).

### Global tag configuration

While individual tags in a Flow file categorize what a test is, defining tags in your `config.yaml` sets the policy for your entire workspace. It acts as a permanent security gate, ensuring that specific types of tests are always included or ignored without you having to remember complex CLI flags every time.

```yaml
# config.yaml
includeTags:
  - production_ready
excludeTags:
  - experimental
  - flaky
```

You can use global tags to:

* **Target environment**: You can create different config files for different environments. For example, a `staging-config.yaml` might globally include tags for internal-only features that shouldn't run in production.
* Enforce quality gates: If you have 10 tests that are currently "flaky" due to a known environment bug, you don't want to delete them. By tagging them as `flaky` in the Flow and adding `excludeTags: [flaky]` to your `config.yaml`, you ensure no one on the team accidentally runs them and breaks the build.

{% hint style="info" %}
CLI flags will always take precedence over global settings in the `config.yaml`.
{% endhint %}

#### Example

Imagine a repository structured by feature:

```
.
├── config.yaml
├── auth/
│   ├── login.yaml (tags: [smoke])
│   └── signup.yaml
└── payments/
    ├── credit_card.yaml (tags: [smoke])
    └── paypal.yaml
```

To run your `smoke` suite across all features, your `config.yaml` should look like this:

```yaml
# config.yaml
appId: com.example.app
flows:
  - "**"          # Look everywhere
includeTags:
  - smoke         # But only run the smoke tests
```

### Next Steps

Now that you've discovered your tests, learn how to manage their Sequential Execution.
