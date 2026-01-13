# Repository configuration

Many teams adopt a monorepo approach, co-locating Maestro test suites with app source code. This strategy offers several technical advantages:

* **Version synchronization**: Tests remain coupled to the codebase version they validate, ensuring historical commits maintain test compatibility
* **Atomic changes**: Feature branches can bundle app logic modifications with corresponding test updates in a single pull request
* **Simplified CI/CD**: Build pipelines can reference tests directly from the same repository checkout without managing separate test artifact versions

## Repository structure patterns

The optimal directory layout depends on your testing strategy and organizational requirements. Consider the following approaches:

### Journeys

Journey-based test organization models end-to-end user workflows as sequential test scenarios. This approach typically begins with a flat directory structure containing workflow definitions, which you can refactor into a hierarchical taxonomy as test coverage scales:

```
├── flows
│   ├── config.yaml
│   ├── login.yaml
│   ├── register.yaml
│   └── shopping.yaml
└── src
    └── app
        └── <code here>
```

As test coverage expands, you can refactor the flat structure into a hierarchical taxonomy that partitions test suites by user segmentation and execution context. The example below demonstrates a modular architecture that separates test scenarios by user lifecycle state, with shared utilities extracted for reusability:

```
├── flows
│   ├── config.yaml
│   ├── tests
│   │   ├── new_users
│   │   │   ├── register.yaml
│   │   │   └── shopping_first_time_discount.yaml
│   │   └── existing_users
│   │       ├── account_settings.yaml
│   │       ├── deeplink_from_email.yaml
│   │       ├── deeplink_from_notification.yaml
│   │       ├── login.yaml
│   │       ├── shopping.yaml
│   │       └── shopping_bulk_buy_discount.yaml
│   └── utils
│       └── set_discount_code.js
└── src
    └── app
        └── <code here>
```

{% hint style="success" %}
#### **Technical implementation note**

To organize your project into a hierarchical structure, you must define the search path in your `config.yaml` using the `flows` key. For example, setting `flows: tests/**` tells Maestro to discover all Flow files within that specific subdirectory using glob syntax. This provides granular control over which tests are executed during local runs or CI/CD pipelines.
{% endhint %}

### Features

Feature-based test organization establishes a structural isomorphism between test suites and app modules, enabling direct traceability between functional requirements and their validation logic. This architectural pattern optimizes for maintainability by collocating tests with their corresponding source code boundaries:

```
├── flows
│   ├── config.yaml
│   ├── account
│   │   └── set_display_name.yaml
│   ├── auth
│   │   ├── login.yaml
│   │   ├── login_invalid.yaml
│   │   └── login_locked_account.yaml
│   ├── basket
│   │   ├── add_to_cart.yaml
│   │   └── update_cart.yaml
│   └── checkout
│       ├── complete_purchase.yaml
│       └── save_for_later.yaml
└── src
    └── app
        ├── account
        │   └── <code here>
        ├── auth
        │   └── <code here>
        ├── basket
        │   └── <code here>
        └── checkout
            └── <code here>
```
