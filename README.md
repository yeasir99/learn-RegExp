# Regular Expressions (Regex)

**Regular Expression, or regex or regexp in short, is extremely and amazingly powerful in searching and manipulating text strings, particularly in processing text files. One line of regex can easily replace several dozen lines of programming codes.**<br />
**Regex is supported in all the scripting languages (such as Perl, Python, PHP, and JavaScript); as well as general purpose programming languages such as Java; and even word processors such as Word for searching texts. Getting started with regex may not be easy due to its geeky syntax, but it is certainly worth the investment of your time.**

## 1. Regex By Examples

**This section is meant for those who need to refresh their memory. For novices, go to the next section to learn the syntax, before looking at these examples.**

### 1.1 Regex Syntax Summary

<hr />

- **Character:** All characters, except those having special meaning in regex, matches themselves. E.g., the regex x matches substring "x"; regex 9 matches "9"; regex = matches "="; and regex @ matches "@".

- **Special Regex Characters:** These characters have special meaning in regex (to be discussed below): ., +, \*, ?, ^, $, (, ), [, ], {, }, |, \\.

- **Escape Sequences (\char):**
  - To match a character having special meaning in regex, you need to use a escape sequence prefix with a backslash (\). E.g., \. matches "."; regex \+ matches "+"; and regex \( matches "(".
  - You also need to use regex \\ to match "\" (back-slash).
  - Regex recognizes common escape sequences such as \n for newline, \t for tab, \r for carriage-return, \nnn for a up to 3-digit octal number, \xhh for a two-digit hex code, \uhhhh for a 4-digit Unicode, \uhhhhhhhh for a 8-digit Unicode.
- **A Sequence of Characters (or String):** Strings can be matched via combining a sequence of characters (called sub-expressions). E.g., the regex Saturday matches "Saturday". The matching, by default, is case-sensitive, but can be set to case-insensitive via modifier.

- **OR Operator (|):** E.g., the regex four|4 accepts strings "four" or "4".

- **OR Operator (|):**
  - [...]: Accept ANY ONE of the character within the square bracket, e.g., [aeiou] matches "a", "e", "i", "o" or "u".
  - [.-.] (Range Expression): Accept ANY ONE of the character in the range, e.g., [0-9] matches any digit; [A-Za-z] matches any uppercase or lowercase letters.
  - [^...]: NOT ONE of the character, e.g., [^0-9] matches any non-digit.
  - Only these four characters require escape sequence inside the bracket list: ^, -, ], \\.
