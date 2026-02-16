---
description: Other text tools!
icon: wrench
---

# Other Tools

In addition to the text manipulation tools that we've uncovered, we have several other tools that you can use easily in your programs.

***

## <mark style="color:$primary;">Regular expression tools</mark>

All regular expression tools can be found in the `RegexTools` class that you can find within the `Textify.Tools` namespace. However, they are not extensions to strings.

<details>

<summary><code>IsValidRegex()</code></summary>

```csharp
public static bool IsValidRegex(string pattern) { }
public static bool IsValidRegex(Regex pattern) { }
```

This function lets you determine whether the specified regular expression pattern contains a valid syntax. This is useful for easy verification of the regex pattern syntax to ensure that you can control the situation where the user code tried to provide invalid regular expression pattern. The `Regex` class by default doesn't validate the syntax until you attempt to match a string with it, so we've made a wrapper to simplify things by testing a specified pattern against an empty string.

* `^[\w.-]+$` returns `true`
* `^[\w.-"]+$` returns `false`
* Empty regexes also return `true`

</details>

<details>

<summary><code>ParseRegex()</code> and <code>TryParseRegex()</code></summary>

```csharp
public static Regex ParseRegex(string pattern) { }
public static bool TryParseRegex(string pattern, out Regex? result) { }
```

These two functions allow you to parse a regular expression, returning an instance of a `Regex` class once it's been validated using the above function, `IsValidRegex()`.

* `ParseRegex()` throws an exception when an invalid regular expression syntax is detected.
* `TryParseRegex()` returns a boolean indicating that either the operation succeeded (`true`) or failed (`false`). When the operation fails, the resulting value is `null`.

</details>

<details>

<summary><code>IsMatch()</code>, <code>Match()</code>, and <code>Matches()</code></summary>

```csharp
public static bool IsMatch(string text, string pattern) { }
public static Match Match(string text, string pattern) { }
public static MatchCollection Matches(string text, string pattern) { }
```

These three functions allow you to check to see if the regular expression engine finds matches in the provided regular expression pattern tested against the text.

* `IsMatch()` returns `true` if there is a match; otherwise, `false`.
* `Match()` returns the first match is there is a match.
* `Matches()` returns all matches that are found.

</details>

<details>

<summary><code>Filter()</code></summary>

```csharp
public static string Filter(string text, string pattern) { }
public static string Filter(string text, string pattern, string replaceWith) { }
```

The above functions allow you to replace all matches in the text with either the replacement string or the empty string.

* The first function overload replaces all matches with an empty string
* The second function overload replaces all matches with the provided replacement string

</details>

<details>

<summary><code>Split()</code></summary>

```csharp
public static string[] Split(string text, string pattern) { }
```

The above function allows you to split the text using the regular expression pattern matches as the delimiter.

</details>

***

## <mark style="color:$primary;">JSON tools</mark>

All JSON tools can be found in the `JsonTools` class that you can find within the `Textify.Tools` namespace. However, they are not extensions to strings. They are wrapped against `Newtonsoft.Json`.

<details>

<summary><code>BeautifyJson()</code> and <code>MinifyJson()</code></summary>

```csharp
public static string BeautifyJson(string JsonFile) { }
public static string MinifyJson(string JsonFile) { }
```

Using these two functions, you can perform the following operations on a JSON file:

* `BeautifyJson()` returns a string that consists of a beautified version of your JSON file that you've passed as an argument.
* `MinifyJson()` returns a string that consists of a minified version of your JSON file that you've passed as an argument.

</details>

<details>

<summary><code>BeautifyJsonText()</code> and <code>MinifyJsonText()</code></summary>

```csharp
public static string BeautifyJsonText(string JsonText) { }
public static string MinifyJsonText(string JsonText) { }
```

Using these two functions, you can perform the following operations on a JSON representation:

* `BeautifyJsonText()` returns a string that consists of a beautified version of your JSON text that you've passed as an argument.
* `MinifyJsonText()` returns a string that consists of a minified version of your JSON text that you've passed as an argument.

</details>

<details>

<summary><code>FindDifferences()</code></summary>

