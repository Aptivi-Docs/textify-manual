---
description: Tools that manipulate with characters
icon: a
---

# Character Manipulation

Character management tools can be found in the `CharManager` class under the `Textify.General` namespace. They make it easier for you to manipulate with individual characters.

<details>

<summary><code>NewLine</code></summary>

```csharp
public static string NewLine
```

This property returns a new line that is returned by the [`Environment.NewLine`](https://learn.microsoft.com/en-us/dotnet/api/system.environment.newline?view=net-8.0) property. This changes depending on the operating system, such as `CR` + `LF` on Windows and `LF` on Unix systems.

</details>

<details>

<summary><code>GetAllAsciiChars()</code></summary>

```csharp
public static char[] GetAllAsciiChars() { }
```

Gets all 256 ASCII characters. You can refer to the ASCII table [here](https://www.asciitable.com/).

</details>

<details>

<summary><code>GetAllChars()</code></summary>

```csharp
public static char[] GetAllChars() { }
```

Gets all Unicode characters ranging from `\u0000` to `\uFFFF` in hexadecimal representation.

</details>

<details>

<summary><code>GetAllLettersAndNumbers()</code></summary>

```csharp
public static char[] GetAllLettersAndNumbers(bool unicode = true) { }
```

Gets all letter and number characters. If `unicode` is set to true, it returns all letter and number characters found within Unicode. Otherwise, it uses the ASCII table to look up letters and numbers.

</details>

<details>

<summary><code>GetAllLetters()</code></summary>

```csharp
public static char[] GetAllLetters(bool unicode = true) { }
```

Gets all letter characters. If `unicode` is set to true, it returns all letter characters found within Unicode. Otherwise, it uses the ASCII table to look up letters.

</details>

<details>

<summary><code>GetAllNumbers()</code></summary>

```csharp
public static char[] GetAllNumbers(bool unicode = true) { }
```

Gets all number characters. If `unicode` is set to true, it returns all number characters found within Unicode. Otherwise, it uses the ASCII table to look up numbers.

</details>

<details>

<summary><code>GetAllDigitChars()</code></summary>

```csharp
public static char[] GetAllDigitChars(bool unicode = true) { }
```

Gets all characters that represent a digit. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

</details>

<details>

<summary><code>GetAllControlChars()</code></summary>

```csharp
public static char[] GetAllControlChars() { }
```

Gets all control characters from the whole Unicode table, such as escape character, bell character, and more.

</details>

<details>

<summary><code>GetAllRealControlChars()</code></summary>

```csharp
public static char[] GetAllRealControlChars() { }
```

Gets all control characters from the whole Unicode table, such as escape character, bell character, and more.

</details>

<details>

<summary><code>GetAllSurrogateChars()</code></summary>

```csharp
public static char[] GetAllSurrogateChars() { }
```

Gets all high and low surrogate characters from the whole Unicode table.

</details>

<details>

<summary><code>GetAllHighSurrogateChars()</code></summary>

```csharp
public static char[] GetAllHighSurrogateChars() { }
```

Gets all high surrogate characters from the whole Unicode table.

</details>

<details>

<summary><code>GetAllLowSurrogateChars()</code></summary>

```csharp
public static char[] GetAllLowSurrogateChars() { }
```

Gets all low surrogate characters from the whole Unicode table.

</details>

<details>

<summary><code>GetAllLowerChars()</code></summary>

```csharp
public static char[] GetAllLowerChars(bool unicode = true) { }
```

Gets all lower case characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

</details>

<details>

<summary><code>GetAllUpperChars()</code></summary>

```csharp
public static char[] GetAllUpperChars(bool unicode = true) { }
```

Gets all upper case characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

</details>

<details>

<summary><code>GetAllPunctuationChars()</code></summary>

```csharp
public static char[] GetAllPunctuationChars(bool unicode = true) { }
```

Gets all punctuation characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

</details>

<details>

<summary><code>GetAllSeparatorChars()</code></summary>

```csharp
public static char[] GetAllSeparatorChars(bool unicode = true) { }
```

Gets all separator characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

</details>

<details>

<summary><code>GetAllSymbolChars()</code></summary>

```csharp
public static char[] GetAllSymbolChars(bool unicode = true) { }
```

Gets all symbol characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

</details>

<details>

<summary><code>GetAllWhitespaceChars()</code></summary>

```csharp
public static char[] GetAllWhitespaceChars(bool unicode = true) { }
```

Gets all whitespace characters. If `unicode` is set to true, it returns all such characters found within Unicode. Otherwise, it uses the ASCII table to look up such characters.

</details>

<details>

<summary><code>GetEsc()</code></summary>

```csharp
public static char GetEsc() { }
```

Gets an escape character. This function is a wrapper of the escape character, `\u001b`.

</details>

<details>

<summary><code>IsControlChar()</code></summary>

```csharp
public static bool IsControlChar(char ch) { }
```

Checks whether the specified character is a real control character. This checks to see if the following conditions are true:

* The character is greater than the NULL character (`\u0000`) and less than the BACKSPACE character (`\u0008`)
* The character is greater than the CARRIAGE RETURN character (`\u000D`) and less than the SUBSTITUTE character (`\u001A`)

Mathematically, the algorithm that this function uses can be described as:

<p align="center"><span class="math">f(c) =\begin{cases}1 &#x26; 0_{16} &#x3C; c &#x3C; 8_{16}\\1 &#x26; D_{16} &#x3C; c &#x3C; 1A_{16}\\0 &#x26; other\end{cases}</span></p>

</details>
