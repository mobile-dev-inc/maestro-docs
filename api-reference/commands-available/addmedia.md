---
description: Add images or videos to the device gallery for media picker testing.
---

# addMedia

The `addMedia` command adds one or more media files from your workspace to the device's gallery on both Android and iOS. This makes the files accessible to your application during a test flow.

The command accepts a list of strings, where each string is the relative path to a media file in your workspace.

### Usage examples

The following example adds a PNG image and an MP4 video to the device's gallery.

```yaml
- addMedia:
    - "./assets/foo.png"
    - "./assets/foo.mp4"
```

### Supported formats

This command supports the following file formats:

* `PNG`
* `JPEG`
* `JPG`
* `GIF`
* `MP4`
