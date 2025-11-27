---
description: Configuring the Maestro Cloud Bitrise Step in your Bitrise pipeline
---

# Bitrise

{% hint style="info" %}
🚀 **Cloud Plan** required - get started for free at [**maestro.dev**](https://signin.maestro.dev/sign-up)
{% endhint %}

Testing in Maestro Cloud is possible with all CI systems but provides native integrations with a number of common providers, including Bitrise. You can start running your Flows in CI with just a few clicks using the Maestro Cloud Bitrise Step.

### Setting up Bitrise

1. Make sure you have your API key & Project ID. Both of these can be found in your [Maestro Cloud Console](https://app.maestro.dev/). The API Key is an option on the left. Project IDs can be found in Settings, then clicking on the individual project on the left.
2. Go to your Bitrise account and save your API key into a secret variable, e.g. `CLOUD_API_KEY` (any variable prefixed with `MAESTRO_` will be [added as environment variable](../../advanced/parameters-and-constants.md) for your run - this might not be desirable for an authentication key!)
3. Open the Workflow Editor and select your desired workflow
   1. To add the Maestro step, you can search for "Maestro" in Bitrise's library of steps.
   2.  The step should be added after your app binary has been built.<br>

       <figure><img src="../../.gitbook/assets/Screenshot 2025-11-27 at 15.38.37.png" alt="Screenshot of the configuration of the Maestro Cloud step on Bitrise.io"><figcaption></figcaption></figure>
4. Lastly, fill out the following information in the step configuration:
   1. API Key (as your secret variable from earlier, e.g. `$CLOUD_API_KEY`
   2. Project ID
   3. Path to your built binary
5. Check the Flow Workspace matches your repo's directory structure
6. That's it! You should now be able to run Maestro tests in the cloud via Bitrise.
