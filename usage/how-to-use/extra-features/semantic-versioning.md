---
description: One version is enough to identify how old this work is!
icon: calendar-range
---

# Semantic Versioning

Using this function is very simple! Just use the `Textify.Versioning` namespace in any piece of code you want to use the function, as in: `using Textify.Versioning;`

To parse your semantic version string, for example, `1.0.0-alpha1` or `1.0.0.0-alpha1`, you must define a variable that has the type of `SemVer`. Assign a variable so that it calls the `SemVer.Parse()`, `SemVer.ParseWithoutRev()`, or the `SemVer.ParseWithRev()` version, passing it your version string, like this:

```csharp
SemVer semVer = SemVer.Parse(version);
```

* Use `Parse()` if you want to be able to parse either the full or the 3-component versions.
* Use `ParseWithoutRev()` if you want to only parse the 3-component versions.
* Use `ParseWithRev()` if you want to only parse the full versions.

Once the parser finishes parsing your semantic version string, it returns a class contains necessary information about your version:

* Major version (`MajorVersion`, `int`)
* Minor version (`MinorVersion`, `int`)
* Patch version (`PatchVersion`, `int`)
* Revision version (`RevisionVersion`, `int`)
* Pre-Release info (`PreReleaseInfo`, `string`)
* Build metadata (`BuildMetadata`, `string`)

As for the equality operators, this class supports the following operators (assuming that `SemVer a` has version `1.0.0` and `SemVer b` has version `1.0.1`):

* `==`: Checks to see if both `SemVer` versions are equal.
* `!=`: Checks to see if both `SemVer` versions are opposite to each other.
* `<`: Checks to see if `a` is older than `b`
* `>`: Checks to see if `a` is newer than `b`
* `<=`: Checks to see if `a` is older or equal to `b`
* `>=`: Checks to see if `a` is newer or equal to `b`
