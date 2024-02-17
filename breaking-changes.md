---
description: Changes that break the API
---

# 🗞 Breaking changes

There are versions of Textify that may bring breaking changes with it. As a result, we'll have to list them to avoid being in the dark.

## Textify 1.x

During the development of the entire Textify 1.x series, we've made the following breaking changes:

### Textify 1.0.x to 1.2.x

Textify 1.2.x contains the following breaking changes that you must do in order for your applications to continue working:

#### Textify.Online is moved to Nettify

The entire Textify.Online library, including getting your ISP information from your e-mail address, has been moved to a separate library, Nettify. You can consult its documentation here:

{% content-ref url="https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/VAbPWc0zpDgwlfwTfz6I/" %}
[Nettify - Manual](https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/VAbPWc0zpDgwlfwTfz6I/)
{% endcontent-ref %}

### Textify 1.2.x to 1.3.x

Textify 1.3.x contains the following breaking changes that you must do in order for your applications to continue working:

#### Split data to Textify.Data

We've split the unicode, the name, and the word data to a separate package that allows Textify to make use of this data without resorting to reflection, called Textify.Data. This reduced the main Textify library size significantly to reduce your download time when building projects that only use the main Textify functions without any data.

{% hint style="info" %}
Your applications will have to call `DataInitializer.Initialize()` before being able to use any of Unicode, Names, and Words.
{% endhint %}

#### Removed VT sequence classes

We have temporarily removed VT sequence classes from Textify while migrating these tools to Terminaux. The reason is that because Terminaux 3.0 needs to host these classes without resorting to make individual versions of Textify intended only to patch VT-related functions, should they contain a bug. The following functions are affected:

* `GetWrappedSentences()`
* `Truncate()`

{% hint style="info" %}
We promise that we'll bring these functions back, but without VT sequences. Should you make use of these functions with support for VT sequences, you have two options:

* Upgrade to Terminaux 3.0 and use its `ConsoleMisc` extension class.
* Downgrade to Textify 1.3.2 and Terminaux 2.7.2.
{% endhint %}
