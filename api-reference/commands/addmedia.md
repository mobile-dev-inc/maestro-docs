---
description: >-
  Add PNG, JPEG, GIF, or MP4 media to device gallery in Maestro tests. Part of
  Maestro testing tutorial.
---

# addMedia

Allows you to add media to the device's gallery for both Android and iOS, making them accessible for use in your application flow.

```yaml
- addMedia:
    - "./assets/foo.png" # path of media file in workspace
    - "./assets/foo.mp4"
```

Currently, maestro supports the following mime types for this command:

* PNG
* JPEG
* JPG
* GIF
*   MP4



