# Android - Jetpack Compose

<figure><img src="../.gitbook/assets/compose.png" alt=""><figcaption></figcaption></figure>

Maestro supports Jetpack Compose.

## Interacting with composable with Text

Given a composable with a displayed text:

```kotlin
Text(
    text = "Like",
    modifier = Modifier.fillMaxWidth(),
    textAlign = TextAlign.Center,
    style = MaterialTheme.typography.titleMedium,
    fontWeight = FontWeight.Bold
)
```

You can use the following command to tap on this `Text` :

```yaml
- tapOn: "Like"
```

## Interacting with composable with Accessibility

Given a composable without text, you can use semantics:

For the following composable:

```kotlin
FloatingActionButton(onClick = onClick, 
    modifier = Modifier
        .semantics { testTagsAsResourceId = true }.testTag("Add")
) {
    Icon(Icons.Filled.Add, "")
}
```

You can tap on this using `testTag`:&#x20;

```yaml
- tapOn: 
    id: "Add"
```

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

## Resources

* [How to automate your UI testing using Maestro](https://www.composables.co/blog/maestro)
