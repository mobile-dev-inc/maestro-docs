# Selectors

Commands that interact with a view (e.g `tapOn`, `assertVisible`, `copyTextFrom`) require the view to be specified using using a _selector_.

There are many different selectors available:

```yaml
- tapOn: # or any other command that works with selectors
    text: 'Text'     # (optional) Finds element with text or accessibility text that matches the regular expression
    id: 'the_id'     # (optional) Finds element with accessibility identifier that matches the regular expression
    index: 0         # (optional) 0-based index of the view to select among those that match all other criteria
    point: 50%, 50%  # (optional) Relative position on screen. "50%, 50%" is the middle of screen
    point: 50, 75    # (optional) Exact coordinates on screen. x:50 y:50, in pixels
    width: 100       # (optional) Finds element of a given width
    height: 100      # (optional) Finds element of a given height
    tolerance: 10    # (optional) Tolerance to apply when comparing width and height
    enabled: true    # (optional) Searches for view with a given "enabled" state
    checked: true    # (optional) Searches for view with a given "checked" state
    focused: true    # (optional) Searches for view with a given "focused" state
    selected: true   # (optional) Searches for view with a given "selected" state
```

### Shorthand selector for text

If you want to use the `text` selector, you can use the following shorthand:

```yaml
- tapOn: 'Text' # or any other command that works with selectors
```

### Relative position selectors

Apart from the selectors mentioned above, Maestro is also able to select views using their relative position (i.e. "below another view", or "contains child"):

```yaml
- tapOn: # or any other command that works with selectors
    below: View above that has this text       # matches a view *above* that has the given text
    above:
        id: view_below_id                      # matches a view *below* that has the given id
    leftOf: View to the right has this text
    rightOf: View to the left has this text
    containsChild: Text in a child view        # matches a view that has a *direct* child view with the given text
    childOf:                                   # matches a view that is a child of a view with id "buy-now"
        id: buy-now
    containsDescendants:                       # matches a view that has all the descendant views given below
        - id: title_id
          text: A descendant view has id "title_id" and this text
        - Another descendant view has this text
```

### Selecting one view among many similar

If you have multiple views matching the same selector (i.e. many views with text `Hello`), use `index` parameter to specify which one to select exactly. For example, the following command will pick the **3rd view** that has text `Hello`:

```yaml
- tapOn:
    text: Hello
    index: 2
```

### Using Regular Expressions

All text fields in Maestro element selectors are regular expressions. Whilst this document isn't intending to replace documentation on regular expressions (use your favourite search engine), here are a few examples of how it operates. In these examples, we've used `assertVisible`, but it's applicable to any text or id field.

#### Partial Matches

If you're on a screen with the sentence 'the quick brown fox jumps over the lazy log', and want to assert on two words in the sentence this won't work:

```yaml
- assertVisible: 'brown fox'
```

Because it's a regular expression, it needs to match the text of the entire element. This would work:

```yaml
- assertVisible: '.*brown fox.*'
```

#### Patterns

Regular Expressions are powerful. Imagine a screen that generates a random 6-digit number (like an OTP). Assuming you don't want to imbue your test with all of the code to generate an identical random number, you could assert that you're getting a number of the correct format like this:

```yaml
- assertVisible: '[0-9]{6}'
```

#### Escaping

One downside of regular expressions is that like any expression, there are control characters. If you're attempting to assert on the text 'Movies \[NEW]', this won't work:

```yaml
- assertVisible: 'Movies [NEW]'
```

That's because square brackets have meaning in regular expressions. Instead, you'll need this:

```yaml
- assertVisible: 'Movies \[NEW\]'
```



### Should I use text or IDs?

Text selectors are good when text is static. They improve the readability and intent of your tests. Anyone can come along and read what you're tapping / inputting / asserting without referring to other files. This is a massive benefit when it comes to maintenance, or to new people joining your project.

ID selectors are great when you just want to target something consistently, regardless of content. They're stable, great for more dynamic content, good for icons without text (like back buttons), and applications with internationalization.
