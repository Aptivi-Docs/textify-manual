---
description: How does it work?
---

# 👑 Figlet Text Internals

Each time Textify.Figlet gets a Figlet font, if said font is already found in the list of cached fonts, it would return. Else, the font parser parses the font stream that contains the individual font properties, including the list of letters.

General specification about the `.flf` font files is available in the source code, and you can view it in the below link:

{% @github-files/github-code-block url="https://github.com/Aptivi/Textify/blob/main/assets/FigletSpecs/figfont.txt" %}

The font parser first looks for the header, which always starts with the `flf2a` in the first five bytes. After that, the string pool is created so that the parser parses the character and installs the final character to the new instance of the Figlet font.

It takes care of the character properties, such as kerning, smushing, and full width.
