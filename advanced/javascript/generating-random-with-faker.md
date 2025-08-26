---
description: >-
  Generating random values for your test data in JavaScript using Faker
---

# Generating Random Data

From Maestro 2.0, you can use DataFaker in JavaScript to generate all kinds of random data for use in tests.

As well as the other well known objects in Maestro's JavaScript engine, such as `output` and `maestro`, there's now also a `faker`. This is based on DataFaker, and works the same way as it would in Java ([see their docs](https://www.datafaker.net/documentation/getting-started/#usage)), including all of their [Providers](https://www.datafaker.net/documentation/providers/).

These are available in JavaScript files called via [runScript](../../api-reference/commands/runscript.md), or any JavaScript expression. The examples below use [evalScript](../../api-reference/commands/evalscript.md), but commands like [inputText](../../api-reference/commands/inputtext.md) also accept JavaScript expressions.

```yaml
appId: com.example.app
jsEngine: graaljs
---
- evalScript: ${output.thisName = faker.name().firstName()}
- evalScript: ${output.thisCreditCard = faker.expression('#{finance.creditcard}')} // same as faker.finance().creditcard()
- evalScript: ${console.log(output.thisName + ' has a credit card number ' + output.thisCreditCard)}

- evalScript: ${console.log(faker.lordOfTheRings().character() + ' is in ' + faker.lordOfTheRings().location())}

- evalScript: ${output.thisNumber = faker.expression("#{number.numberBetween '1' '10'}")}
- evalScript: ${console.log('Random number between 1 and 10 = ' + output.thisNumber)}
```

Note: This works in the default engine, GraalJS. It will not work in the Rhino engine.