```csharp
public static JObject FindDifferences(JToken sourceObj, JToken targetObj) { }
```

This function returns a JSON object that consists of collected differences between two different JSON tokens. The below rules are defined:

* If the JSON objects are the same, it returns an empty JSON object.
* Otherwise, it returns one of the following:
  * A list of additions, deletions, or modifications if the target object type is an object.
  * An array of additions and deletions if the target object type is an array.
  * An array of the whole object difference if the target object type is something else.

### <mark style="color:$primary;">Difference between two objects</mark>

To clarify this, here's an example of a difference between two objects:

{% code title="Source JSON" lineNumbers="true" %}
```json
{
  "LyricsPath": "C:/Users/MyUser/Music/",
  "DebugPath": "C:/Users/MyUser/Debug/",
  "DebugPath2": "C:/Users/MyUser/Debug2/",
  "DebugPath3": "C:/Users/MyUser/Debug3/",
  "DebugPath4": "C:/Users/MyUser/Debug4/",
}
```
{% endcode %}

{% code title="Target JSON" lineNumbers="true" %}
```json
{
  "LyricsPath": "C:/Users/MyUser/Music/",
  "DebugPath": "C:/Users/MyUser/Debug2/",
  "DebugPath2": "C:/Users/MyUser/Debug/",
  "DebugPath3": "C:/Users/MyUser/Debug3/",
  "DebugPath5": "C:/Users/MyUser/Debug4/",
}
```
{% endcode %}

{% code title="Resultant difference" lineNumbers="true" %}
```json
{
  "+DebugPath5": {
    "+": "DebugPath5"
  },
  "-DebugPath4": {
    "-": "DebugPath4"
  },
  "*DebugPath": {
    "*": {
      "source": "C:/Users/MyUser/Debug/",
      "target": "C:/Users/MyUser/Debug2/"
    }
  },
  "*DebugPath2": {
    "*": {
      "source": "C:/Users/MyUser/Debug2/",
      "target": "C:/Users/MyUser/Debug/"
    }
  },
  "*DebugPath5": {
    "*": {
      "source": null,
      "target": "C:/Users/MyUser/Debug4/"
    }
  }
}
```
{% endcode %}

A difference JSON object in this state can be described like this:

* `+<PropertyName>`: Indicates an addition
  * A JSON object with a single property, `+`, with the value that holds the name of the property.
* `-<PropertyName>`: Indicates a removal
  * A JSON object with a single property, `-`, with the value that holds the name of the property.
* `*<PropertyName>`: Indicates a modification
  * A JSON object with a single property, `*`, that has a JSON object that has the following two properties:
    * `source`: Old value of the property
    * `target`: New value of the property

### <mark style="color:$primary;">Difference between two arrays</mark>

Another example of a difference between two arrays:

{% code title="Source JSON" lineNumbers="true" %}
```json
[
  "C:/Users/MyUser/Music/",
  "C:/Users/MyUser/Debug/",
  "C:/Users/MyUser/Debug2/",
  "C:/Users/MyUser/Debug3/",
  "C:/Users/MyUser/Debug4/",
]
```
{% endcode %}

{% code title="Target JSON" lineNumbers="true" %}
```json
[
  "C:/Users/MyUser/Music/",
  "C:/Users/MyUser/Debug/",
  "C:/Users/MyUser/Debug2/",
]
```
{% endcode %}

{% code title="Resultant difference" lineNumbers="true" %}
```json
{
  "+": [],
  "-": [
    "C:/Users/MyUser/Debug3/",
    "C:/Users/MyUser/Debug4/"
  ]
}
```
{% endcode %}

A difference JSON object in this state is an object that contains two properties:

* `+`: Indicates additions
* `-`: Indicates removals

### <mark style="color:$primary;">Difference between two values</mark>

Another example of a difference between two values "`test`" and "`test2`":

{% code title="Resultant difference" lineNumbers="true" %}
```json
{
  "+": "test2",
  "-": "test"
}
```
{% endcode %}

A difference JSON object in this state is an object that contains two properties:

* `+`: Indicates a value of the target
* `-`: Indicates a value of the source

</details>
