---
description: Select a random word!
---

# 🖊 Word Selection

{% hint style="info" %}
Your applications will have to call `DataInitializer.Initialize()` before being able to use any of Unicode, Names, and Words.
{% endhint %}

Using this function is very simple! Just use the `Textify.Words` namespace in any piece of code you want to use the function, as in: `using Textify.Words;`

The `WordManager` class contains the following functions (asynchronous functions are suffixed with the `Async` word):

* `InitializeWords()`
* `GetWords()`
* `GetRandomWord()`
* `GetRandomWordConditional()`

These functions call the `InitializeWords()` function to download the list of words and installs the list of words to the words list for the two above functions to use.

If the conditional version is used, you can specify the maximum length of the word, the prefix of the word, the postfix of the word, and the exact word length.
