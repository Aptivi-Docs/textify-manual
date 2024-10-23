---
icon: text-size
description: Extensions that manipulate with text
---

# Text Manipulation

Textify has a main goal of providing you with text extensions that allow you to perform various operations on a string, and they will be listed individually in this page to have a quick overview of what each function does.

## Text tools

Text tools can be found in the `TextTools` class under the `Textify.Global` namespace. They make it easier for you to manipulate with strings.

### Character width tools

The below tools allow you to get the width of a character.

#### `GetCharWidth()`

```csharp
public static int GetCharWidth(int c)
```

This uses the Unicode width database that Textify maintains internally to be able to determine whether a character use one, two, or zero cells. Some of the characters are either assigned as ambiguous, are private use characters, or unassigned characters, and their handling can be controlled by the following properties:

```csharp
public static bool UseTwoCellsForUnassignedChars { get; set; }
public static bool UseTwoCellsForAmbiguousChars { get; set; }
public static bool UseTwoCellsForPrivateChars { get; set; }
```

{% hint style="info" %}
This is primarily used for console operations, and is a good start to implement console applications that support CJK, such as console applications that use [Terminaux](https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/G0KrE9Uk2AiblqjWtpAo/).
{% endhint %}

#### `GetCharWidthType()`

```csharp
public static CharWidthType GetCharWidthType(int c)
```

This function allows you to easily get the character width type from a specified Unicode character codepoint. This will return one of the following types:

* Private
* NonPrinting
* Combining
* DoubleWidth
* Ambiguous
* Emoji
* Unassigned

### Wrapped sentence tools

The following functions allow you to wrap a long string into a specified length, both character-wise and word-wise.

{% hint style="info" %}
The below functions are also found in Terminaux, though they also employ VT sequence support to help process them. For console applications, it's better to use the [Terminaux](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-extensions) version.
{% endhint %}

#### `GetWrappedSentences()`

```csharp
public static string[] GetWrappedSentences(this string text, int maximumLength)
public static string[] GetWrappedSentences(this string text, int maximumLength, int indentLength)
```

This function allows you to wrap a long string into a list of strings that represent resultant lines. These lines correspond wrapped sentences by a specified length, and only wraps by the amount of characters. In addition to that, you can also specify an indentation length for the first line of the wrapped sentence.

* `Nitrocid` wrapped into four characters with no indentation will result in the following lines:
  * `Nitr`
  * `ocid`
* `Nitrocid` wrapped into four characters with 2 characters indentation will result in the following lines:
  * `Ni`
  * `troc`
  * `id`

#### `GetWrappedSentencesByWords()`

