---
description: Extensions that manipulate with text
icon: text-size
---

# Text Manipulation

Text tools can be found in the `TextTools` class under the `Textify.General` namespace. They make it easier for you to manipulate with strings.

### <mark style="color:$primary;">Character width tools</mark>

The below tools allow you to get the width of a character.

<details>

<summary><code>GetCharWidth()</code></summary>

```csharp
public static int GetCharWidth(int c) { }
```

This uses the Unicode width database that Textify maintains internally to be able to determine whether a character use one, two, or zero cells. Some of the characters are assigned as unassigned characters, and their handling can be controlled by the following properties:

```csharp
public static bool UseTwoCellsForUnassignedChars { get; set; }
```

{% hint style="info" %}
This is primarily used for console operations, and is a good start to implement console applications that support CJK, such as console applications that use [Terminaux](https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/G0KrE9Uk2AiblqjWtpAo/).
{% endhint %}

{% code title="Example" lineNumbers="true" %}
```
'\u001A' -> 0
'A' -> 1
'*' -> 1
'你' -> 2
```
{% endcode %}

</details>

<details>

<summary><code>GetCharWidthType()</code></summary>

```csharp
public static CharWidthType GetCharWidthType(int c) { }
```

This function allows you to easily get the character width type from a specified Unicode character codepoint. This will return one of the following types:

* Formatting
* NonPrinting
* Combining
* DoubleWidth
* Emoji
* Unassigned

{% code title="Example" lineNumbers="true" %}
```
'\u001A' -> NonPrinting
'A' -> -1
'*' -> -1
'你' -> DoubleWidth
```
{% endcode %}

</details>

### <mark style="color:$primary;">Wrapped sentence tools</mark>

The following functions allow you to wrap a long string into a specified length, both character-wise and word-wise.

<details>

<summary><code>GetWrappedSentences()</code></summary>

```csharp
public static string[] GetWrappedSentences(this string text, int maximumLength) { }
public static string[] GetWrappedSentences(this string text, int maximumLength, int indentLength) { }
```

This function allows you to wrap a long string into a list of strings that represent resultant lines. These lines correspond wrapped sentences by a specified length, and only wraps by the amount of characters. In addition to that, you can also specify an indentation length for the first line of the wrapped sentence.

* `Nitrocid` wrapped into four characters with no indentation will result in the following lines:
  * `Nitr`
  * `ocid`
* `Nitrocid` wrapped into four characters with 2 characters indentation will result in the following lines:
  * `Ni`
  * `troc`
  * `id`

{% hint style="info" %}
This function is also found in Terminaux, though it also employs VT sequence support to help process the text. For console applications, it's better to use the [Terminaux](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-extensions) version.
{% endhint %}

</details>

<details>

<summary><code>GetWrappedSentencesByWords()</code></summary>

```csharp
public static string[] GetWrappedSentencesByWords(this string text, int maximumLength) { }
public static string[] GetWrappedSentencesByWords(this string text, int maximumLength, int indentLength) { }
```

This function allows you to wrap a long string into a list of strings that represent resultant lines. These lines correspond wrapped sentences by a specified length, but also takes words into account, like word processors, for readability. In addition to that, you can also specify an indentation length for the first line of the wrapped sentence.

* `Nitrocid KS kernel sim` wrapped into four characters with no indentation will result in the following lines:
  * `Nitr`
  * `ocid`
  * `KS`
  * `kern`
  * `el`
  * `sim`
* `Nitrocid KS kernel sim` wrapped into four characters with 2 characters indentation will result in the following lines:
  * `Ni`
  * `troc`
  * `id`
  * `KS`
  * `kern`
  * `el`
  * `sim`

{% hint style="info" %}
This function is also found in Terminaux, though it also employs VT sequence support to help process the text. For console applications, it's better to use the [Terminaux](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-extensions) version.
{% endhint %}

</details>

### <mark style="color:$primary;">Double quote tools</mark>

The following functions manipulate with the double quotation in the string.

<details>

<summary><code>SplitEncloseDoubleQuotes()</code></summary>

```csharp
public static string[] SplitEncloseDoubleQuotes(this string target) { }
public static string[] SplitEncloseDoubleQuotes(this string target, char[]? partialQuoteSplitChars = null) { }
public static string[] SplitEncloseDoubleQuotes(this string target, char match = ' ', char[]? partialQuoteSplitChars = null) { }
public static string[] SplitEncloseDoubleQuotes(this string target, Func<char, bool> condition, char[]? partialQuoteSplitChars = null) { }
```

