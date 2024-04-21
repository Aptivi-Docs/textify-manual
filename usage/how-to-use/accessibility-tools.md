---
description: Accessibility tools for people with disabilities
---

# 👨‍🦽 Accessibility Tools

Textify not only provides all the common text tools, but it also provides the accessibility tools for people with disabilities. This ensures that applications become usable for such people. The following tools have been implemented:

* Braille conversion

The below sections explain the details of the above tools.

## Braille conversion

In the `BrailleBuilder` class, you can initiate the Braille text conversion. Currently, we only support text to Braille conversion. You can perform this conversion by calling the `ToBraille()` function, passing it the sentence of your choice. This uses the Braille map that Textify provides to let you convert text to Braille.

{% hint style="info" %}
Some elevators provide Braille number representations usually found at the bottom of the floor number in the buttons. For example, you may find `⠼⠙` under the number `4` that indicates the fourth floor.
{% endhint %}

Calling the above function is so simple! You can just call it like this:

```csharp
string braille = BrailleBuilder.ToBraille("Hello world!");
// braille = ⠓⠑⠇⠇⠕⠀⠺⠕⠗⠇⠙⠖
```

{% hint style="warning" %}
Make sure that you have a font that supports the Braille characters. For GUI apps, they should automatically use the Braille-supported typeface, depending on the operating system. For console applications, such as Nitrocid KS, you should use the monospaced font that supports the Braille typefaces, such as [Cascadia Code](https://github.com/microsoft/cascadia-code).
{% endhint %}

{% hint style="warning" %}
Currently, this converter supports a limited set of characters, so you may not be able to convert all characters using this function. We're working on it across several releases to enhance it.
{% endhint %}
