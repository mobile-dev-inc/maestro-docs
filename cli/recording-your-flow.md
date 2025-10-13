---
description: >-
  Record a Flow as an MP4 with Maestro CLI. Share runs for debugging or demos,
  using local or remote rendering with secure temporary links.
---

# Record Your Flow

<figure><img src="../.gitbook/assets/maestro-record-cover.png" alt=""><figcaption></figcaption></figure>

It's often useful to record a video of your Flow. Some reasons you might want to do this:

* Showcase a Maestro Flow to your team
* Share a Maestro Flow on social media
* Demonstrate some behavior of your Flow (eg. for debugging purposes)

Maestro makes this easy to do without needing to clean up your desktop, arrange your windows, or deal with screen recording software.

Simply run the command below to render a beautiful MP4 video of your Flow in action:

```bash
maestro record YourFlow.yaml
```

Here's an example of the final output:

{% embed url="https://player.vimeo.com/video/775621555?h=736930f7f9" %}

## FAQ

### How does this work?

The `maestro record` command captures the raw Flow output and app screen recording, and then programmatically stitches them together into an mp4 file.

Rendering is possible

1. **Remotely** on mobile.dev servers so the command sends the screen recording and Flow output securely over the internet to our API.
2.  **Locally** so the command uses Skiko to create the screen recording and Flow output video without contacting the mobile.dev servers.

    To do this, you need to pass `--local` flag right after `record` command to `maestro`, like shown below:

    ```sh
    maestro record --local YourFlow.yaml
    ```

### When using Remote rendering option

**Are video URLs private?**

Yes - `maestro record` generates [a signed url](https://cloud.google.com/storage/docs/access-control/signed-urls) that is valid for 60 minutes. This means that no one can guess your video url and you are the only one who can download your video (unless you share the signed url). After 60 minutes, the url will be invalidated.

**How long are videos stored?**

Videos are deleted from our servers after 24 hours.

### What is the maximum duration for a Flow recording?

The maximum duration is two minutes.
