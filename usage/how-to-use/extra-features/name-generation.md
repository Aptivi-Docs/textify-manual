---
description: Get a random name!
icon: square-user
---

# Name Generation

Name generation is another extra Textify feature that allows you to randomly select a name and a surname.

***

## <mark style="color:$primary;">Usage</mark>

You can use the `NameGenerator` class found in the `Textify.Data.NameGen` namespace.

<details>

<summary>Available functions</summary>

You can use the `NameGenerator` class that contains:

| Function               | Description                                      |
| ---------------------- | ------------------------------------------------ |
| `PopulateNames()`      | Populates the names                              |
| `GenerateNames()`      | Generates random names based on conditions       |
| `GenerateFirstNames()` | Generates random first names based on conditions |
| `GenerateLastNames()`  | Generates random last names based on conditions  |
| `FindFirstNames()`     | Finds the first names                            |
| `FindLastNames()`      | Finds the last names                             |
| `GetAllFirstNames()`   | Gets all first names                             |
| `GetAllLastNames()`    | Gets all last names                              |

{% hint style="info" %}
The asynchronous version of the functions is provided for web applications and other apps that require async operations.
{% endhint %}

</details>

<details>

<summary>Available gender types</summary>

You can specify the name gender type using the `NameGenderType` enumeration that has the following values:

| Value            | Description                                 |
| ---------------- | ------------------------------------------- |
| `Unified`        | Uses the list of both male and female names |
| `Female`         | Uses the list of female names               |
| `Male`           | Uses the list of male names                 |
| `FemaleImplicit` | Uses the list of implicit female names      |
| `MaleImplicit`   | Uses the list of implicit male names        |
| `Natural`        | Uses the list of unified natural names      |

</details>

<details>

<summary>Conditional name generation</summary>

If the conditional version is used, you can specify the maximum amount of names, as well as supplying the name suffix and prefix and the surname suffix and prefix.

For example, if you called the generation function like this:

```csharp
var names = GenerateNames(5, "Th", "", "", "ey")
```

...it'll generate five full names that the first name starts with `Th` and that the surname ends with `ey`, for example:

```
Thomas Dawsey
Thalia Ermey
(...)
```

</details>
