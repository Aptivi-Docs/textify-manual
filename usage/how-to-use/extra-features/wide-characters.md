---
description: Characters that take up more than 16 bits!
icon: square-t
---

# Wide Characters

Wide characters are UTF-32 characters that are usually formed by surrogate pairs, which are connected with each other to form a single character not normally available in the UTF-16 encoding, such as what the predefined 2-byte `char` type in .NET is using.

***

## <mark style="color:$primary;">Usage</mark>

They are used in simple emojis and other characters, and Textify provides a solution to handle these characters, which is a `WideChar` struct. It's found in the `Textify.General.Structures` namespace.

{% hint style="warning" %}
While `WideChar` provides 32-bit characters, some of them, such as color-toned emojis or modified emojis, come with multiple characters, such as zero-width joiners, that can't be represented in a single `WideChar` struct.

Terminal emulators provide little to no support for such cases, and Textify won't support such characters, so they show up as multiple characters in the terminal. However, you can deal with such characters using [emoji management](emoji-management.md) functions.
{% endhint %}

<details>

<summary>Formation of wide characters</summary>

Wide characters take up 4 bytes, which means 32 bits. `WideChar` internally uses two 16-bit characters to indicate this wide character in its separated form:

* **Low character**: First two bytes of the whole wide character (Bytes 1 and 2), and is always populated unless the source character is a NUL character.
* **High character**: Last two bytes of the whole wide character (Bytes 3 and 4), and is always NUL unless the source exceeds the UTF-16 maximum size.

{% hint style="info" %}
According to Textify, high surrogate characters are "low characters" (due to no usage in normal ASCII characters) and low surrogate characters are "high characters" (due to frequent usage), because a `WideChar` instance doesn't necessarily represent a surrogate character, such as normal ASCII characters.

However, you can't get these individual high or low characters directly as they are used internally for operations, but you can use implicit casting to a tuple of two characters.
{% endhint %}

</details>

<details>

<summary>Creation of the wide character instance</summary>

You can create an instance of a wide character from one of the following sources:

* Source string representing a single wide character or a single normal character.
* Character code representing a result of logical OR of the high character integral value with 16 bits shifted to the left and the low character integral value without any bit shift: $$(Hi << 16) | Lo$$
* Two separate characters indicating a high character, which comes first in the parameters, and a low character.

{% hint style="info" %}
You can perform the usual `Parse()` and `TryParse()` function calls against either a string, a character code, or high and low characters, with the high character being the first and the low character being the second.
{% endhint %}

</details>

<details>

<summary>Casting to the wide character instance</summary>

You can either create a new instance manually using the `new` keyword or using explicit casting from the following types:

* String instances that represent a single wide character or a single normal character.
* Character code as mentioned above.

</details>

<details>

<summary>Casting from the wide character instance</summary>

You can perform implicit casting to the following types:

* A string to get the resultant character formed by putting the low and the high characters together, or just the low character if it's not a wide character.
* A tuple of characters to get two characters with the high character first and the low character second.
* An integer to get the character code as mentioned above.

</details>

<details>

<summary>Available comparison operators</summary>

You can use the following comparison operators between two `WideChar` instances:

<table><thead><tr><th width="110.3333740234375">Operator</th><th>Description</th></tr></thead><tbody><tr><td><code>==</code></td><td>Tests for equality of the two <code>WideChar</code> instances</td></tr><tr><td><code>!=</code></td><td>Tests for inequality of the two <code>WideChar</code> instances</td></tr><tr><td><code>&#x3C;</code></td><td>Checks to see if the first <code>WideChar</code> is less than the second <code>WideChar</code> by comparing their character codes</td></tr><tr><td><code>&#x3C;=</code></td><td>Checks to see if the first <code>WideChar</code> is less than or equal to the second <code>WideChar</code> by comparing their character codes</td></tr><tr><td><code>></code></td><td>Checks to see if the first <code>WideChar</code> is greater than the second <code>WideChar</code> by comparing their character codes</td></tr><tr><td><code>>=</code></td><td>Checks to see if the first <code>WideChar</code> is greater than or equal to the second <code>WideChar</code> by comparing their character codes</td></tr><tr><td><code>+</code></td><td>Performs the addition of the two <code>WideChar</code> instances</td></tr><tr><td><code>-</code></td><td>Performs the subtraction of the two <code>WideChar</code> instances</td></tr></tbody></table>

</details>

<details>

<summary>Available checking functions</summary>

You can also perform the following checks:

| Function             | Description                                                                                                                                 |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `IsValidChar()`      | Checks to see if this character is a valid character                                                                                        |
| `IsValidSurrogate()` | Checks to see if this character is a valid surrogate pair of both the low character (high surrogate) and the high character (low surrogate) |

</details>

<details>

<summary>Miscellaneous functions</summary>

Some extra functions can be found here:

<table><thead><tr><th width="151">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>GetWideChars()</code></td><td>Gets a list of wide characters from a string</td></tr></tbody></table>

</details>

***

## <mark style="color:$primary;">Unicode character width</mark>

For applications that need to deal with the Unicode character width as in console cells, we've introduced this fine feature from Terminaux that allows you to query a Unicode character for its width, such as:

* Modifier characters that take up zero console cells (i.e. zero width characters)
* English letters that take up one cell (i.e. half-width characters)
* Chinese characters that take up two cells (i.e. full-width characters)

{% hint style="info" %}
Please note that this information doesn't indicate the string length either by the amount of UTF-8 characters or by the text element as `StringInfo` class returns. This indicates how many console grid cells a character or a sentence consumes.

For example, when an application tries to get the string length that contains zero-width or full-width characters, it doesn't indicate the number of cells, but the number of absolute characters, so Chinese characters are considered as one character that takes up two cells and Arabic modifier characters are considered as one character that takes up zero cells.

If you want to measure the correct string length as how it would show up on a console, you should use this feature. The easiest way to use it is to rely on Terminaux's character extensions.
{% endhint %}
