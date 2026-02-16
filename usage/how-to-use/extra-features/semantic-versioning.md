---
description: One version is enough to identify how old this work is!
icon: calendar-range
---

# Semantic Versioning

Semantic versioning is another extra Textify feature that checks the stringified version to see if it is SemVer 2.0 compliant.

***

## <mark style="color:$primary;">Parsing semantic version string</mark>

To parse your semantic version string, for example, `1.0.0-alpha1` or `1.0.0.0-alpha1`, you must define a variable that has the type of `SemVer`. Then, call one of the following functions:

<table><thead><tr><th width="229.99993896484375">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>SemVer.Parse()</code></td><td>Parses either the full or the 3-component versions</td></tr><tr><td><code>SemVer.ParseWithoutRev()</code></td><td>Parses the 3-component version.</td></tr><tr><td><code>SemVer.ParseWithRev()</code></td><td>Parses the full version.</td></tr></tbody></table>

A simple example on how to get a `SemVer` instance from the version string is:

```csharp
SemVer semVer = SemVer.Parse(version);
```

Once the parser finishes parsing your semantic version string, it returns a `SemVer` class instance.

<details>

<summary>Version information class</summary>

A `SemVer` class instance contains the necessary information about your version:

| Property          | Description      |
| ----------------- | ---------------- |
| `MajorVersion`    | Major version    |
| `MinorVersion`    | Minor version    |
| `PatchVersion`    | Patch version    |
| `RevisionVersion` | Revision version |
| `PreReleaseInfo`  | Pre-Release info |
| `BuildMetadata`   | Build metadata   |

</details>

<details>

<summary>Version information equality operators</summary>

As for the equality operators, this class supports the following operators:

| Operator | Description                                                         |
| -------- | ------------------------------------------------------------------- |
| `==`     | Checks to see if both `SemVer` versions are equal.                  |
| `!=`     | Checks to see if both `SemVer` versions are opposite to each other. |
| `<`      | Checks to see if `a` is older than `b`.                             |
| `>`      | Checks to see if `a` is newer than `b`.                             |
| `<=`     | Checks to see if `a` is older or equal to `b`.                      |
| `>=`     | Checks to see if `a` is newer or equal to `b`.                      |

</details>
