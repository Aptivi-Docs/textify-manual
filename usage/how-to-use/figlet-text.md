---
description: Figlet text makes your text look more awesome!
---

# 👑 Figlet Text

As part of Textify's Figlet library, you can write figlet text using one of the 550+ fonts provided with the library!

## How do you write Figlet text to the console?

This feature is easy to use. Just call the `Console.WriteLine()` function with `FigletTools.RenderFiglet()`, passing the text and the figlet font name (case sensitive):

```csharp
string figletText = FigletTools.RenderFiglet("Hello!", "banner");
Console.WriteLine(figletText);
```

Additionally, you can get the Figlet font instance using one of the following `FigletFonts` functions, passing the font name (lowercase) to the first argument:

* `GetByName()`
* `TryGetByName()`

After you get the instance, you can call the `Render()` function on it, passing the text as the first argument.

```csharp
var fontInstance = FigletizeFonts.TryGetByName(fontName);
if (fontInstance is null)
{
    Console.Error.WriteLine($"Font {fontName} not found. Exiting...");
    return;
}
string rendered = fontInstance.Render(message);
Console.WriteLine(rendered);
```

### Other ways

Additionally, you can use the `FigletTools` class to get a list of supported Figlet fonts and their instances using the `GetFigletFonts()` function.

`GetFigletFont()` also does the same as `GetByName()`, except that it uses the fallback font, `small`, when the font is not found.