This function splits a string with either a new line, a specific character, or a character condition, with support for splitting with double quotation marks (single quote, double quote, or backticks), while releasing the quotation marks that surround the string.

* A string, `First "Second Third" Fourth`, will be split like this:
  * `First`
  * `Second Third`
  * `Fourth`

{% hint style="info" %}
Partial quote split characters can also be specified, but you'll need to be aware of the implications when using it, so it's best not to specify unless you're dealing with a very specific string.
{% endhint %}

</details>

<details>

<summary><code>SplitEncloseDoubleQuotesNoRelease()</code></summary>

```csharp
public static string[] SplitEncloseDoubleQuotesNoRelease(this string target) { }
public static string[] SplitEncloseDoubleQuotesNoRelease(this string target, char[]? partialQuoteSplitChars = null) { }
public static string[] SplitEncloseDoubleQuotesNoRelease(this string target, char match = ' ', char[]? partialQuoteSplitChars = null) { }
public static string[] SplitEncloseDoubleQuotesNoRelease(this string target, Func<char, bool> condition, char[]? partialQuoteSplitChars = null) { }
```

This function splits a string with either a new line, a specific character, or a character condition, with support for splitting with double quotation marks (single quote, double quote, or backticks), without releasing the quotation marks that surround the string.

A string, `First "Second Third" Fourth`, will be split like this:

* `First`
* `"Second Third"`
* `Fourth`

{% hint style="info" %}
Partial quote split characters can also be specified, but you'll need to be aware of the implications when using it, so it's best not to specify unless you're dealing with a very specific string.
{% endhint %}

</details>

<details>

<summary><code>ReleaseDoubleQuotes()</code></summary>

```csharp
public static string ReleaseDoubleQuotes(this string target)
```

This function allows you to remove surrounding double quotes from the beginning and the end of the string. For example, the following strings will be changed:

* `"Double quotes"` -> `Double quotes`
* `'Single quotes'` -> `Single quotes`
* `` `Backticks` `` -> `Backticks`

</details>

<details>

<summary><code>GetEnclosedDoubleQuotesType()</code></summary>

```csharp
public static EnclosedDoubleQuotesType GetEnclosedDoubleQuotesType(this string target)
```

This function allows you to determine the type of the double quotation that is found in the beginning and the end of the string. The following strings will be processed this way:

* `"Double quotes"` -> `EnclosedDoubleQuotesType.DoubleQuotes`
* `'Single quotes'` -> `EnclosedDoubleQuotesType.SingleQuotes`
* `` `Backticks` `` -> `EnclosedDoubleQuotesType.Backticks`
* `Normal` -> `EnclosedDoubleQuotesType.None`

</details>

### <mark style="color:$primary;">New line tools</mark>

The following functions manipulate with the new lines in the string.

<details>

<summary><code>SplitNewLines()</code></summary>

```csharp
public static string[] SplitNewLines(this string target, bool emptyStrings = true) { }
```

This function allows you to easily split the string by new lines. You can optionally exclude empty lines by setting `emptyStrings` to `false`. This is platform-agnostic so that you don't have to specify what kind of new line you're splitting with.

* A string that contains line breaking characters, such as `"First\r\nSecond\r\nThird"`, will be split like this:
  * `First`
  * `Second`
  * `Third`

</details>

<details>

<summary><code>UnixifyNewLines()</code></summary>

```csharp
public static string UnixifyNewLines(this string target) { }
```

This function allows you to normalize the new line characters to convert them to Unix-based newlines (`LF`). This supports common and uncommon new line characters, such as `CR` + `LF` for Windows, `CR` for Mac OS 9, and others. This conforms to the Unicode standards.

* `"First\r\nSecond\r\nThird"` -> `"First\nSecond\nThird"`
* `"First\rSecond\rThird"` -> `"First\nSecond\nThird"`

</details>

<details>

<summary><code>TrimNewLines()</code></summary>

{% code expandable="true" %}
```csharp
public static string TrimNewLines(this string text) { }
public static string[] TrimNewLines(this string[] lines) { }
public static List<string> TrimNewLines(this List<string> lines) { }
```
{% endcode %}

