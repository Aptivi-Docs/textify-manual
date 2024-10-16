---
description: Manage your emoticons here.
icon: face-smile
---

# Emoji Management

Textify provides a tool for emoji management that allows you to obtain a full list of Unicode emojis according to the latest Unicode 16.0.0 standard taken from [this source](https://unicode.org/Public/emoji/16.0/). This tool allows you to analyze an emoji, get its sequence, its name, and other properties. Currently, the `Emoji` class instances can be get using one of the following functions from the `EmojiManager` class from `Textify.Data.Unicode`:

* `GetEmojis()`: Gets an array of all known Unicode emojis
* `GetEmojisFromName()`: Gets an array of emojis from a name
* `GetEmojiFromEmoji()`: Gets an emoji instance from an emoji sequence
* `GetEmojiFromEnum()`: Gets an emoji instance from an emoji enumeration value, `EmojiEnum`.

An `Emoji` class instance contains the following properties:

* `Name`: Name of an emoji according to the Unicode database.
* `Enum`: Automatically generated emoji enumeration.
* `Status`: Unicode status for a particular emoji.
  * `Component`: Emoji is a component (excluding Regional\_Indicators, ASCII, and non-Emoji.)
  * `FullyQualified`: Emoji is fully qualified
  * `MinimalQualified`: Emoji is minimally qualified
  * `NotQualified`: Emoji is not qualified
* `Sequence`: A string containing an actual emoji. This can be either one characters, two surrogate characters, or a sequence of characters that modify a base emoji using width joiners or something similar.
