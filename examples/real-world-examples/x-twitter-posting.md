Automate the X (Twitter) Android app to create and publish a new post using Maestro commands.
---

# Automate X (Twitter) Post Creation Flow

Testing social media integrations or validating user-generated content flows often requires creating posts programmatically. This recipe demonstrates how to automate the X (formerly Twitter) Android app to compose and publish a new post using Maestro.

This Flow is useful for:
- validating social sharing features
- testing deep links that open the composer
- automating repetitive posting scenarios in QA environments

---

### The Workflow

Since this Flow interacts with a third-party system app, it focuses on navigating dynamic UI elements and ensuring the post composer opens reliably before inputting text.

1. Launch the X Android app with a clean session.
2. Tap the **New post** floating action button.
3. Focus the text input field.
4. Enter the post content.
5. Publish the post using the **POST** button.

---

## 1. X Post Flow

Create a YAML file in your Maestro tests directory, for example:

```yaml
# twitter_post.yaml
appId: com.twitter.android
---
- launchApp:
    clearState: true

# Open post composer
- tapOn: New post
- tapOn: New post

# Focus the text field
- tapOn: What’s happening?

# Enter post content
- inputText: Hello World

# Publish the post
- tapOn: POST
````

---

### Why this Flow is structured this way

* **`clearState: true`** ensures that each test run starts from a consistent session. This avoids failures caused by being on a different screen or logged-in state from a previous run.
* The **double `tapOn: New post`** is used because some versions of the X app require two taps to reliably open the composer (one for the FAB animation and one for the actual action).
* Using the accessibility label **“What’s happening?”** is more stable than relying on view IDs, which frequently change in third-party apps.
* Keeping the post text simple (`Hello World`) makes it easy to validate success in downstream assertions if needed.

---

## 2. Running the Flow

Once the Maestro CLI is installed and an Android emulator or device is running, execute the Flow using:

```bash
maestro test twitter_post.yaml
```

This will automatically:

1. Launch X
2. Open the composer
3. Create a post
4. Publish it to the timeline

---

## Related content

Explore Maestro documentation for additional automation patterns:

* inputText – Learn how to send text into input fields.
* launchApp – Understand options like `clearState` and package targeting.
* runFlow – Reuse smaller flows inside complex test scenarios.

