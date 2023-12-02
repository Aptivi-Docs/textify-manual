---
description: How does it work?
---

# 📚 English Dictionary Internals

This function first downloads the word information from the dictionary API if it's not cached yet. If the word is cached, it'll return the cached `DictionaryWord` instance in an array.

However, if it's the first time using the word, it attempts to serialize the result into a `DictionaryWord` array that contains necessary information.

A `DictionaryWord` contains the following properties:

* `string Word`
  * The actual word
* `string PhoneticWord`
  * The base phonetic representation of the word
* `List<Phonetic> Phonetics`
  * The alternative phonetic representations
* `List<Meaning> Meanings`
  * Word meanings
* `License LicenseInfo`
  * License information
* `List<string> SourceUrls`
  * List of where we got the word information from

A `Phonetic` class contains the following properties:

* `string Text`
  * Phonetic representation of the word
* `string Audio`
  * Link to the pronounciation, usually in MP3 format. Use [NAudio (Windows)](https://github.com/naudio/NAudio) to play it.
* `string SourceUrl`
  * From where did we get the audio from?
* `License License`
  * License information for the source

A `Meaning` class contains the following properties:

* `string PartOfSpeech`
  * Part of speech, usually noun, verb, adjective, adverb, interjection, etc.
* `List<DefinitionType> Definitions`
  * List of word definitions. Words usually come with one or more definitions.
* `List<string> Synonyms`
  * List of synonyms based on the word meaning
* `List<string> Antonyms`
  * List of antonyms based on the word meaning

A `DefinitionType` class contains the following properties:

* `string Definition`
  * Word definition
* `List<string> Synonyms`
  * List of synonyms based on the definition
* `List<object> Antonyms`
  * List of antonyms based on the definition
* `string Example`
  * Example in sentence

A `License` class contains the following properties:

* `string Name`
  * License name
* `string Url`
  * License URL

{% hint style="warning" %}
You should be showing the license information somewhere in your program, usually in the About section, using the License class found within the dictionary word instance.
{% endhint %}
