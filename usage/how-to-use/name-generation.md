---
description: Get a random name!
---

# 👤 Name Generation

{% hint style="info" %}
This feature requires a working Internet connection.
{% endhint %}

Using this function is very simple! Just use the `Textify.Online.NameGen` namespace in any piece of code you want to use the function, as in: `using Textify.Online.NameGen;`

Just use the `NameGenerator` class that contains:

* `GenerateNames()`
* `GenerateNames(int)`
* `GenerateNames(int, string, string, string, string)`

These functions call the `PopulateNames()` function to download the list of words and installs the list of words to the words list for the two above functions to use.

If the conditional version is used, you can specify the maximum amount of names, as well as supplying the name suffix and prefix and the surname suffix and prefix.

For example, if you called the generation function like this:

```csharp
var names = GenerateNames(5, "Th", "", "", "ey")
```

...it'll generate five full names that the first name starts with `Th` and that the surname ends with `ey`, for example:

```
Thomas Dawsey
Thalia Ermey
(...)
```
