---
description: Select a random word!
icon: pen
---

# Word Management

Word management is another feature of Textify that manages a list of words and generates a random set of words.

***

## <mark style="color:$primary;">Usage</mark>

You can use the `WordManager` class found in the `Textify.Data.Words` namespace.

<details>

<summary>Available functions</summary>

You can use the `WordManager` class that contains the following functions:

| Function                     | Description                          |
| ---------------------------- | ------------------------------------ |
| `InitializeWords()`          | Initializes the whole group of words |
| `GetWords()`                 | Gets a random set of words           |
| `GetRandomWord()`            | Gets a random word                   |
| `GetRandomWordConditional()` | Gets a random word conditionally     |

{% hint style="info" %}
The asynchronous version of the functions is provided for web applications and other apps that require async operations.
{% endhint %}

</details>

<details>

<summary>Available word flavors</summary>

You can also select one of the following flavors (`WordDataType`) of the word list:

| Flavor             | Description                                                            |
| ------------------ | ---------------------------------------------------------------------- |
| `Words`            | Word list                                                              |
| `WordsFull`        | Word list, including alphanumeric characters                           |
| `WordsDirty`       | Word list, including offensive words (18+)                             |
| `WordsDirtyFull`   | Word list, including offensive words (18+) and alphanumeric characters |
| `BadWords`         | Offensive words list (18+) for bad word filtering                      |
| `CommonWords`      | Common word list                                                       |
| `CommonWordsDirty` | Common word list, including offensive words (18+)                      |

{% hint style="info" %}
The last three word flavors contains offensive words that may not be suitable for users and developers, so it's best not to use them unless you have a reason to, such as swearing filters that Textify provides. Considering this point, we've decided to move the words list to its own flavor, `WordsDirty`, and clean all possible offensive words in the `Words` flavor.
{% endhint %}

</details>

***

## <mark style="color:$primary;">Profanity filter</mark>

Textify provides a profanity filter that lets you sanitize your sentences from any possible profanity. You can find it under the `ProfanityManager` class in the `Textify.Data.Words.Profanity` namespace.

<details>

<summary>Available functions</summary>

You can analyze and filter your sentence from profanities using these functions:

<table><thead><tr><th width="189.66668701171875">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>GetProfanities()</code></td><td>Gets all profanities found</td></tr><tr><td><code>FilterProfanities()</code></td><td>Filters all profanities found</td></tr></tbody></table>

</details>

<details>

<summary>Methods of analysis</summary>

The profanity filter can analyze your sentences in four ways:

<table><thead><tr><th width="109.6666259765625">Method</th><th>Description</th></tr></thead><tbody><tr><td><code>Thorough</code></td><td>Thorough searching. May not find swearing embedded in two or more words.</td></tr><tr><td><code>Shallow</code></td><td>Shallow searching. May not find swearing embedded in two or more words and/or separated by whitespace.</td></tr><tr><td><code>Mitigated</code></td><td>Mitigated partial searching. May not find swearing that has its characters separated by whitespace.</td></tr><tr><td><code>Partial</code></td><td>Partial searching. May cause legitimate words to be found, such as <a href="https://en.wikipedia.org/wiki/Scunthorpe_problem">Scunthorpe</a> (a <a href="https://en.wikipedia.org/wiki/Scunthorpe">town</a> in the UK) and <a href="https://web.archive.org/web/20200223093609/https://www.telegraph.co.uk/news/newstopics/howaboutthat/2667634/The-Clbuttic-Mistake-When-obscenity-filters-go-wrong.html">Classic</a>.</td></tr></tbody></table>

</details>
