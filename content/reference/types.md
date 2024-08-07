---
title: types
---
In a computer, all information is stored as numbers. The numbers themselves don't tell you anything about the data they represent, so you have to know what *type* of data a particular number is supposed to represent in order to interpret it.

### char (Single character)
A character is something like `a`, `5`, or `@`. They are letters, digits, punctuation, but also whitespace (e.g. space, tab, line-break) and some non-printing control characters.

Character *literals* are indicated with single quotes, like this:

```cs
char c = '&';
```

### string (Text)
Characters make up things like words and sentences, so you might want to string them together, hence, strings!

Strings are zero or more characters, and string literals are marked with double quotes, like this:

```cs
string name = "Barbara";
string empty = "";
```

If you are coming from Python, you might be used to using single and double quotes interchangeably; this is not the case in C#, and is a common source of errors at the beginning.

### int (Whole numbers)
Integers are whole numbers:

```cs
int i = 2;
int j = -7;
```

### float and double (Decimals)
Floating point numbers are stored in scientific notation, and can store a very large range of decimal numbers. For the most part, floats behave themselves fine, but there are some *weird* things that happen in certain circumstances (you will probably not encounter these). To minimise the weirdness, we often use *double precision floating point numbers*, or doubles, instead, which work in the same way but which double the number of digits that can be stored. This pushes the weirdness into a very small corner that you'll likely never encounter. Unless speed is a *massive* concern of yours, use doubles over floats.

The default type for handling decimals in C# is, for this reason, the double:

```cs
double pi = 3.14159;
```

If you wish to explicitly store a decimal number as a float, rather than a double, put an f at the end of the number, like this:

```cs
float length = 143.25f;
```

You will find that Unity uses floats almost exclusively, because speed *is* a major issue (there are a load of calculations that need to be performed dozens of times per second), but a little bit of inaccuracy is not a huge problem (if your health slips by a fraction of a point, or an object moves a whisker more or less than it is meant to).