# Arrange your repository for Maestro tests

Lots of teams choose to keep their Maestro tests alongside the code for their application. That way, a build from a few months back that now needs a patch also has the correct version of the tests sat with them, and a new feature branch that changes how login works can have the changes to the test flows developed right alongside.

But what's a good way to lay this out?

Boring tester answer: it depends :smile:



### Journeys

If you arrange your tests as journeys through your application, then you likely want some top-level folder to contain them, and only start organising them into deeper subfolders once they become unwieldy. Maybe you end up with something like this:

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

Which later spreads into something deeper, once you decide to start splitting. Here, I've broken this up between flows centered around new and existing users, and an extra folder to contain utility scripts that might be shared.&#x20;

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

_In this example, the instructions in_ [_Controlling What Tests to Include_](../../cli/test-suites-and-reports.md#controlling-what-tests-to-include) _have been used to set inclusion patterns in the config.yaml to include everything below the 'tests' folder._

### Features

For testing approaches that are centered on validating the behaviours of individual features or requirements, you might choose to mirror the source structure, so that the tests are easy to find and maintain:

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
