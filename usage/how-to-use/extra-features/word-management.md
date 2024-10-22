---
description: Select a random word!
icon: pen
---

# Word Management

Using this function is very simple! Just use the `Textify.Words` namespace in any piece of code you want to use the function, as in: `using Textify.Data.Analysis.Words;`

The `WordManager` class contains the following functions (asynchronous functions are suffixed with the `Async` word):

* `InitializeWords()`
* `GetWords()`
* `GetRandomWord()`
* `GetRandomWordConditional()`

These functions call the `InitializeWords()` function to download the list of words and installs the list of words to the words list for the two above functions to use.

If the conditional version is used, you can specify the maximum length of the word, the prefix of the word, the postfix of the word, and the exact word length.

You can also select one of the following flavors of the word list:

* `Words`
* `WordsFull`
* `WordsDirty`
* `WordsDirtyFull`
* `BadWords`
* `CommonWords`
* `CommonWordsDirty`

{% hint style="info" %}
The last three word flavors contains offensive words that may not be suitable for users and developers, so it's best not to use them unless you have a reason to, such as swearing filters that Textify provides. Considering this point, we've decided to move the words list to its own flavor, `WordsDirty`, and clean all possible offensive words in the `Words` flavor.
{% endhint %}

## Swearing filter

Textify provides a swearing filter that lets you sanitize your sentences from any possible profanity. You can find it under the `ProfanityManager` class in the `Textify.Data.Analysis.Words.Profanity` namespace.

The profanity filter can analyze your sentences in four ways:

* Thorough
* Shallow
* Mitigated
* Partial

However, every search type has its downs. For instance, shallow and thorough searches may not find swearing words that are embedded in two or more words, while shallow and mitigated searches may not find swearing words that have its characters separated by whitespace. In addition, the partial search type may return false positives for completely legitimate words, such as [Scunthorpe](https://en.wikipedia.org/wiki/Scunthorpe\_problem) (a [town](https://en.wikipedia.org/wiki/Scunthorpe) in the UK) and [Classic](https://web.archive.org/web/20200223093609/https://www.telegraph.co.uk/news/newstopics/howaboutthat/2667634/The-Clbuttic-Mistake-When-obscenity-filters-go-wrong.html).

You can analyze and filter your sentence from profanities using these functions:

* `GetProfanities()`
* `FilterProfanities()`
