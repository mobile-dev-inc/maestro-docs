---
hidden: true
---

# Repository configuration

Many teams adopt a monorepo approach, co-locating Maestro test suites with app source code. This strategy offers several technical advantages:

* **Version synchronization**: Tests remain coupled to the codebase version they validate, ensuring historical commits maintain test compatibility
* **Atomic changes**: Feature branches can bundle app logic modifications with corresponding test updates in a single pull request
* **Simplified CI/CD**: Build pipelines can reference tests directly from the same repository checkout without managing separate test artifact versions

### Repository structure patterns

A well-structured repository ensures that your test suite remains maintainable as your application grows. Most Maestro projects are organized around one of two core strategies:&#x20;

| **Strategy**  | **Primary objective** | **Best for**      |
| ------------- | --------------------- | ----------------- |
| User journeys | Funnel completion     | Goal-driven apps  |
| Feature tests | Friction reduction    | Habit-driven apps |

Choosing the right structure helps ensure your automation remains relevant as your app grows.

#### User journeys (Goal-driven Apps)

This approach is best for E-commerce, food delivery, or fintech (e.g., DoorDash, Uber, Banking) apps. These apps exist to help users complete a specific task. When a user is hungry, they open the app to order food,  once they are fed, they stop using it.

* **The Goal**: Success is defined by the user reaching the end of a funnel (e.g., Order Confirmed).
* **The Strategy**: Organize your repository by journeys. Focus on end-to-end flows that track variations of the main task (e.g., Delivery vs. Collection, applying coupons, or external payment processors).

This pattern often partitions test suites by user segmentation (new vs. existing) and execution context.

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
#### Technical implementation note

To organize your project into a hierarchical structure, you must define the search path in your `config.yaml` using the `flows` key. For example, setting `flows: tests/**` tells Maestro to discover all Flow files within that specific subdirectory using glob syntax. This provides granular control over which tests are executed during local runs or CI/CD pipelines.
{% endhint %}

#### Feature tests (Habit-driven Apps)

This approach is best for social media, content aggregators, or entertainment (e.g., Reddit, Instagram, Spotify) Apps. These apps succeed when they reduce friction and keep users engaged. Success is a cumulative experience of many small, slick interactions.

* **The Goal**: Success is defined by high engagement and zero friction.
* **The Strategy**: Organize your repository by individual features. You need deep coverage for components because one slow spinner or broken interaction can cause a user to drop off.

Feature-based organization establishes a structural isomorphism (direct mapping) between test suites and app modules:

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
