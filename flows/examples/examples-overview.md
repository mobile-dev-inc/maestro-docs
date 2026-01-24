# Examples overview

This section of the documentation is a curated library of real-world scenarios designed to bridge the gap between basic commands and complex, production-ready automation.

While the core documentation explains how commands work, this section focuses on implementation patterns, solving specific technical hurdles like system-level interactions, dynamic content, and scalable architecture.

### Implementation Recipes

These guides provide targeted solutions for specific technical requirements:

* [android-contacts-flow-automation-with-maestro.md](android-contacts-flow-automation-with-maestro.md "mention"): A perfect starting point to see how Maestro interacts with native Android system apps using text and ID selectors.
* [choose-images-from-the-gallery.md](choose-images-from-the-gallery.md "mention"): Learn the specific sequence needed to navigate out of your app, interact with the system photo picker, and return to your Flow.
* [check-the-clipboard-content.md](check-the-clipboard-content.md "mention"): See how to verify that your app correctly copied text or links to the device clipboard using JavaScript assertions.
* [download-and-open-a-file.md](download-and-open-a-file.md "mention"): A guide on handling "Save to Device" flows and verifying that files (like PDFs or images) are accessible.
* [custom-scrolling-for-screen-fragments.md](custom-scrolling-for-screen-fragments.md "mention"): Master scrolling in complex layouts where elements are hidden inside sub-containers or fragments.
* [get-the-last-matching-element.md](get-the-last-matching-element.md "mention"): Learn how to target a specific instance of an element when multiple identical items (like "Delete" buttons) appear in a list.

#### Full-flow blueprints

See how Maestro handles real-world complexity in popular applications.

* [Facebook Signup Flow](facebook-signup-flow-automation-with-maestro.md): Covers complex form filling, handling multiple screens, and navigating onboarding.
* [Wikipedia on Android](https://www.google.com/search?q=wikipedia-on-android-with-maestro): Demonstrates deep navigation, search interactions, and content verification.

#### Enterprise Design Patterns

For teams building large-scale test suites, these architectural guides are essential.

* [Page Object Model (POM) with Maestro](page-object-model-with-maestro.md): Learn how to separate your element selectors from your test logic. This is the industry-standard approach for reducing maintenance and making tests readable for the whole team.

