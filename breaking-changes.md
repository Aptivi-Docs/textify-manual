---
description: Changes that break the API
---

# 🗞️ Breaking changes

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
**We brought back these functions!**

~~We promise that we'll bring these functions back, but without VT sequences. Should you make use of these functions with support for VT sequences, you have two options:~~

* ~~Upgrade to Terminaux 3.0 and use its `ConsoleMisc` extension class.~~
* ~~Downgrade to Textify 1.3.2 and Terminaux 2.7.2.~~
{% endhint %}

### Textify 1.3.x to 1.5.x

Textify 1.5.x contains the following breaking changes that you must do in order for your applications to continue working:

#### Split JSON functions to Textify.Json

We've split JSON functions to `Textify.Json` as it forms a very small fraction of the main library. This is to ensure that the main library is scalable.

### Textify 1.5.x to 1.6.x

Textify 1.6.x contains the following breaking changes that you must do in order for your applications to continue working:

#### Split data-based functions to Textify.Data.Json

We've split data-based functions, such as words and names, to `Textify.Data.Json` to reduce the main library distribution and download size. This is to ensure that the main library users are able to use it without having to download 30+ MB of assets.

### Textify 1.6.x to 1.9.x

Textify 1.9.x contains the following breaking changes that you must do in order for your applications to continue working:

#### Moved Figletize to Textify.Figlet

As part of the migration effort, we've decided to migrate Figletize and its assets to the Textify.Figlet library that you can download from NuGet. Please note that when referencing this library, it'll automatically download Textify, too. This is required for the Figlet component to work. We've also re-licensed this part of code as GNU GPL 3.0 or Later.

## Textify 2.x

During the development of the entire Textify 2.x series, we've made the following breaking changes:

### Textify 1.2.x to 2.0.x

Textify 2.0.x contains the following breaking changes that you must do in order for your applications to continue working:

#### Textify.Data.Analysis and Textify.Figlet merged to Textify.Data

We've moved all the code files from both the Textify.Data.Analysis and the Textify.Figlet package to the Textify.Data library in order to unify all data-related functions.

{% hint style="info" %}
Usually, you'll need to change the `using` clause to point to `Textify.Data`.
{% endhint %}

#### Textify.Json merged to Textify

We've moved all the code files from the Textify.Json library to the main Textify library.

{% hint style="info" %}
Usually, you'll need to change the `using` clause to point to `Textify`.
{% endhint %}
