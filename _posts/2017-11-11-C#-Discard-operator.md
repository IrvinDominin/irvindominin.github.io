---
layout: post
title: C# - Discard operator
category: Dev
tags: [C#, .NET]
image: https://irvindominin.github.io/images/CS7/C7.0.png
excerpt: "Often, we want to ignore values returned from a method, for example out arguments..."
---

Often, we want to ignore values returned from a method, a typical example is to check if a string can be parsed to another type, for example a bool:

```csharp
bool myStringIsABool;
if (bool.TryParse("false", out myStringIsABool)) { /* Rest of the code */ }
```
Often, we want to ignore myStringIsABool and we also want to make this variable inaccessible, because is not relevant in the current context and we don't want it.

C# 7.0 offer a feature called discards, which can be used to achieve this.

<h2>Discards</h2>
Discards are local variables which you can assign, but cannot read from, we can consider them as "write-only" local variables. They don’t have names, instead, they are represented with a specific simble, the _ (underscore). 
The symbol _ is a contextual keyword, with some limitations:
 - is very similar to var
 - it cannot be read, and can't appear on the right side of an assignment

If we try to use the discard to the previous code, it will be:
```csharp
if (bool.TryParse("false", out bool _)) { /* Rest of the code */ }
```
Because _ is unreadable, we can't use its value to assign other variables, it will not appear in IntelliSense and if we try to use it the code will not compile.

<img class="alignnone size-full wp-image-114" src="/images/CS7/Discard_Usage_1.png.png" alt="Discard_Usage_1.png" width="819" height="521" />

<h2>Conclusion</h2>
The discards it is a designer feature, the local variable still be required at runtime and the compiler also generate a name for it. This feature is compatible with previous versions of .NET platforms as it does not require a CLR change.