---
description: How does it work?
icon: square-u
---

# Unicode Analyzer Internals

When one of the `QueryChar` functions gets called, it first caches the Unicode database from the library resources to the memory. As the library resources consist of ZIP files fetched from the Unicode UCD database which can be get, they're unpacked into memory.

`QueryChar` then attempts to serialize the UCD XML file to the `Ucd` class, which contains these:

* `string Description`: the Unicode version
* `Repertoire Repertoire`: the master class for Unicode character list

This function then tries to get the character according to the character number from the `Repertoire` class instance.

Once it returns a `Char`, it allows you to access all the Unicode character database properties whose manual is [found here](https://www.unicode.org/reports/tr44/).
