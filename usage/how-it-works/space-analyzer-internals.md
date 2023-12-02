---
description: How does it work?
---

# ☑ Space Analyzer Internals

Textify's space analyzer works by treating the string as if it's a stream to ensure greater efficiency for large strings. It also uses streams to handle large files.

### Analysis

When a caller invokes one of the `AnalyzeSpaces()` functions, it does the following:

* If `AnalyzeSpaces()` is called, it converts the string to a `MemoryStream`, which is later fed to `AnalyzeSpacesFrom()`.
* If `AnalyzeSpacesFrom(string pathToFile)` is called, it opens a file to feed its stream to `AnalyzeSpacesFrom()`.
* If `AnalyzeSpacesFrom(Stream stream)` is called, it does checks on the source stream to check to see if it can read and seek.

After that, these functions return a `SpaceAnalysisResult` instance by making a new instance of it using a constructor that takes a stream. This constructor seeks through the entire stream to process a byte and compare it to a list of bad spaces pattern.

If there are any bad spaces, it will continue reading bytes until there is exactly one bad space, which is further processed by skipping all the bytes that may have left over until it goes to the next character that isn't part of this bad space sequence. Then, it'll add this bad space to the list of found bad spaces.

### Conversion

When a caller invokes one of the `ConvertSpaces()` functions with the analysis result as the first parameter, it does the following:

* If `ConvertSpaces()` is called, it does the same seeking procedure as the analysis, but, this time, adding a normal space to the resulting byte list.
* If `ConvertSpacesToString()` is called, `ConvertSpaces()` takes responsibility of returning a resulting byte array. After that, it gets converted to a string using the UTF8 decoder.
* If `ConvertSpacesTo(string pathToFile)` is called, it writes the resulting string to the target file.
* If `ConvertSpacesTo(Stream stream)` is called, it writes the resulting bytes to the stream.
