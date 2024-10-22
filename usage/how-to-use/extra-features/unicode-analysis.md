---
description: Any special characters?
icon: square-u
---

# Unicode Analysis

Using this functionality that is available on Textify is very simple! Just use the `Textify.Unicode` namespace in any piece of code you want to use the library, as in: `using Textify.Data.Analysis.Unicode;`

Just use the `UnicodeQuery` class that contains:

* `QueryChar(char)`
* `QueryChar(int)`
* `QueryChar(char, UnicodeQueryType)`
* `QueryChar(int, UnicodeQueryType)`

You can control which database this feature uses using the `UnicodeQueryType` enumeration:

* Simple: Simple Unicode characters without the Unihan characters and their info
* Unihan: All Unihan Unicode characters with just the Unihan info
* Full: All characters with their Unihan info