This function allows you to trim the new lines from a string that contains new lines from the first lines and the last lines of the string. It can also remove empty lines from the start and the end of the string array.

Spaces that are in between the first non-empty line and the last non-empty line are not removed, but preserved.

</details>

### <mark style="color:$primary;">Starts, Ends, and Contains tools</mark>

The following functions allow you to perform different kinds of beginning, ending, and substring detection in the string.

<details>

<summary><code>StartsWithAnyOf()</code> and <code>StartsWithAllOf()</code></summary>

```csharp
public static bool StartsWithAnyOf(this string target, string[] values) { }
public static bool StartsWithAllOf(this string source, string[] values) { }
public static bool StartsWithAnyOf(this string target, char[] values) { }
public static bool StartsWithAllOf(this string source, char[] values) { }
```

This checks the string for a list of prefixes in the OR and the AND logical condition, respectively.

* `StartsWithAnyOf()` checks to see if any of the prefixes is found within the beginning of the string.
  * For example, this string `"pre_rel-01-Servicing"` returns `true` if any of `"pre_"` and `"rel_"` prefixes match.
* `StartsWithAllOf()` checks to see if all of the prefixes is found within the beginning of the string.
  * For example, this string `"dotnet-hostfxr-8.0"` returns `true` if all of `"dotnet-"` and `"dotnet-hostfxr-"` prefixes match, but returns `false` if one of the prefixes don't match, such as `"dotnet-runtime-8.0"`.

</details>

<details>

<summary><code>EndsWithAnyOf()</code> and <code>EndsWithAllOf()</code></summary>

```csharp
public static bool EndsWithAnyOf(this string target, string[] values) { }
public static bool EndsWithAllOf(this string source, string[] values) { }
public static bool EndsWithAnyOf(this string source, char[] values) { }
public static bool EndsWithAllOf(this string source, char[] values) { }
```

This checks the string for a list of suffixes in the OR and the AND logical condition, respectively.

* `EndsWithAnyOf()` checks to see if any of the suffixes is found within the ending of the string.
  * For example, this string `"Release-5.0-OOB"` returns `true` if either the `"-OOB"` or the `"-RTM"` suffixes match.
* `EndsWithAllOf()` checks to see if all of the suffixes is found within the ending of the string.
  * For example, this string `"Release-5.0-OOB"` returns `true` if both the `"-OOB"` and the `"-5.0-OOB"` suffixes match, but returns `false` if one of the suffixes doesn't match, for example, `"Release-4.6-OOB"`.

</details>

<details>

<summary><code>ContainsAnyOf()</code> and <code>ContainsAllOf()</code></summary>

```csharp
public static bool ContainsAnyOf(this string source, string[] targets) { }
public static bool ContainsAllOf(this string source, string[] targets) { }
public static bool ContainsAnyOf(this string source, char[] targets) { }
public static bool ContainsAllOf(this string source, char[] targets) { }
```

This checks the string for a list of substrings in the OR and the AND logical condition, respectively.

* `ContainsAnyOf()` checks to see if any of the substrings is found within the string.
  * For example, this string `"Branch-Prod-5.0"` returns `true` if either the `"Prod"` or the `"Staging"` substrings match.
* `ContainsAllOf()` checks to see if all of the substrings is found within the string.
  * For example, this string `"Branch-Prod-5.0"` returns `true` if both the `"Prod"` and the `"Branch"` substrings match, but returns `false` if one of the substrings doesn't match, for example, `"Branch-Staging-5.0"`.

</details>

### <mark style="color:$primary;">Replacement tools</mark>

The following functions allow you to perform replacement operations on a string.

<details>

<summary><code>ReplaceAll()</code></summary>

```csharp
public static string ReplaceAll(this string target, string[] toBeReplaced, string toReplace) { }
public static string ReplaceAll(this string target, string[] toBeReplaced, char toReplace) { }
public static string ReplaceAll(this string target, char[] toBeReplaced, string toReplace) { }
public static string ReplaceAll(this string target, char[] toBeReplaced, char toReplace) { }
```

This function allows you to perform a replacement of a list of specified characters or substrings with either a single string or a single character that will be used for replacement.

* `Please <replace> Nitrocid. This sub is a unit <replace2>.`
* Replacement string to replace `<replace>` and `<replace2>`: `test`
* Result: `Please test Nitrocid. This sub is a unit test.`

