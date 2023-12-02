---
description: Analyzing spaces in your text...
---

# ✅ Space Analysis and Correction

Textify provides two essential tools:

* Analyzing a string, a file, or a stream for abnormal spaces
* Converting occurrences of abnormal spaces to normal ones

### Analysis

The analysis tools are found under the `SpaceAnalysisTools` class to provide you with the analysis results about abnormal spaces, like non-breaking spaces in the middle of the text, or zero-width spaces in the URLs for malicious intentions, such as phishing.

This class currently provides the following tools:

```csharp
public static SpaceAnalysisResult AnalyzeSpaces(string text)
public static SpaceAnalysisResult AnalyzeSpacesFrom(string pathToFile)
public static SpaceAnalysisResult AnalyzeSpacesFrom(Stream stream)
```

It supports analyzing the spaces either from the provided string, the path to a file containing abnormal spaces, or the stream that holds the data containing such spaces. When analysis is complete, `SpaceAnalysisResult` provides the following values:

* `ResultingStream`
  * This provides a stream resulting from the analysis functions.
* `FalseSpaces`
  * This provides an array of tuples containing a false space character as the first item and the character name as the second item.

{% hint style="warning" %}
The stream that you're going to use should be readable and seekable, or SpaceMan will complain about it by throwing an exception to the caller.
{% endhint %}

### Conversion

The other part of SpaceMan is conversion, which lets you convert all the abnormal spaces found to normal spaces. `SpaceConversionTools` plays a role in this area, which makes it an important part of the library.

The class currently provides the following tools:

```csharp
public static byte[] ConvertSpaces(SpaceAnalysisResult analysisResult)
public static string ConvertSpacesToString(SpaceAnalysisResult analysisResult)
public static void ConvertSpacesTo(SpaceAnalysisResult analysisResult, string pathToFile)
public static void ConvertSpacesTo(SpaceAnalysisResult analysisResult, Stream stream)
```

It requires running one of the analysis functions found at the top of this page. `ConvertSpaces()` returns an array of resulting bytes for further operation, like sending an array of bytes to a serial device. Alternatively, `ConvertSpacesToString()` offers to give you a result as a string.

`ConvertSpacesTo()` provides you with two versions of this function; the one that writes to a file, and another that writes to a stream.

{% hint style="warning" %}
The resulting stream that `ConvertSpacesTo()` writes to must be writable, or SpaceMan will complain about it by throwing an exception to the caller.
{% endhint %}