```csharp
public static string[] GetWrappedSentencesByWords(this string text, int maximumLength)
public static string[] GetWrappedSentencesByWords(this string text, int maximumLength, int indentLength)
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

### Double quote tools

The following functions manipulate with the double quotation in the string.

#### `SplitEncloseDoubleQuotes()`

```csharp
public static string[] SplitEncloseDoubleQuotes(this string target)
public static string[] SplitEncloseDoubleQuotes(this string target, char[]? partialQuoteSplitChars = null)
public static string[] SplitEncloseDoubleQuotes(this string target, char match = ' ', char[]? partialQuoteSplitChars = null)
public static string[] SplitEncloseDoubleQuotes(this string target, Func<char, bool> condition, char[]? partialQuoteSplitChars = null)
```

This function splits a string with either a new line, a specific character, or a character condition, with support for splitting with double quotation marks (single quote, double quote, or backticks), while releasing the quotation marks that surround the string.

_The primary reason was that because we were uncomfortable with the usage of `Microsoft.VisualBasic` in C# applications as we were migrating to C# for Nitrocid KS in 2022._

* A string, `First "Second Third" Fourth`, will be split like this:
  * `First`
  * `Second Third`
  * `Fourth`

{% hint style="info" %}
Partial quote split characters can also be specified, but you'll need to be aware of the implications when using it, so it's best not to specify unless you're dealing with a very specific string.
{% endhint %}

#### `SplitEncloseDoubleQuotesNoRelease()`

```csharp
public static string[] SplitEncloseDoubleQuotesNoRelease(this string target)
public static string[] SplitEncloseDoubleQuotesNoRelease(this string target, char[]? partialQuoteSplitChars = null)
public static string[] SplitEncloseDoubleQuotesNoRelease(this string target, char match = ' ', char[]? partialQuoteSplitChars = null)
public static string[] SplitEncloseDoubleQuotesNoRelease(this string target, Func<char, bool> condition, char[]? partialQuoteSplitChars = null)
```

This function splits a string with either a new line, a specific character, or a character condition, with support for splitting with double quotation marks (single quote, double quote, or backticks), without releasing the quotation marks that surround the string.

_The primary reason was that because we were uncomfortable with the usage of `Microsoft.VisualBasic` in C# applications as we were migrating to C# for Nitrocid KS in 2022._

A string, `First "Second Third" Fourth`, will be split like this:

* `First`
* `"Second Third"`
* `Fourth`

{% hint style="info" %}
Partial quote split characters can also be specified, but you'll need to be aware of the implications when using it, so it's best not to specify unless you're dealing with a very specific string.
{% endhint %}

#### `ReleaseDoubleQuotes()`

```csharp
public static string ReleaseDoubleQuotes(this string target)
```

This function allows you to remove surrounding double quotes from the beginning and the end of the string. For example, the following strings will be changed:

* `"Double quotes"` -> `Double quotes`
* `'Single quotes'` -> `Single quotes`
* `` `Backticks` `` -> `Backticks`

#### `GetEnclosedDoubleQuotesType()`

```csharp
public static EnclosedDoubleQuotesType GetEnclosedDoubleQuotesType(this string target)
```

This function allows you to determine the type of the double quotation that is found in the beginning and the end of the string. The following strings will be processed this way:

* `"Double quotes"` -> `EnclosedDoubleQuotesType.DoubleQuotes`
* `'Single quotes'` -> `EnclosedDoubleQuotesType.SingleQuotes`
* `` `Backticks` `` -> `EnclosedDoubleQuotesType.Backticks`
* `Normal` -> `EnclosedDoubleQuotesType.None`

### New line tools

The following functions manipulate with the new lines in the string.

#### `SplitNewLines()`

```csharp
public static string[] SplitNewLines(this string target, bool emptyStrings = true)
```

This function allows you to easily split the string by new lines. You can optionally exclude empty lines by setting `emptyStrings` to `false`. This is platform-agnostic so that you don't have to specify what kind of new line you're splitting with.

* A string that contains line breaking characters, such as `"First\r\nSecond\r\nThird"`, will be split like this:
  * `First`
  * `Second`
  * `Third`

#### `UnixifyNewLines()`

```csharp
public static string UnixifyNewLines(this string target)
```

This function allows you to normalize the new line characters to convert them to Unix-based newlines (`LF`). This supports common and uncommon new line characters, such as `CR` + `LF` for Windows, `CR` for Mac OS 9, and others. This conforms to the Unicode standards.

* `"First\r\nSecond\r\nThird"` -> `"First\nSecond\nThird"`
* `"First\rSecond\rThird"` -> `"First\nSecond\nThird"`

### Starts, Ends, and Contains tools

The following functions allow you to perform different kinds of beginning, ending, and substring detection in the string.

#### `StartsWithAnyOf()` and `StartsWithAllOf()`

```csharp
public static bool StartsWithAnyOf(this string target, string[] values)
public static bool StartsWithAllOf(this string source, string[] values)
public static bool StartsWithAnyOf(this string target, char[] values)
public static bool StartsWithAllOf(this string source, char[] values)
```

This checks the string for a list of prefixes in the OR and the AND logical condition, respectively.

* `StartsWithAnyOf()` checks to see if any of the prefixes is found within the beginning of the string.
  * For example, this string `"pre_rel-01-Servicing"` returns `true` if any of `"pre_"` and `"rel_"` prefixes match.
* `StartsWithAllOf()` checks to see if all of the prefixes is found within the beginning of the string.
  * For example, this string `"dotnet-hostfxr-8.0"` returns `true` if all of `"dotnet-"` and `"dotnet-hostfxr-"` prefixes match, but returns `false` if one of the prefixes don't match, such as `"dotnet-runtime-8.0"`.

#### `EndsWithAnyOf()` and `EndsWithAllOf()`

```csharp
public static bool EndsWithAnyOf(this string target, string[] values)
public static bool EndsWithAllOf(this string source, string[] values)
public static bool EndsWithAnyOf(this string source, char[] values)
public static bool EndsWithAllOf(this string source, char[] values)
```

This checks the string for a list of suffixes in the OR and the AND logical condition, respectively.

* `EndsWithAnyOf()` checks to see if any of the suffixes is found within the ending of the string.
  * For example, this string `"Release-5.0-OOB"` returns `true` if either the `"-OOB"` or the `"-RTM"` suffixes match.
* `EndsWithAllOf()` checks to see if all of the suffixes is found within the ending of the string.
  * For example, this string `"Release-5.0-OOB"` returns `true` if both the `"-OOB"` and the `"-5.0-OOB"` suffixes match, but returns `false` if one of the suffixes doesn't match, for example, `"Release-4.6-OOB"`.

`ContainsAnyOf()` and `ContainsAllOf()`

```csharp
public static bool ContainsAnyOf(this string source, string[] targets)
public static bool ContainsAllOf(this string source, string[] targets)
public static bool ContainsAnyOf(this string source, char[] targets)
public static bool ContainsAllOf(this string source, char[] targets)
```

This checks the string for a list of substrings in the OR and the AND logical condition, respectively.

* `ContainsAnyOf()` checks to see if any of the substrings is found within the string.
  * For example, this string `"Branch-Prod-5.0"` returns `true` if either the `"Prod"` or the `"Staging"` substrings match.
* `ContainsAllOf()` checks to see if all of the substrings is found within the string.
  * For example, this string `"Branch-Prod-5.0"` returns `true` if both the `"Prod"` and the `"Branch"` substrings match, but returns `false` if one of the substrings doesn't match, for example, `"Branch-Staging-5.0"`.

### Replacement tools

The following functions allow you to perform replacement operations on a string.

#### `ReplaceAll()`

```csharp
public static string ReplaceAll(this string target, string[] toBeReplaced, string toReplace)
public static string ReplaceAll(this string target, string[] toBeReplaced, char toReplace)
public static string ReplaceAll(this string target, char[] toBeReplaced, string toReplace)
public static string ReplaceAll(this string target, char[] toBeReplaced, char toReplace)
```

This function allows you to perform a replacement of a list of specified characters or substrings with either a single string or a single character that will be used for replacement.

* `Please <replace> Nitrocid. This sub is a unit <replace2>.`
* Replacement string to replace `<replace>` and `<replace2>`: `test`
* Result: `Please test Nitrocid. This sub is a unit test.`

#### `ReplaceAllRange()`

```csharp
public static string ReplaceAllRange(this string target, string[] toBeReplaced, string[] toReplace)
public static string ReplaceAllRange(this string target, string[] toBeReplaced, char[] toReplace)
public static string ReplaceAllRange(this string target, char[] toBeReplaced, string[] toReplace)
public static string ReplaceAllRange(this string target, char[] toBeReplaced, char[] toReplace)
```

This function allows you to perform a replacement of a list of specified characters or substrings with either a list of strings or characters that will be used for replacement. This is a bulk replacement.

* `Please <replace> Nitrocid. This sub is a unit <replace2>.`
* Replacement strings to replace `<replace>` and `<replace2>`: `test the integrity of`, `test`
* Result: `Please test the integrity of Nitrocid. This sub is a unit test.`

{% hint style="warning" %}
In order for this to work, the length of both the replacement source array and the target array must be at the same length.
{% endhint %}

#### `ReplaceLastOccurrence()`

```csharp
public static string ReplaceLastOccurrence(this string source, string searchText, string replace)
public static string ReplaceLastOccurrence(this string source, string searchText, char replace)
public static string ReplaceLastOccurrence(this string source, char searchText, string replace)
public static string ReplaceLastOccurrence(this string source, char searchText, char replace)
```

This function allows you to replace the last occurrence of either a character or a substring with the target replacement character or substring.

* `Nitrocid is awesome and is great!`
* Replacement string to replace the last `is`: `its features are`
* Result: `Nitrocid is awesome and its features are great!`

`ReplaceChar()`

```csharp
public static string ReplaceChar(this string source, int idx, char replacement)
```

This function allows you to replace a character in a specified index with a replacement character.

* `Textyfy`
* Character to replace in index `4` (char 5): `i`
* Result: `Textify`

### Index tools

The following functions allow you to perform index operations on a string.

#### `AllIndexesOf()`

```csharp
public static IEnumerable<int> AllIndexesOf(this string target, string value)
public static IEnumerable<int> AllIndexesOf(this string target, char value)
```

This function allows you to get all indexes of either a target string or a target character. This allows for more specific replacements or analysis.

* `Nitrocid is awesome and is great!`
* Character to get its index in a string: `a`
* Results
  * First index: `12` (char 13)
  * Second index: `20` (char 21)
  * Third index: `30` (char 31)

### Format tools

The following functions allow you to perform formatting operations on a string.

#### `FormatString()`

```csharp
public static string FormatString(this string Format, params object?[]? Vars)
```

This function allows you to format a string using a string extension. This makes use of the [`String.Format()`](https://learn.microsoft.com/en-us/dotnet/api/system.string.format?view=net-8.0) function, but doesn't throw an exception. If formatting fails, the string is returned unmodified.

* `Nitrocid KS 0.0.1 first launched {0}/{1}/{2}.`
* Formatted variables: `2`, `22`, `2018`
* Result: `Nitrocid KS 0.0.1 first launched 2/22/2018.`

#### `IsStringNumeric()`

```csharp
public static bool IsStringNumeric(this string Expression)
```

This function checks to see whether this string can be expressed as a number or not. This function also supports double-precision floating point values.

* String `"1"` returns `true`
* String `"a"` returns `false`

### Prefix and suffix tools

The following functions allow you to perform operations on a prefix or a suffix within a string.

#### `AddPrefix()` and `AddSuffix()`

```csharp
public static string AddPrefix(this string text, string prefix, bool check = true)
public static string AddSuffix(this string text, string suffix, bool check = true)
```

These functions allow you to add either a prefix or a suffix to the string, respectively. This makes the task easier for you by automatically checking to see if the string already starts with a prefix or ends with a suffix.

* Prefixes
  * Adding prefixes with checking: `Hello` with `str` as prefix becomes `strHello`, and `strHello` with `str` as prefix becomes `strHello`.
  * Adding prefixes without checking: `Hello` with `str` as prefix becomes `strHello`, and `strHello` with `str` as prefix becomes `strstrHello`.
* Suffixes
  * Adding suffixes with checking:&#x20;

{% hint style="info" %}
If you want to turn automatic checking off, you can set the `check` argument value to `false`.
{% endhint %}

#### `RemovePrefix()` and `RemoveSuffix()`

```csharp
public static string RemovePrefix(this string text, string prefix)
public static string RemoveSuffix(this string text, string suffix)
```

These functions allow you to remove either a prefix or a suffix to the string, respectively. This operation checks to see if the string already starts with a prefix or ends with a suffix.

#### `VerifyPrefix()` and `VerifySuffix()`

```csharp
public static bool VerifyPrefix(this string text, string prefix, StringComparison comparison = StringComparison.CurrentCulture)
public static bool VerifySuffix(this string text, string suffix, StringComparison comparison = StringComparison.CurrentCulture)
```

These functions allow you to verify a prefix and a suffix within a string by comparing the following:

* Prefix at the beginning of the string
* Suffix at the end of the string

{% hint style="info" %}
Currently, this comparison is case-sensitive according to your current culture settings determined by your operating system. However, the `comparison` argument lets you control case-sensitivity and culture-specific settings. For instance, you can make use of `OrdinalIgnoreCase` to verify the prefix or the suffix ordinally without checking for case sensitivity.
{% endhint %}

### Encoding tools

The following functions allow you to encode and decode your string easily.

#### `GetBase64Encoded()`

```csharp
public static string GetBase64Encoded(this string text)
```

This encodes a specified string and returns a BASE64 encoded string that can be decoded.

#### `GetBase64Decoded()`

```csharp
public static string GetBase64Decoded(this string text)
```

This decodes a specified BASE64 string and returns a decoded string that can be encoded.

### Casing tools

The following functions allow you to manipulate with cases in a string.

#### `UpperFirst()` and `LowerFirst()`

```csharp
public static string UpperFirst(this string target)
public static string LowerFirst(this string target)
```

This allows you to make the first character in a string upper case or lower case.

#### `ToTitleCase()`

```csharp
public static string ToTitleCase(this string target)
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

