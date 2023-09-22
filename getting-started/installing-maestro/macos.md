# macOS

Dependencies:

* [Xcode](https://developer.apple.com/xcode/) (recommended version is 14 or higher)\
  \
  Please make sure that Command Line Tools are installed (Xcode -> Preferences -> Locations -> Command Line Tools)

## Note

Xcode 15 is currently not supported due to a bug with setting permissions, `launchApp` command will most probably fail with exception `Unable to clear state for app xxx.xxx`, we're working to fix it asap, meanwhile following workarounds can be done to be able to test with maestro:

* downgrading maestro to 1.32.0 via `export MAESTRO_VERSION=1.32.0; curl -Ls "https://get.maestro.mobile.dev" | bash`
* downloading and installing Xcode 14:\
  1\. download the .xip from [Apple developer website](https://developer.apple.com/download/all/?q=xcode)\
  2\. open the .xip file and move it to Applications folder\
  3\. change command line tools to Xcode 14 SDK via `sudo xcode-select -s </path/to/your/Xcode_14.app>`

Follow the default install instructions

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}
