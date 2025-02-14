# Device timezones

Android emulator instances and macOS instances (iOS flows are executed on iOS simulators) are located in following regions and timezones.

| Device type | Region\*\*                                                                 | Timezone |
| ----------- | -------------------------------------------------------------------------- | -------- |
| Android     | us-west1-a ([gcloud](https://cloud.google.com/compute/docs/regions-zones)) | UTC      |
| iOS         | vegas                                                                      | GMT -7   |

\*\* In here region represents a physical location of an emulated (linux instance with hosted Android emulator) / simulated (macOS instance with iOS simulator) environment. Device has an ability to override some of those settings, i.e. timezone of an Android emulator is UTC by default.
