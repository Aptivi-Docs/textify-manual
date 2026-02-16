---
description: Manage your emoticons here.
icon: face-smile
---

# Emoji Management

Textify provides a tool for emoji management that allows you to obtain a full list of Unicode emojis according to the latest Unicode 16.0.0 standard taken from [this source](https://unicode.org/Public/emoji/16.0/). This tool allows you to analyze an emoji, get its sequence, its name, and other properties.

***

## <mark style="color:$primary;">Usage</mark>

Currently, the `Emoji` class instances can be get using the `EmojiManager` class from `Textify.Data.Unicode`.

<details>

<summary>Available functions</summary>

You can use one of the following functions:

<table><thead><tr><th width="189.6666259765625">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>GetEmojis()</code></td><td>Gets an array of all known Unicode emojis</td></tr><tr><td><code>GetEmojisFromName()</code></td><td>Gets an array of emojis from a name</td></tr><tr><td><code>GetEmojiFromEmoji()</code></td><td>Gets an emoji instance from an emoji sequence</td></tr><tr><td><code>GetEmojiFromEnum()</code></td><td>Gets an emoji instance from an emoji enumeration value, <code>EmojiEnum</code>.</td></tr></tbody></table>

</details>

<details>

<summary>Emoji instance class properties</summary>

An `Emoji` class instance contains the following properties:

<table><thead><tr><th width="110.3333740234375">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>Name</code></td><td>Name of an emoji according to the Unicode database.</td></tr><tr><td><code>Enum</code></td><td>Automatically generated emoji enumeration.</td></tr><tr><td><code>Status</code></td><td>Unicode status for a particular emoji.</td></tr><tr><td><code>Sequence</code></td><td>A string containing an actual emoji. This can be either one character, two surrogate characters, or a sequence of characters that modify a base emoji using width joiners or something similar.</td></tr></tbody></table>

where `Status` can be one of the following values:

<table><thead><tr><th width="170.3333740234375">Value</th><th>Description</th></tr></thead><tbody><tr><td><code>Component</code></td><td>Emoji is a component (excluding Regional_Indicators, ASCII, and non-Emoji.)</td></tr><tr><td><code>FullyQualified</code></td><td>Emoji is fully qualified</td></tr><tr><td><code>MinimalQualified</code></td><td>Emoji is minimally qualified</td></tr><tr><td><code>NotQualified</code></td><td>Emoji is not qualified</td></tr></tbody></table>

</details>