</details>

<details>

<summary><code>ReplaceAllRange()</code></summary>

```csharp
public static string ReplaceAllRange(this string target, string[] toBeReplaced, string[] toReplace) { }
public static string ReplaceAllRange(this string target, string[] toBeReplaced, char[] toReplace) { }
public static string ReplaceAllRange(this string target, char[] toBeReplaced, string[] toReplace) { }
public static string ReplaceAllRange(this string target, char[] toBeReplaced, char[] toReplace) { }
```

This function allows you to perform a replacement of a list of specified characters or substrings with either a list of strings or characters that will be used for replacement. This is a bulk replacement.

* `Please <replace> Nitrocid. This sub is a unit <replace2>.`
* Replacement strings to replace `<replace>` and `<replace2>`: `test the integrity of`, `test`
* Result: `Please test the integrity of Nitrocid. This sub is a unit test.`

{% hint style="warning" %}
In order for this to work, the length of both the replacement source array and the target array must be at the same length.
{% endhint %}

</details>

<details>

<summary><code>ReplaceLastOccurrence()</code></summary>

```csharp
public static string ReplaceLastOccurrence(this string source, string searchText, string replace) { }
public static string ReplaceLastOccurrence(this string source, string searchText, char replace) { }
public static string ReplaceLastOccurrence(this string source, char searchText, string replace) { }
public static string ReplaceLastOccurrence(this string source, char searchText, char replace) { }
```

This function allows you to replace the last occurrence of either a character or a substring with the target replacement character or substring.

* `Nitrocid is awesome and is great!`
* Replacement string to replace the last `is`: `its features are`
* Result: `Nitrocid is awesome and its features are great!`

</details>

<details>

<summary><code>ReplaceChar()</code></summary>

```csharp
public static string ReplaceChar(this string source, int idx, char replacement) { }
```

This function allows you to replace a character in a specified index with a replacement character.

* `Textyfy`
* Character to replace in index `4` (char 5): `i`
* Result: `Textify`

</details>

### <mark style="color:$primary;">Index tools</mark>

The following functions allow you to perform index operations on a string.

<details>

<summary><code>AllIndexesOf()</code></summary>

```csharp
public static IEnumerable<int> AllIndexesOf(this string target, string value) { }
public static IEnumerable<int> AllIndexesOf(this string target, char value) { }
```

This function allows you to get all indexes of either a target string or a target character. This allows for more specific replacements or analysis.

* `Nitrocid is awesome and is great!`
* Character to get its index in a string: `a`
* Results
  * First index: `12` (char 13)
  * Second index: `20` (char 21)
  * Third index: `30` (char 31)

</details>

### <mark style="color:$primary;">Format tools</mark>

The following functions allow you to perform formatting operations on a string.

<details>

<summary><code>FormatString()</code></summary>

```csharp
public static string FormatString(this string Format, params object?[]? Vars) { }
```

