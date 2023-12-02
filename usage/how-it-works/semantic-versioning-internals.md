---
description: How does it work?
---

# 🗓 Semantic Versioning Internals

When `SemVer.Parse()` or `SemVer.ParseWithRev()` gets called with a semantic version string, it first checks the string against the SemVer compliance using the following regular expression (fetched from [this](https://semver.org/)). If it doesn't find any version element, such as the case of `1.0-1`, it returns an error.

This is the regular expression used:

```regex
^(0|[1-9]\d*)\.(0|[1-9]\d*)\.(0|[1-9]\d*)(?:-((?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*)(?:\.(?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*))*))?(?:\+([0-9a-zA-Z-]+(?:\.[0-9a-zA-Z-]+)*))?$
```

If there's a match, the next step is to extract the following information:

* Major version (`MajorVersion`, `int`)
* Minor version (`MinorVersion`, `int`)
* Patch version (`PatchVersion`, `int`)
* Pre-Release info (`PreReleaseInfo`, `string`)
* Build metadata (`BuildMetadata`, `string`)

Finally, the parser creates a new class instance which holds all the parsed information.
