---
description: We have extra features!
icon: square-plus
---

# Extra Features

Textify also provides extra features in order to make various operations, such as Unicode analysis, semantic versioning, and word management, easier than before. Some of these features are located in the main `Textify` library, and some others are located in the `Textify.Data` library. Click on a feature that you want to learn about in the sidebar to get information about one of these features.

The following features are available in `Textify.Data`:

{% content-ref url="name-generation.md" %}
[name-generation.md](name-generation.md)
{% endcontent-ref %}

{% content-ref url="unicode-analysis.md" %}
[unicode-analysis.md](unicode-analysis.md)
{% endcontent-ref %}

{% content-ref url="word-management.md" %}
[word-management.md](word-management.md)
{% endcontent-ref %}

{% content-ref url="figlet-text.md" %}
[figlet-text.md](figlet-text.md)
{% endcontent-ref %}

{% content-ref url="emoji-management.md" %}
[emoji-management.md](emoji-management.md)
{% endcontent-ref %}

The following features are available in the base Textify library:

{% content-ref url="space-analysis-and-correction.md" %}
[space-analysis-and-correction.md](space-analysis-and-correction.md)
{% endcontent-ref %}

{% content-ref url="semantic-versioning.md" %}
[semantic-versioning.md](semantic-versioning.md)
{% endcontent-ref %}

{% content-ref url="accessibility-tools.md" %}
[accessibility-tools.md](accessibility-tools.md)
{% endcontent-ref %}

{% content-ref url="wide-characters.md" %}
[wide-characters.md](wide-characters.md)
{% endcontent-ref %}

## Unicode character width

For applications that need to deal with the Unicode character width as in console cells, we've introduced this fine feature from Terminaux that allows you to query a Unicode character for its width, such as modifier characters that take up zero console cells (i.e. zero width characters), English letters that take up one cell (i.e. half-width characters), and Chinese characters that take up two cells (i.e. full-width characters).

{% hint style="info" %}
Please note that this information doesn't indicate the string length either by the amount of UTF-8 characters or by the text element as `StringInfo` class returns. This indicates how many console grid cells a character or a sentence consumes. For example, when an application tries to get the string length that contains zero-width or full-width characters, it doesn't indicate the number of cells, but the number of absolute characters, so Chinese characters are considered as one character that takes up two cells and Arabic modifier characters are considered as one character that takes up zero cells. If you want to measure the correct string length as how it would show up on a console, you should use this feature. The easiest way to use it is to rely on Terminaux's character extensions.
{% endhint %}
