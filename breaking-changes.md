---
description: Changes that break the API
icon: newspaper
---

# Breaking changes

There are versions of Textify that may bring breaking changes with it. As a result, we'll have to list them to avoid being in the dark.

***

Textify 1.2.x contains the following breaking changes that you must do in order for your applications to continue working:

<details>

<summary>Textify.Online is moved to Nettify</summary>

The entire Textify.Online library, including getting your ISP information from your e-mail address, has been moved to a separate library, Nettify. You can consult its documentation by clicking on the below button:

<a href="https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/VAbPWc0zpDgwlfwTfz6I/" class="button primary">Open Nettify manual</a>

</details>

***

## <mark style="color:$primary;">Textify 1.2.x to 1.3.x</mark>

Textify 1.3.x contains the following breaking changes that you must do in order for your applications to continue working:

<details>

<summary>Split data to Textify.Data</summary>

We've split the unicode, the name, and the word data to a separate package that allows Textify to make use of this data without resorting to reflection, called Textify.Data. This reduced the main Textify library size significantly to reduce your download time when building projects that only use the main Textify functions without any data.

{% hint style="info" %}
Your applications will have to call `DataInitializer.Initialize()` before being able to use any of Unicode, Names, and Words.
{% endhint %}

</details>

<details>

<summary>Removed VT sequence classes</summary>

We have temporarily removed VT sequence classes from Textify while migrating these tools to Terminaux. The reason is that because Terminaux 3.0 needs to host these classes without resorting to make individual versions of Textify intended only to patch VT-related functions, should they contain a bug. The following functions are affected:

* `GetWrappedSentences()`
* `Truncate()`

</details>

***

## <mark style="color:$primary;">Textify 1.3.x to 1.5.x</mark>

Textify 1.5.x contains the following breaking changes that you must do in order for your applications to continue working:

<details>

<summary>Split JSON functions to Textify.Json</summary>

We've split JSON functions to `Textify.Json` as it forms a very small fraction of the main library. This is to ensure that the main library is scalable.

</details>

***

## <mark style="color:$primary;">Textify 1.5.x to 1.6.x</mark>

Textify 1.6.x contains the following breaking changes that you must do in order for your applications to continue working:

<details>

<summary>Split data-based functions to Textify.Data.Json</summary>

We've split data-based functions, such as words and names, to `Textify.Data.Json` to reduce the main library distribution and download size. This is to ensure that the main library users are able to use it without having to download 30+ MB of assets.

</details>

***

## <mark style="color:$primary;">Textify 1.6.x to 1.9.x</mark>

Textify 1.9.x contains the following breaking changes that you must do in order for your applications to continue working:

<details>

<summary>Moved Figletize to Textify.Figlet</summary>

As part of the migration effort, we've decided to migrate Figletize and its assets to the Textify.Figlet library that you can download from NuGet. Please note that when referencing this library, it'll automatically download Textify, too. This is required for the Figlet component to work. We've also re-licensed this part of code as GNU GPL 3.0 or Later.

</details>

***

## <mark style="color:$primary;">Textify 1.2.x to 2.0.x</mark>

Textify 2.0.x contains the following breaking changes that you must do in order for your applications to continue working:

<details>

<summary>Textify.Data.Analysis and Textify.Figlet merged to Textify.Data</summary>

We've moved all the code files from both the Textify.Data.Analysis and the Textify.Figlet package to the Textify.Data library in order to unify all data-related functions.

{% hint style="info" %}
Usually, you'll need to change the `using` clause to point to `Textify.Data`.
{% endhint %}

</details>

<details>

<summary>Textify.Json merged to Textify</summary>

We've moved all the code files from the Textify.Json library to the main Textify library.

{% hint style="info" %}
Usually, you'll need to change the `using` clause to point to `Textify`.
{% endhint %}

</details>
