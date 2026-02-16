---
description: Figlet text makes your text look more awesome!
icon: crown
---

# Figlet Text

As part of the main Textify library, you can write figlet text using one of the 550+ fonts provided with the library!

***

## <mark style="color:$primary;">Usage</mark>

You can use the Figlet tools using the `FigletTools` class in the `Textify.Data.Figlet` namespace.

<details>

<summary>Available functions</summary>

You can use one of the following functions:

<table><thead><tr><th width="170.333251953125">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>GetByName()</code></td><td>Gets a Figlet font instance from name</td></tr><tr><td><code>TryGetByName()</code></td><td>Tries to get the Figlet font instance from name</td></tr><tr><td><code>GetFigletFonts()</code></td><td>Gets a list of supported Figlet fonts and their instances</td></tr><tr><td><code>GetFigletFont()</code></td><td>Gets a Figlet font instance from name but with fallback to <code>small</code> if the font is not found</td></tr></tbody></table>

</details>

<details>

<summary>Example of printing Figlet text to the console using <code>FigletTools</code></summary>

This feature is easy to use. Just call the `Console.WriteLine()` function with `FigletTools.RenderFiglet()`, passing the text and the figlet font name (case sensitive):

```csharp
string figletText = FigletTools.RenderFiglet("Hello!", "banner");
Console.WriteLine(figletText);
```

</details>

<details>

<summary>Example of printing Figlet text to the console using the font instance</summary>

You can get the Figlet font instance using a function that we've mentioned earlier.

After you get the instance, you can call the `Render()` function on it, passing the text as the first argument.

```csharp
var fontInstance = FigletTools.TryGetByName(fontName);
if (fontInstance is null)
{
    Console.Error.WriteLine($"Font {fontName} not found. Exiting...");
    return;
}
string rendered = fontInstance.Render(message);
Console.WriteLine(rendered);
```

</details>