### Escape tools

These tools allow you to escape and unescape some of the illegal characters.

{% hint style="info" %}
The following characters are escaped:

`\`, `*`, `+`, `?`, `|`, `{`, `[`, `(`, `)`, `^`, `$`, `.`, `#`,  , `-`, `"`, `'`, `` ` ``, `!`
{% endhint %}

#### `Escape()`

```csharp
public static string Escape(this string target)
```

This function allows you to escape some of the illegal characters for string parsing.

#### `Unescape()`

```csharp
public static string Unescape(this string target)
```

This function allows you to unescape some of the illegal characters for human readability.

### Letter repetition tools

The functions that fall into this category allow you to determine the letter repetition pattern by the number of steps.

#### `GetLetterRepetitionPattern()`

```csharp
public static int GetLetterRepetitionPattern(this string target, int steps)
```

This function allows you to get a number that represents a letter repetition pattern (LRP) that determines how many times a program needs to step `n` characters, which is specified in the `steps` parameter, before the final step round reaches the end of the string.

#### `GetLetterRepetitionPatternTable()`

```csharp
public static ReadOnlyDictionary<int, int> GetLetterRepetitionPatternTable(this string target, bool twice = false)
public static ReadOnlyDictionary<int, int> GetLetterRepetitionPatternTable(this string target, int iterations)
```

These functions allow you to get a read-only dictionary that represents a number of steps taken multipled by the number of iterations.

* The first function overload allows you to specify either a single iteration or double iterations.
* The second function overload allows you to specify a number of iterations.

#### `GetListOfRepeatedLetters()`

```csharp
public static ReadOnlyDictionary<char, int> GetListOfRepeatedLetters(this string target, bool removeSingle = false)
```

This allows you to get a list of repeated letters in a read-only dictionary form:

* The key is a single unique character found in a string
* The value represents how many times a character has occurred in a string

{% hint style="info" %}
By default, this function populates characters that are only populated once. If you're not interested in this detail, you can remove them by passing the `removeSingle` argument as `true`.
{% endhint %}

### Logical comparsion tools

These tools allow you to perform logical comparison operations in a string.

#### `CompareLogical()`

```csharp
public static int CompareLogical(string source, string compare)
```

This function allows you to compare two strings logically (that is, alphanumerically) similar to how Windows Explorer sorts files. This returns either a result of [`CompareTo()`](https://learn.microsoft.com/en-us/dotnet/api/system.string.compareto?view=net-8.0) against two strings or a result of the same function against two numeric chunks detected.

{% hint style="info" %}
Usually, you'll only need to use the `LogicalComparer` class as a comparer when sorting strings this way.
{% endhint %}

`OrderLogically()` and `OrderDescendLogically()`

```csharp
// Normal string arrays
public static string[] OrderLogically(this string[] source)
public static string[] OrderDescendLogically(this string[] source)

// IEnumerables
public static IEnumerable<string> OrderLogically(this IEnumerable<string> source)
public static IEnumerable<string> OrderDescendLogically(this IEnumerable<string> source)
```

This function simplifies the usage of the `LogicalComparer` class by wrapping it with the [`OrderBy()`](https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.orderby?view=net-8.0) and the [`OrderByDescending()`](https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.orderbydescending?view=net-8.0) functions.

### Case sensitive and insensitive comparison tools

These tools allow you to test strings for equality, prefixes, and suffixes in different ways.

#### `EqualsNoCase()`

```csharp
public static bool EqualsNoCase(this string source, string target, StringComparison comparison = StringComparison.OrdinalIgnoreCase)
```

This function allows you to test string equality easily without checking for case sensitivity.

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCultureIgnoreCase`
* `StringComparison.InvariantCultureIgnoreCase`
* `StringComparison.OrdinalIgnoreCase`
{% endhint %}

#### `EqualsCase()`

```csharp
public static bool EqualsCase(this string source, string target, StringComparison comparison = StringComparison.Ordinal)
```

This function allows you to test string equality easily while checking for case sensitivity.

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCulture`
* `StringComparison.InvariantCulture`
* `StringComparison.Ordinal`
{% endhint %}

#### `StartsWithNoCase()`

```csharp
public static bool StartsWithNoCase(this string source, string target, StringComparison comparison = StringComparison.OrdinalIgnoreCase))
```

This function allows you to test string prefix easily without checking for case sensitivity.

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCultureIgnoreCase`
* `StringComparison.InvariantCultureIgnoreCase`
* `StringComparison.OrdinalIgnoreCase`
{% endhint %}

#### `StartsWithCase()`

```csharp
public static bool StartsWithCase(this string source, string target, StringComparison comparison = StringComparison.Ordinal)
```

This function allows you to test string prefix easily while checking for case sensitivity.

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCulture`
* `StringComparison.InvariantCulture`
* `StringComparison.Ordinal`
{% endhint %}

#### `EndsWithNoCase()`

```csharp
public static bool EndsWithNoCase(this string source, string target, StringComparison comparison = StringComparison.OrdinalIgnoreCase))
```

This function allows you to test string suffix easily without checking for case sensitivity.

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCultureIgnoreCase`
* `StringComparison.InvariantCultureIgnoreCase`
* `StringComparison.OrdinalIgnoreCase`
{% endhint %}

#### `EndsWithCase()`

```csharp
public static bool EndsWithCase(this string source, string target, StringComparison comparison = StringComparison.Ordinal)
```

This function allows you to test string suffix easily while checking for case sensitivity.

{% hint style="info" %}
The comparison argument must be supplied with one of the following comparison options:

* `StringComparison.CurrentCulture`
* `StringComparison.InvariantCulture`
* `StringComparison.Ordinal`
{% endhint %}

#### `ContainsWithNoCase()`

```csharp
public static bool ContainsWithNoCase(this string source, string target)
```

This function allows you to check a substring without checking for case sensitivity.

### Wide character and string tools

The following functions allow you to perform operations with wide strings and characters on a string.

#### `GetWideChars()`

```csharp
public static WideChar[] GetWideChars(this string sentence)
```

This function allows you to get a list of wide characters that are found within a string. A wide character description can be found in [this page](../extra-features/wide-characters.md).

### Miscellaneous tools

The following functions allow you to perform even more operations on a string.

#### `ShiftLetters()`

```csharp
public static string ShiftLetters(this string text, int shift)
```

This function allows you to easily shift characters within a string by a number of character shifting steps that can be specified from `-255` to `255`.

* Shift `Hello` by `1`: `Ifmmp`
* Shift `Hello` by `-1`: `Gdkkn`

#### `TruncateString()`

```csharp
public static string TruncateString(this string target, int threshold)
```

This function allows you to truncate a string into a specified string length. This helps in situations where wrapping is not possible or the user needs a truncated string.

{% hint style="info" %}
This function also found in Terminaux, though they also employ VT sequence support to help process them. For console applications, it's better to use the [Terminaux](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-extensions) version.
{% endhint %}

#### `Reverse()`

```csharp
public static string Reverse(this string target)
```

This function allows you to easily reverse the order of characters in a string. For example, `Reversed` is `desreveR`.

#### `GetEnclosedWordFromIndex()`

```csharp
public static string GetEnclosedWordFromIndex(this string target, int sourceIdx, bool includeSymbols = false)
```

This function splits the string by spaces internally, then determines what word is from a specified source index. You can also include the symbols in the resultant enclosed word. Here are the following examples:

* Without symbols
  * `Hello world!` at index `2`: `Hello`
  * `Hello world!` at index `8`: `World`
* With symbols
  * `Hello world!` at index `2`: `Hello`
  * `Hello world!` at index `8`: `World!`

#### `GetIndexOfEnclosedWordFromIndex()`

```csharp
public static int GetIndexOfEnclosedWordFromIndex(this string target, int sourceIdx, bool includeSymbols = false)
```

This function splits the string by spaces internally, then determines what word is from a specified source index, and gets the index of its first character. You can also include the symbols in the resultant enclosed word. Here are the following examples:

* Without symbols
  * `!Hello world!` at index `2`: `1`
  * `Hello world!` at index `8`: `6`
* With symbols
  * `!Hello world!` at index `2`: `0`
  * `Hello world!` at index `8`: `6`

#### `ReadNullTerminatedString()`

```csharp
public static string ReadNullTerminatedString(this string source, int offset)
```

This function allows you to read a null-terminated string, optionally chopping the source string starting from `offset` index.

#### `IsPalindrome()`

```csharp
public static bool IsPalindrome(this string target, bool caseSensitive = false)
```

This function checks to see if a specified string is a palindrome or not. A string is considered to be a palindrome if the other half of the string is a mirror of the first half, such as `madam` or `noon`. Strings such as `Word` and `Laura` are not palindromes.

#### `ToStringBuilder()`

```csharp
public static StringBuilder ToStringBuilder(this string source)
```

This function allows you to easily get a string builder from a string to perform operations on a string without allocations.

#### `BreakSurrogates()`

```csharp
public static (char high, char low) BreakSurrogates(this string source)
```

This function allows you to break a string that consists of high surrogate and low surrogate characters into their individual character representations of the surrogates.

## Character manipulation

Character management tools can be found in the `CharManager` class under the `Textify.General` namespace. They make it easier for you to manipulate with individual characters.

### `NewLine`

```csharp
public static string NewLine
```

This property returns a new line that is returned by the [`Environment.NewLine`](https://learn.microsoft.com/en-us/dotnet/api/system.environment.newline?view=net-8.0) property. This changes depending on the operating system, such as `CR` + `LF` on Windows and `LF` on Unix systems.

### `GetAllAsciiChars()`

```csharp
public static char[] GetAllAsciiChars()
```

Gets all 256 ASCII characters. You can refer to the ASCII table [here](https://www.asciitable.com/).

### `GetAllChars()`

```csharp
public static char[] GetAllChars()
```

Gets all Unicode characters ranging from `\u0000` to `\uFFFF` in hexadecimal representation.

### `GetAllLettersAndNumbers()`

```csharp
public static char[] GetAllLettersAndNumbers(bool unicode = true)
```

Gets all letter and number characters. If `unicode` is set to true, it returns all letter and number characters found within Unicode. Otherwise, it uses the ASCII table to look up letters and numbers.

### `GetAllLetters()`

```csharp
public static char[] GetAllLetters(bool unicode = true)
```

Gets all letter characters. If `unicode` is set to true, it returns all letter characters found within Unicode. Otherwise, it uses the ASCII table to look up letters.

### `GetAllNumbers()`

```csharp
public static char[] GetAllNumbers(bool unicode = true)
```

Gets all number characters. If `unicode` is set to true, it returns all number characters found within Unicode. Otherwise, it uses the ASCII table to look up numbers.

### `GetAllDigitChars()`

```csharp
public static char[] GetAllDigitChars(bool unicode = true)
```

Gets all characters that represent a digit. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

### `GetAllControlChars()`

```csharp
public static char[] GetAllControlChars()
```

Gets all control characters from the whole Unicode table, such as escape character, bell character, and more.

### `GetAllRealControlChars()`

```csharp
public static char[] GetAllRealControlChars()
```

Gets all control characters from the whole Unicode table, such as escape character, bell character, and more.

### `GetAllSurrogateChars()`

```csharp
public static char[] GetAllSurrogateChars()
```

Gets all high and low surrogate characters from the whole Unicode table.

### `GetAllHighSurrogateChars()`

```csharp
public static char[] GetAllHighSurrogateChars()
```

Gets all high surrogate characters from the whole Unicode table.

### `GetAllLowSurrogateChars()`

```csharp
public static char[] GetAllLowSurrogateChars()
```

Gets all low surrogate characters from the whole Unicode table.

### `GetAllLowerChars()`

```csharp
public static char[] GetAllLowerChars(bool unicode = true)
```

Gets all lower case characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

### `GetAllUpperChars()`

```csharp
public static char[] GetAllUpperChars(bool unicode = true)
```

Gets all upper case characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

### `GetAllPunctuationChars()`

```csharp
public static char[] GetAllPunctuationChars(bool unicode = true)
```

Gets all punctuation characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

### `GetAllSeparatorChars()`

```csharp
public static char[] GetAllSeparatorChars(bool unicode = true)
```

Gets all separator characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

### `GetAllSymbolChars()`

```csharp
public static char[] GetAllSymbolChars(bool unicode = true)
```

Gets all symbol characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

### `GetAllWhitespaceChars()`

```csharp
public static char[] GetAllWhitespaceChars(bool unicode = true)
```

Gets all whitespace characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

### `GetEsc()`

```csharp
public static char GetEsc()
```

Gets an escape character. This function is a wrapper of the escape character, `\u001b`.

### `IsControlChar()`

```csharp
public static bool IsControlChar(char ch)
```

Checks whether the specified character is a real control character. This checks to see if the following conditions are true:

* The character is greater than the NULL character (`\u0000`) and less than the BACKSPACE character (`\u0008`)
* The character is greater than the CARRIAGE RETURN character (`\u000D`) and less than the SUBSTITUTE character (`\u001A`)

Mathematically, the algorithm that this function uses can be described as:

$$
f(c) =\begin{cases}1 & 0_{16} < c < 8_{16}\\1 & D_{16} < c < 1A_{16}\\0 & other\end{cases}
$$
