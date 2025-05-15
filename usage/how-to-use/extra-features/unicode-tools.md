---
description: How can I manage Unicode characters?
icon: square-u
---

# Unicode Tools

Using this functionality that is available on Textify is very simple! Just use the `Textify.Unicode` namespace in any piece of code you want to use the library, as in: `using Textify.Data.Unicode;`

Just use the `UnicodeTools` class that contains:

* `ReverseRtl(string)*`: Reverses the RTL characters.

{% hint style="info" %}
For functions that are marked with an asterisk, this means that the underlying function is available when `libicu` is installed. You may have to specify the path to the `libicu` and the `libicudata` libraries in some cases with `IcuLibPath` and `IcuDataLibPath`.
{% endhint %}
