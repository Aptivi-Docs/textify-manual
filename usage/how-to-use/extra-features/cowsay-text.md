---
description: Make the cows say something!
icon: comment-lines
---

# Cowsay Text

Textify also provides you with Cowsay that lets you write any text and make the cow (or any other entity) speak or think about your text.

***

## <mark style="color:$primary;">Usage</mark>

You can get started with creating an instance of a cow then make it either speak or think about a text. For more advanced usage, you can use the `Textify.Data.Cowsay` namespace and use the classes there.

<details>

<summary>Example of creating a cowsay text (default cow, speak)</summary>

{% code expandable="true" %}
```csharp
ICow cowsay = DefaultCattleFarmer.RearCowWithDefaults("default").Result;
string spoken = cowsay.Speak("Hello world! Mooooo!");
```
{% endcode %}

{% code expandable="true" %}
```
 ______________________ 
< Hello world! Mooooo! >
 ---------------------- 
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```
{% endcode %}

</details>

<details>

<summary>Example of creating a cowsay text (custom cow, speak)</summary>

{% code expandable="true" %}
```csharp
ICow cowsay = DefaultCattleFarmer.RearCowWithDefaults("robot").Result;
string spoken = cowsay.Speak("Beep... boop...");
```
{% endcode %}

{% code expandable="true" %}
```
 _________________ 
< Beep... boop... >
 ----------------- 
  \
   \

     [-]
     (+)=C
     | |
     OOO
```
{% endcode %}

</details>

<details>

<summary>Example of creating a cowsay text (default cow, think)</summary>

{% code expandable="true" %}
```csharp
ICow cowsay = DefaultCattleFarmer.RearCowWithDefaults("default").Result;
string spoken = cowsay.Think("Hello world! Mooooo!");
```
{% endcode %}

{% code expandable="true" %}
```
 ______________________ 
( Hello world! Mooooo! )
 ---------------------- 
        o   ^__^
         o  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```
{% endcode %}

</details>

<details>

<summary>Example of creating a cowsay text (custom cow, think)</summary>

{% code expandable="true" %}
```csharp
ICow cowsay = DefaultCattleFarmer.RearCowWithDefaults("robot").Result;
string spoken = cowsay.Think("Hello world! Mooooo!");
```
{% endcode %}

{% code expandable="true" %}
```
 _________________ 
( Beep... boop... )
 ----------------- 
  o
   o

     [-]
     (+)=C
     | |
     OOO
```
{% endcode %}

</details>
