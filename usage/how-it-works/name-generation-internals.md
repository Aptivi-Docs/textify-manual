---
description: How does it work?
---

# 👥 Name Generation Internals

When any of this feature's functions get called in your application, it first downloads the name list and installs the names and the surnames to the memory if it's the first time it's been run. Then, it uses the random number generator to select a random name and a random surname.

As soon as they're selected, it returns a list of full names satisfying your conditions, if any.
