---
description: How does it work?
---

# 🖋 Word Selection Internals

When any of this feature's functions get called in your application, it first downloads the word list and installs the words to the memory if it's the first time it's been run. Then, it uses the random number generator to select a random word.

As soon as it's selected, it returns that word for your application to use.
