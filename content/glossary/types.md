---
title: types
---

Kind of information|Name|Main type|Other types
---|---|---|---
whole numbers|integer|int|uint, sbyte, byte, short, ushort, long, ulong
decimals in scientific notation|floating point number|double|float
true/false|boolean|bool|
text|string|string|
individual letters, digits|character|char|

{{< toc >}}

# Boolean
## `bool`

# Integer
Integers are whole numbers: positive, negative or zero. When you declare an integer you need to tell the computer how much space (how many digits) you need. On most modern systems, the default kind of integer (usually called `int`) is a *32-bit signed* integer, which can store numbers between `-2,147,483,648` and `2,147,483,647`. Unless you have a good reason to choose differently, this is usually the best bet.

type|length|signed|range
---:|-----:|-----:|-----
sbyte|8 bits|y|`-128` to `127`
byte|8 bits|n|`0` to `255`
short|16 bits|y|`-32,678` to `32,767`
ushort|16 bits|n|`0` to `65,535`
int|32 bits|y|`-2,147,483,648` to `2,147,483,647`
uint|32 bits|n|`0` to `4,294,967,295`
long|64 bits|n|`-9,223,372,036,854,775,808` to `9,223,372,036,854,775,807`
ulong|64 bits|n|`0` to `18,446,744,073,709,551,615`
char|16 bits|n|`0` to `65,535`

# Floating point
Non-integer numbers in computers are usually stored as floating-point numbers, which are essentially numbers in scientific notation.

{{< katex display >}}
mantissa x 2^{exponent}
{{< /katex >}}
# Text