This function allows you to format a string using a string extension. This makes use of the [`String.Format()`](https://learn.microsoft.com/en-us/dotnet/api/system.string.format?view=net-8.0) function, but doesn't throw an exception. If formatting fails, the string is returned unmodified.

* `Nitrocid KS 0.0.1 first launched {0}/{1}/{2}.`
* Formatted variables: `2`, `22`, `2018`
* Result: `Nitrocid KS 0.0.1 first launched 2/22/2018.`

</details>

<details>

<summary><code>IsStringNumeric()</code></summary>

```csharp
public static bool IsStringNumeric(this string Expression) { }
```

This function checks to see whether this string can be expressed as a number or not. This function also supports double-precision floating point values.

* String `"1"` returns `true`
* String `"a"` returns `false`

</details>

### <mark style="color:$primary;">Prefix and suffix tools</mark>

The following functions allow you to perform operations on a prefix or a suffix within a string.

<details>

<summary><code>AddPrefix()</code> and <code>AddSuffix()</code></summary>

```csharp
public static string AddPrefix(this string text, string prefix, bool check = true) { }
public static string AddSuffix(this string text, string suffix, bool check = true) { }
```

These functions allow you to add either a prefix or a suffix to the string, respectively. This makes the task easier for you by automatically checking to see if the string already starts with a prefix or ends with a suffix.

* Prefixes
  * Adding prefixes with checking: `Hello` with `str` as prefix becomes `strHello`, and `strHello` with `str` as prefix becomes `strHello`.
  * Adding prefixes without checking: `Hello` with `str` as prefix becomes `strHello`, and `strHello` with `str` as prefix becomes `strstrHello`.
* Suffixes
  * Adding suffixes with checking: `Hello` with `str` as suffix becomes `Hellostr`, and `Hellostr` with `str` as suffix becomes `Hellostr`.
  * Adding suffixes without checking: `Hello` with `str` as suffix becomes `Hellostr`, and `Hellostr` with `str` as suffix becomes `Hellostrstr`.

{% hint style="info" %}
If you want to turn automatic checking off, you can set the `check` argument value to `false`.
{% endhint %}

</details>

<details>

<summary><code>RemovePrefix()</code> and <code>RemoveSuffix()</code></summary>

```csharp
public static string RemovePrefix(this string text, string prefix) { }
public static string RemoveSuffix(this string text, string suffix) { }
```

These functions allow you to remove either a prefix or a suffix to the string, respectively. This operation checks to see if the string already starts with a prefix or ends with a suffix.

* Prefixes: `strHello` with `str` as prefix becomes `Hello`.
* Suffixes: `Hellostr` with `str` as suffix becomes `Hello`.

</details>

<details>

<summary><code>VerifyPrefix()</code> and <code>VerifySuffix()</code></summary>

```csharp
public static bool VerifyPrefix(this string text, string prefix, StringComparison comparison = StringComparison.CurrentCulture) { }
public static bool VerifySuffix(this string text, string suffix, StringComparison comparison = StringComparison.CurrentCulture) { }
```

These functions allow you to verify a prefix and a suffix within a string by comparing the following:

* Prefix at the beginning of the string: Testing `strHello` with `str` as prefix returns `true`, and with `Hello` as prefix returns `false`.
* Suffix at the end of the string: Testing `Hellostr` with `str` as suffix returns `true`, and with `Hello` as suffix returns `false`.

{% hint style="info" %}
Currently, this comparison is case-sensitive according to your current culture settings determined by your operating system. However, the `comparison` argument lets you control case-sensitivity and culture-specific settings. For instance, you can make use of `OrdinalIgnoreCase` to verify the prefix or the suffix ordinally without checking for case sensitivity.
{% endhint %}

</details>

### <mark style="color:$primary;">Encoding tools</mark>

The following functions allow you to encode and decode your string easily.

<details>

<summary><code>GetBase64Encoded()</code></summary>

```csharp
public static string GetBase64Encoded(this string text) { }
```

This encodes a specified string and returns a BASE64 encoded string that can be decoded.

* For example, `Nitrocid KS` is converted to `Tml0cm9jaWQgS1M=`.

</details>

<details>

<summary><code>GetBase64Decoded()</code></summary>

```csharp
public static string GetBase64Decoded(this string text) { }
```

This decodes a specified BASE64 string and returns a decoded string that can be encoded.

For example, `Tml0cm9jaWQgS1M=` is converted to Nitrocid KS.

</details>

### <mark style="color:$primary;">Casing tools</mark>

The following functions allow you to manipulate with cases in a string.

<details>

<summary><code>UpperFirst()</code> and <code>LowerFirst()</code></summary>

```csharp
public static string UpperFirst(this string target) { }
public static string LowerFirst(this string target) { }
```

This allows you to make the first character in a string upper case or lower case.

* `UpperFirst()`: `hello` becomes `Hello`
* `LowerFirst()`: `Hello` becomes `hello`

</details>

<details>

<summary><code>ToTitleCase()</code></summary>

```csharp
public static string ToTitleCase(this string target) { }
```

This function allows you to change the casing of all words in a string except the small words that should be kept lowercase, such as the following:

* of
* the
* a
* an
* in
* on
* to
* from

For example, calling this function on the string `"Reconnecting your network to the work connection..."` becomes `"Reconnecting Your Network to the Work Connection..."`

</details>

### <mark style="color:$primary;">Escape tools</mark>

These tools allow you to escape and unescape some of the illegal characters.

{% hint style="info" %}
The following characters are escaped:

`\`, `*`, `+`, `?`, `|`, `{`, `[`, `(`, `)`, `^`, `$`, `.`, `#`,  , `-`, `"`, `'`, `` ` ``, `!`
{% endhint %}

<details>

<summary><code>Escape()</code></summary>

```csharp
public static string Escape(this string target) { }
```

This function allows you to escape some of the illegal characters for string parsing.

* `"Hello world!"` -> `"Hello\ world\!"`
* `"Helloworld"` -> `"Helloworld"`

</details>

<details>

<summary><code>Unescape()</code></summary>

```csharp
public static string Unescape(this string target) { }
```

This function allows you to unescape some of the illegal characters for human readability.

* `"Hello\ world\!"` -> `"Hello world!"`
* `"Helloworld"` -> `"Helloworld"`

</details>

### <mark style="color:$primary;">Letter repetition tools</mark>

The functions that fall into this category allow you to determine the letter repetition pattern by the number of steps.

<details>

<summary><code>GetLetterRepetitionPattern()</code></summary>

```csharp
public static int GetLetterRepetitionPattern(this string target, int steps) { }
```

This function allows you to get a number that represents a letter repetition pattern (LRP) that determines how many times a program needs to step `n` characters, which is specified in the `steps` parameter, before the final step round reaches the end of the string.

* `Hello!` with 3 LRP steps returns 2 rounds
* `Hello` with 7 LRP steps returns 5 rounds
* `Hello` with 5 LRP steps returns 1 round

</details>

<details>

<summary><code>GetLetterRepetitionPatternTable()</code></summary>

```csharp
public static ReadOnlyDictionary<int, int> GetLetterRepetitionPatternTable(this string target, bool twice = false) { }
public static ReadOnlyDictionary<int, int> GetLetterRepetitionPatternTable(this string target, int iterations) { }
```

These functions allow you to get a read-only dictionary that represents a number of steps taken multipled by the number of iterations.

* The first function overload allows you to specify either a single iteration or double iterations.
* The second function overload allows you to specify a number of iterations.

For example, a string with the length of 6 returns a dictionary consisting of the following values: `{ 1, 6 }, { 2, 3 }, { 3, 2 }, { 4, 3 }, { 5, 6 }, { 6, 1 }`

</details>

<details>

<summary><code>GetListOfRepeatedLetters()</code></summary>

```csharp
public static ReadOnlyDictionary<char, int> GetListOfRepeatedLetters(this string target, bool removeSingle = false) { }
```

This allows you to get a list of repeated letters in a read-only dictionary form:

* The key is a single unique character found in a string
* The value represents how many times a character has occurred in a string

{% hint style="info" %}
By default, this function populates characters that are only populated once. If you're not interested in this detail, you can remove them by passing the `removeSingle` argument as `true`.
{% endhint %}

For example, a list of repeated letters in the `Hello!` string becomes:

* With single letter occurrences:
  * `{ 'H', 1 }, { 'e', 1 }, { 'l', 2 }, { 'o', 1 }, { '!', 1 }`
* WIthout single letter occurrences:
  * `{ 'l', 2 }`

</details>

### <mark style="color:$primary;">Logical comparsion tools</mark>

These tools allow you to perform logical comparison operations in a string.

<details>

<summary><code>CompareLogical()</code></summary>

```csharp
public static int CompareLogical(string source, string compare) { }
```

This function allows you to compare two strings logically (that is, alphanumerically) similar to how Windows Explorer sorts files. This returns either a result of [`CompareTo()`](https://learn.microsoft.com/en-us/dotnet/api/system.string.compareto?view=net-8.0) against two strings or a result of the same function against two numeric chunks detected.

{% hint style="info" %}
Usually, you'll only need to use the `LogicalComparer` class as a comparer when sorting strings this way.
{% endhint %}

</details>

<details>

<summary><code>OrderLogically()</code> and <code>OrderDescendLogically()</code></summary>

```csharp
// Normal string arrays
public static string[] OrderLogically(this string[] source) { }
public static string[] OrderDescendLogically(this string[] source) { }

// IEnumerables
public static IEnumerable<string> OrderLogically(this IEnumerable<string> source) { }
public static IEnumerable<string> OrderDescendLogically(this IEnumerable<string> source) { }
```

This function simplifies the usage of the `LogicalComparer` class by wrapping it with the [`OrderBy()`](https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.orderby?view=net-8.0) and the [`OrderByDescending()`](https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.orderbydescending?view=net-8.0) functions.

</details>

### <mark style="color:$primary;">Case sensitive and insensitive comparison tools</mark>

These tools allow you to test strings for equality, prefixes, and suffixes in different ways.

<details>

<summary><code>EqualsNoCase()</code></summary>

```csharp
public static bool EqualsNoCase(this string source, string target, StringComparison comparison = StringComparison.OrdinalIgnoreCase) { }
```

This function allows you to test string equality easily without checking for case sensitivity.

* Comparing `Hello` against `Hello` returns true
* Comparing `Hello` against `HELLO` returns true

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCultureIgnoreCase`
* `StringComparison.InvariantCultureIgnoreCase`
* `StringComparison.OrdinalIgnoreCase`
{% endhint %}

</details>

<details>

<summary><code>EqualsCase()</code></summary>

```csharp
public static bool EqualsCase(this string source, string target, StringComparison comparison = StringComparison.Ordinal) { }
```

This function allows you to test string equality easily while checking for case sensitivity.

* Comparing `Hello` against `Hello` returns true
* Comparing `Hello` against `HELLO` returns false

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCulture`
* `StringComparison.InvariantCulture`
* `StringComparison.Ordinal`
{% endhint %}

</details>

<details>

<summary><code>StartsWithNoCase()</code></summary>

```csharp
public static bool StartsWithNoCase(this string source, string target, StringComparison comparison = StringComparison.OrdinalIgnoreCase)) { }
```

This function allows you to test string prefix easily without checking for case sensitivity.

* Testing `Hello` with `He` returns true
* Testing `Hello` with `HE` returns true

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCultureIgnoreCase`
* `StringComparison.InvariantCultureIgnoreCase`
* `StringComparison.OrdinalIgnoreCase`
{% endhint %}

</details>

<details>

<summary><code>StartsWithCase()</code></summary>

```csharp
public static bool StartsWithCase(this string source, string target, StringComparison comparison = StringComparison.Ordinal) { }
```

This function allows you to test string prefix easily while checking for case sensitivity.

* Testing `Hello` with `He` returns true
* Testing `Hello` with `HE` returns false

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCulture`
* `StringComparison.InvariantCulture`
* `StringComparison.Ordinal`
{% endhint %}

</details>

<details>

<summary><code>EndsWithNoCase()</code></summary>

```csharp
public static bool EndsWithNoCase(this string source, string target, StringComparison comparison = StringComparison.OrdinalIgnoreCase)) { }
```

This function allows you to test string suffix easily without checking for case sensitivity.

* Testing `Hello` with `lo` returns true
* Testing `Hello` with `Lo` returns true

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCultureIgnoreCase`
* `StringComparison.InvariantCultureIgnoreCase`
* `StringComparison.OrdinalIgnoreCase`
{% endhint %}

</details>

<details>

<summary><code>EndsWithCase()</code></summary>

```csharp
public static bool EndsWithCase(this string source, string target, StringComparison comparison = StringComparison.Ordinal) { }
```

This function allows you to test string suffix easily while checking for case sensitivity.

* Testing `Hello` with `lo` returns true
* Testing `Hello` with `Lo` returns false

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCulture`
* `StringComparison.InvariantCulture`
* `StringComparison.Ordinal`
{% endhint %}

</details>

<details>

<summary><code>ContainsWithNoCase()</code></summary>

```csharp
public static bool ContainsWithNoCase(this string source, string target) { }
```

This function allows you to check a substring without checking for case sensitivity.

* Testing `Hello` with `lo` returns true
* Testing `Hello` with `Lo` returns true

</details>

### <mark style="color:$primary;">Wide character and string tools</mark>

The following functions allow you to perform operations with wide strings and characters on a string.

<details>

<summary><code>GetWideChars()</code></summary>

```csharp
public static WideChar[] GetWideChars(this string sentence) { }
```

This function allows you to get a list of wide characters that are found within a string. A wide character description can be found in [this page](../extra-features/wide-characters.md).

</details>

### <mark style="color:$primary;">Miscellaneous tools</mark>

The following functions allow you to perform even more operations on a string.

<details>

<summary><code>ShiftLetters()</code></summary>

```csharp
public static string ShiftLetters(this string text, int shift) { }
```

This function allows you to easily shift characters within a string by a number of character shifting steps that can be specified from `-255` to `255`.

* Shift `Hello` by `1`: `Ifmmp`
* Shift `Hello` by `-1`: `Gdkkn`

</details>

<details>

<summary><code>TruncateString()</code></summary>

```csharp
public static string TruncateString(this string target, int threshold) { }
```

This function allows you to truncate a string into a specified string length. This helps in situations where wrapping is not possible or the user needs a truncated string.

* `Nitrocid is awesome and is great!` with the truncation threshold of `20`: `Nitrocid is awesome ...`

{% hint style="info" %}
This function is also found in Terminaux, though it also employs VT sequence support to help process the text. For console applications, it's better to use the [Terminaux](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-extensions) version.
{% endhint %}

</details>

<details>

<summary><code>Reverse()</code></summary>

```csharp
public static string Reverse(this string target) { }
```

This function allows you to easily reverse the order of characters in a string. For example, `Reversed` is `desreveR`.

</details>

<details>

<summary><code>GetEnclosedWordFromIndex()</code></summary>

```csharp
public static string GetEnclosedWordFromIndex(this string target, int sourceIdx, bool includeSymbols = false) { }
```

This function splits the string by spaces internally, then determines what word is from a specified source index. You can also include the symbols in the resultant enclosed word. Here are the following examples:

* Without symbols
  * `Hello world!` at index `2`: `Hello`
  * `Hello world!` at index `8`: `World`
* With symbols
  * `Hello world!` at index `2`: `Hello`
  * `Hello world!` at index `8`: `World!`

</details>

<details>

<summary><code>GetIndexOfEnclosedWordFromIndex()</code></summary>

```csharp
public static int GetIndexOfEnclosedWordFromIndex(this string target, int sourceIdx, bool includeSymbols = false) { }
```

This function splits the string by spaces internally, then determines what word is from a specified source index, and gets the index of its first character. You can also include the symbols in the resultant enclosed word. Here are the following examples:

* Without symbols
  * `!Hello world!` at index `2`: `1`
  * `Hello world!` at index `8`: `6`
* With symbols
  * `!Hello world!` at index `2`: `0`
  * `Hello world!` at index `8`: `6`

</details>

<details>

<summary><code>ReadNullTerminatedString()</code></summary>

```csharp
public static string ReadNullTerminatedString(this string source, int offset) { }
```

This function allows you to read a null-terminated string, optionally chopping the source string starting from `offset` index.

* `Hello\0Goodbye` with offset 3 becomes `lo`
* `Hello\0Goodbye` with offset 5 becomes an empty string
* `Hello\0Goodbye` with offset 6 becomes `Goodbye`

</details>

<details>

<summary><code>IsPalindrome()</code></summary>

```csharp
public static bool IsPalindrome(this string target, bool caseSensitive = false) { }
```

This function checks to see if a specified string is a palindrome or not. A string is considered to be a palindrome if the other half of the string is a mirror of the first half, such as `madam` or `noon`. Strings such as `Word` and `Laura` are not palindromes.

</details>

<details>

<summary><code>ToStringBuilder()</code></summary>

```csharp
public static StringBuilder ToStringBuilder(this string source) { }
```

This function allows you to easily get a string builder from a string to perform operations on a string without allocations.

</details>

<details>

<summary><code>BreakSurrogates()</code></summary>

```csharp
public static (char high, char low) BreakSurrogates(this string source) { }
```

This function allows you to break a string that consists of high surrogate and low surrogate characters into their individual character representations of the surrogates.

* `\U0001F607` becomes `('\ud83d', '\ude07')`
* `\U0001F923` becomes `('\ud83e', '\udd23')`
* `\U0001FAE1` becomes `('\ud83e', '\udee1')`

</details>

<details>

<summary><code>Paragraphize()</code></summary>

{% code expandable="true" %}
```csharp
public static string[] Paragraphize(this string text, bool wrapLines = true, int wrapWidth = 75) { }
```
{% endcode %}

This function allows you to turn a piece of text to an array of lines that are processed for paragraph rendering. This means that excess new lines are removed from the string, while allowing you to choose whether to wrap the lines or not. Currently, this function wraps the lines, but you can tell it not to wrap them.

New lines are trimmed from the first and the last new lines, while excess new lines are removed from the string, replacing them with only one new line.

</details>
