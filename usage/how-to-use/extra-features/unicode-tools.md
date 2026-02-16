---
description: How can I manage Unicode characters?
icon: square-u
---

# Unicode Tools

Unicode tools are extra features of Textify that allow you to manage the Unicode characters and get information about them.

***

## <mark style="color:$primary;">Analysis tools</mark>

You can use the `UnicodeQuery` class found in the `Textify.Data.Unicode` namespace.

<details>

<summary>Available functions</summary>

The UnicodeQuery class contains the following functions:

<table><thead><tr><th width="309.6666259765625">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>QueryChar(char)</code></td><td>Queries a Unicode character and gets its information with a char.</td></tr><tr><td><code>QueryChar(int)</code></td><td>Queries a Unicode character and gets its information with a char number.</td></tr><tr><td><code>QueryChar(char, UnicodeQueryType)</code></td><td>Queries a Unicode character and gets its information with a char and a query type.</td></tr><tr><td><code>QueryChar(int, UnicodeQueryType)</code></td><td>Queries a Unicode character and gets its information with a char number and a query type.</td></tr></tbody></table>

</details>

<details>

<summary>Available query types</summary>

You can control which Unicode database this feature uses using the `UnicodeQueryType` enumeration:

* `Simple`: Simple Unicode characters without the Unihan characters and their info
* `Unihan`: All Unihan Unicode characters with just the Unihan info
* `Full`: All characters with their Unihan info

</details>

***

## <mark style="color:$primary;">Other tools</mark>

You can use the `UnicodeTools` class found in the `Textify.Data.Unicode` namespace to get access to other tools.

<details>

<summary>Reverse RTL</summary>

The following functions are available:

| Function       | Description                  |
| -------------- | ---------------------------- |
| `ReverseRtl()` | Reverses the RTL characters. |

{% hint style="info" %}
This function is available when `libicu` is installed. You may have to specify the path to the `libicu` and the `libicudata` libraries in some cases with `IcuLibPath` and `IcuDataLibPath`.
{% endhint %}

</details>
