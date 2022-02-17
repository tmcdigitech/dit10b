---
title: Strings
---
*adapted from [Medium.com](https://medium.com/analytics-vidhya/interesting-cool-python-tricks-for-working-with-strings-d37fcf8842b2)*

Let us see the different operations that can be performed on the below string.
```python
word = 'Sample'
len(word)
# 6
```
---
```python
 +---+---+---+---+---+---+
 | S | a | m | p | l | e |
 +---+---+---+---+---+---+
 0   1   2   3   4   5   6
-6  -5  -4  -3  -2  -1
```

### 1 Concatenation
Join a string with another string
```python
word = 'Sample'
word + ' ' + 'trick'
# 'Sample trick'
```

### 2 Indexed Access of Strings
A string in a python can be indexed to perform operations on the string.

Positive single character
```python
word = 'Sample'
word[3]
# 'p'
```

Negative single character
```python
word = 'Sample'
word[-2]
# 'l'
```

String Reverse
```python
word = 'Sample'
word[::-1]
# 'elpmaS'
```

Reverse string by iterating through string contents.
```python
word = 'Sample'
for char in reversed(word):    
    print(char)

### Output ###
e
l
p
m
a
S
```

### 3 Slicing of Strings
Slicing allows us to access a substring of characters from a word.
```python
Example 1
word = 'Sample'
word[0:3]
# 'Sam'
```
---
```python
Example 2
word = 'Sample'
word[4:5]
# 'le'
```
---
```python
Example 3
word = 'Sample'
word[:5]
# 'Sampl'
```

### 4 Remove leading and trailing characters
To remove space before and after a string the strip() method can be used has shown below
```python
'   Sample   '.strip()
# 'Sample'
'sample'.strip('ple')
# 'sam'
```

### 5 Left fill with ASCII ‘0’
To left fill with ASCII ‘0’’, we can use zfill() method to make a length of required string width.
```python
"10".zfill(6)
# '000010'
"-10".zfill(6)
# '-00010'
```
### 6 Find Substring
The find() method can be used to extract a substring from a string
```python
'sample'.find('am',0,5)
# '1'
'sam' in 'sample'
# True
```

### 7 Find if the string contains Numbers
The isalpha() method can be used to find if a string contains number
```python
'123'.isalpha()
# False
'abc'.isalpha()
# True
'1abc'.isalpha()
# False
```

### 8 Find if the string is alphanumeric
The isalnum() method can be used to find if the string contains alphanumeric and at least one character
```python
' '.isalnum()
# False
'abc'.isalnum()
# True
```

### 9 Find if the string is having only whitespace
The isspace() method can be used to determine if the string is only whitespace character
```python
' '.isspace()
# True
'Sample  '.isspace()
# False
```

### 10 Remove Spaces on the left side of the string
The lstrip() Strings
can be used to remove whitespace characters on the left.
```python
'   sample   '.lstrip()
# 'spacious   '
'www.example.com'.lstrip('cmowz.')
# 'example.com'
```

### 11 Remove Spaces on the right side of the string
The rstrip() can be used to remove whitespace characters on the left.
```python
'   sample   '.rstrip()
# 'spacious   '
'mississippi'.rstrip('ipz')
# 'mississ'
```

### 12 Formatted String Literals
The string literals which are prefixed with ‘f’ or ’F’ are called f-string.
```python
word = "Sample"
f"THis is a {word!r} string."
# "THis is a 'Sample' string."
```

### 13 Joining multiple strings from a list
The join() method can be used to join the strings in a list
```python
Test = ["This","is","Sample"]
print(" ".join(Test))
# This is Sample
```

### 14 Repeat string multiple times
Same like nos the strings can be multiplied to generate multiple string
```python
word = "Sample"
print(word*3)
# SampleSampleSample
```

### 15 Search for multiple prefixes in a string
The startswith() and endswith() method can be passed with multiple patterns of substrings to check if it is present.
```python
"sample".startswith(("sam","Sam"))
# True
"sample".endswith(("ple","ple."))
# True
```

### 16 Splitting a sentence to word
The split() method can be used to split a sentence to multiple words to form a list
```python
"This is a Sample".split()
# ['This', 'is', 'a', 'Sample']
```

### 17 Find the frequent word in a sentence
The word which occurs most times in a sentence can be found using the below trick
```python
sentence = "She was young the way an actual young person is young"
split_sentence = sentence.split()
most_frequent_word = max(set(split_sentence),key=split_sentence.count)
# 'young'
```

### 18 Find how many occurences of words in a sentence
The below trick helps in finding, how many times the word is present in the sentence sorted by the increasing rate of word occurence.
```python
from collections import Counter
sentence = "She was young the way an actual young person is young"
split_sentence = sentence.split()
Counter(split_sentence)
# Counter({'young': 3, 'She': 1, 'was': 1, 'the': 1, 'way': 1, 'an': 1, 'actual': 1, 'person': 1, 'is': 1})
```

### 19 Convert all the words to capital in a sentence
The map() method can be used to make all words to capital letters.
```python
sentence = "Quick brown fox".split()
list(map(str.capitalize,sentence))
# ['Quick', 'Brown', 'Fox']
```

### 20 Remove duplicate words in a sentence
Duplicate words in a sentence can be removed has shown below
```python
sentence = "The sound sounds sound".split()
list(set(sentence))
# ['sound', 'The', 'sounds']
```

### 21 Remove duplicate words retain the sentence order
The below trick removes the duplicate word keeping the order of words in the sentence.
```python
from collections import OrderedDict
sentence = "The sound sounds sound".split()
list(OrderedDict.fromkeys(sentence).keys())
# ['The', 'sound', 'sounds']
```

### 22 Reversing a sentence
The reverse() method can be used to reverse a sentence
```python
sentence = "This is Sample".split()
sentence.reverse()
print(sentence)
# ['Sample', 'is', 'This']
```

### 23 Splitting words to multiple string
The below trick can be used to split a sentence into multiple words and storing in a string variable.
```python
sentence = "This is Sample".split()
first_word, second_word, third_word = sentence
print(first_word)
print(second_word)
print(third_word)
```

### 24 Combine list using zip() method
The zip() method can be used to combine two seperate list of strings.
```python
Name = ['Tom', 'Marry', 'Jon']
Age = ['35', '30', '40']
for Name, Age in zip(Name,Age):
    print(Name,Age)
###  Output ###
Tom 35
Marry 30
Jon 40
```

### 25 Sort words in a list using sorted() method
The sorted() method can be used to sort the list of strings.
```python
sorted(['string1','string2','string3'],reverse=True)
# ['string3', 'string2', 'string1']
```