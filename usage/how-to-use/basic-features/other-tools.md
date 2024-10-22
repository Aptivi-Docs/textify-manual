---
description: Other text tools!
icon: wrench
---

# Other Tools

In addition to the text manipulation tools that we've uncovered, we have several other tools that you can use easily in your programs.

## Regular expression tool

All regular expression tools can be found in the `RegexTools` class that you can find within the `Textify.Tools` namespace. However, they are not extensions to strings.

### `IsValidRegex()`

```csharp
public static bool IsValidRegex(string pattern)
public static bool IsValidRegex(Regex pattern)
```

This function lets you determine whether the specified regular expression pattern contains a valid syntax. This is useful for easy verification of the regex pattern syntax to ensure that you can control the situation where the user code tried to provide invalid regular expression pattern. The `Regex` class by default doesn't validate the syntax until you attempt to match a string with it, so we've made a wrapper to simplify things by testing a specified pattern against an empty string.

### `ParseRegex()` and `TryParseRegex()`

```csharp
public static Regex ParseRegex(string pattern)
public static bool TryParseRegex(string pattern, out Regex? result)
```

These two functions allow you to parse a regular expression, returning an instance of a `Regex` class once it's been validated using the above function, `IsValidRegex()`.

* `ParseRegex()` throws an exception when an invalid regular expression syntax is detected.
* `TryParseRegex()` returns a boolean indicating that either the operation succeeded (`true`) or failed (`false`). When the operation fails, the resulting value is `null`.

## String syntax attribute

First introduced in .NET 7, you can use the string syntax attribute, called `StringSyntaxAttribute`, to give your strings in the function context, but it's only available in the source code level. This depends on your IDE and how it supports this attribute.

Here's a simple example of how to use it:

```csharp
public static bool IsValidRegex([StringSyntax(StringSyntaxAttribute.Regex)] string pattern) =>
    IsValidRegex(new Regex(pattern));
```

You can use this syntax attribute in not only .NET 7.0+ apps, but you can also use it in .NET Standard and .NET Framework applications.

{% hint style="warning" %}
When trying to use this attribute in .NET 7.0+ apps while using Textify, you'll notice this error message appearing in the error list:

```
The type 'StringSyntaxAttribute' exists in both 'Textify, Version=x.x.x.x, Culture=neutral, PublicKeyToken=21c82ea14d2d7748' and 'System.Runtime, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'
```

This is intentional, because Visual Studio only highlights the string based on context defined by this attribute when it is found in the `System.Diagnostics.CodeAnalysis` namespace.

To solve this error, you must make an alias of the `Textify.Offline` NuGet package by clicking on the Properties button in the right-click menu of the package and writing `global, TextifyAlias` to the `Aliases` property. Then, write the extern alias statement at the top of the source code file and modify the `using` statement for the `CodeAnalysis` namespace, such as:

```csharp
extern alias TextifyAlias;
using TextifyAlias::System.Diagnostics.CodeAnalysis;
```

After that, you should be able to use this attribute.
{% endhint %}

If everything works properly, you should be able to see that parts of your string, such as regex in the below screenshot, are highlighted in different colors, and warnings should work, too.

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

## JSON tools

All JSON tools can be found in the `JsonTools` class that you can find within the `Textify.Tools` namespace. However, they are not extensions to strings. They are wrapped against `Newtonsoft.Json`.

### `BeautifyJson()` and `MinifyJson()`

```csharp
public static string BeautifyJson(string JsonFile)
public static string MinifyJson(string JsonFile)
```

Using these two functions, you can perform the following operations on a JSON file:

* `BeautifyJson()` returns a string that consists of a beautified version of your JSON file that you've passed as an argument.
* `MinifyJson()` returns a string that consists of a minified version of your JSON file that you've passed as an argument.

### `BeautifyJsonText()` and `MinifyJsonText()`

```csharp
public static string BeautifyJsonText(string JsonText)
public static string MinifyJsonText(string JsonText)
```

Using these two functions, you can perform the following operations on a JSON representation:

* `BeautifyJsonText()` returns a string that consists of a beautified version of your JSON text that you've passed as an argument.
* `MinifyJsonText()` returns a string that consists of a minified version of your JSON text that you've passed as an argument.

### `FindDifferences()`

```csharp
public static JObject FindDifferences(JToken sourceObj, JToken targetObj)
```

This function returns a JSON object that consists of collected differences between two different JSON tokens. If the JSON objects are the same, it returns an empty JSON object. Otherwise, it returns either a list of additions, deletions, or modifications if the target object type is an object, an array of additions and deletions if the target object type is an array, or an array of the whole object difference if the target object type is something else. To clarify this, here's an example of a difference between two objects:

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
