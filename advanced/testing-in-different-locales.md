---
description: >-
  Create devices with specific locales using maestro start-device
  --device-locale for localized testing.
---

# Test in different locales

It is possible to use `maestro start-device` command to create a new device with a custom locale. This functionality enables an option to write and test Maestro flows for different languages. The parameter `--device-locale` is a combination of [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) + [ISO-3166-1](https://en.wikipedia.org/wiki/ISO_3166-1), separated by an underscore `_` symbol in between them.

Let's see some examples:

{% code title="Create a new iOS simulator with locale set to Italy (Italian)" %}
```console
maestro start-device \
  --platform ios \
  --device-locale it_IT
```
{% endcode %}

{% code title="Create a new Android emulator with locale set to France (French)" %}
```console
maestro start-device \
  --platform android \
  --device-locale fr_FR
```
{% endcode %}

Below you can find a full list of supported device locales per platform.

### Supported device locales on Android

| Language code | Language name    |
| ------------- | ---------------- |
| ar            | Arabic           |
| bg            | Bulgarian        |
| ca            | Catalan          |
| zh            | Chinese          |
| hr            | Croatian         |
| cs            | Czech            |
| da            | Danish           |
| nl            | Dutch            |
| en            | English          |
| fi            | Finnish          |
| fr            | French           |
| de            | German           |
| el            | Greek            |
| he            | Hebrew           |
| hi            | Hindi            |
| hu            | Hungarian        |
| id            | Indonesian       |
| it            | Italian          |
| ja            | Japanese         |
| ko            | Korean           |
| lv            | Latvian          |
| lt            | Lithuanian       |
| nb            | Norwegian-Bokmol |
| pl            | Polish           |
| pt            | Portuguese       |
| ro            | Romanian         |
| ru            | Russian          |
| sr            | Serbian          |
| sk            | Slovak           |
| sl            | Slovenian        |
| es            | Spanish          |
| sv            | Swedish          |
| tl            | Tagalog          |
| th            | Thai             |
| tr            | Turkish          |
| uk            | Ukrainian        |
| vi            | Vietnamese       |

| Country code | Country name   |
| ------------ | -------------- |
| AU           | Australia      |
| AT           | Austria        |
| BE           | Belgium        |
| BR           | Brazil         |
| GB           | Britain        |
| BG           | Bulgaria       |
| CA           | Canada         |
| HR           | Croatia        |
| CZ           | Czech Republic |
| DK           | Denmark        |
| EG           | Egypt          |
| FI           | Finland        |
| FR           | France         |
| DE           | Germany        |
| GR           | Greece         |
| HK           | Hong-Kong      |
| HU           | Hungary        |
| IN           | India          |
| ID           | Indonesia      |
| IE           | Ireland        |
| IL           | Israel         |
| IT           | Italy          |
| JP           | Japan          |
| KR           | Korea          |
| LV           | Latvia         |
| LI           | Liechtenstein  |
| LT           | Lithuania      |
| NL           | Netherlands    |
| NZ           | New Zealand    |
| NO           | Norway         |
| PH           | Philippines    |
| PL           | Poland         |
| PT           | Portugal       |
| CN           | PRC            |
| RO           | Romania        |
| RU           | Russia         |
| RS           | Serbia         |
| SG           | Singapore      |
| SK           | Slovakia       |
| SI           | Slovenia       |
| ES           | Spain          |
| SE           | Sweden         |
| CH           | Switzerland    |
| TW           | Taiwan         |
| TH           | Thailand       |
| TR           | Turkey         |
| UA           | Ukraine        |
| US           | USA            |
| VN           | Vietnam        |
| ZA           | Zimbabwe       |

### Supported device locales on iOS

| Locale code | Locale name             |
| ----------- | ----------------------- |
| en\_AU      | Australia (English)     |
| nl\_BE      | Belgium (Dutch)         |
| fr\_BE      | Belgium (French)        |
| ms\_BN      | Brunei Darussalam       |
| en\_CA      | Canada (English)        |
| fr\_CA      | Canada (French)         |
| cs\_CZ      | Czech Republic          |
| fi\_FI      | Finland                 |
| de\_DE      | Germany                 |
| el\_GR      | Greece                  |
| hu\_HU      | Hungary                 |
| hi\_IN      | India (Hindi)           |
| id\_ID      | Indonesia               |
| he\_IL      | Israel                  |
| it\_IT      | Italy                   |
| ja\_JP      | Japan                   |
| ms\_MY      | Malaysia                |
| nl\_NL      | Netherlands             |
| en\_NZ      | New Zealand             |
| nb\_NO      | Norway                  |
| tl\_PH      | Philippines             |
| pl\_PL      | Poland                  |
| zh\_CN      | PRC                     |
| ro\_RO      | Romania                 |
| ru\_RU      | Russia                  |
| en\_SG      | Singapore               |
| sk\_SK      | Slovakia                |
| ko\_KR      | Korea                   |
| sv\_SE      | Sweden                  |
| zh\_TW      | Taiwan                  |
| th\_TH      | Thailand                |
| tr\_TR      | Turkey                  |
| en\_GB      | UK (English)            |
| uk\_UA      | Ukraine                 |
| es\_US      | USA (Spanish)           |
| en\_US      | USA (English)           |
| vi\_VN      | Vietnam                 |
| pt-BR       | Brazil (Portuguese)     |
| zh-Hans     | China (Simplified)      |
| zh-Hant     | China (Traditional)     |
| zh-HK       | Hong Kong               |
| en-IN       | India (English)         |
| en-IE       | Ireland                 |
| es-419      | Latin America (Spanish) |
| es-MX       | Mexico (Spanish)        |
| en-ZA       | South Africa (English)  |
| es\_ES      | Spain                   |
| fr\_FR      | France                  |
