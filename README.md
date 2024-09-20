# Regular Expressions (Regex)

**Regular Expression, or regex or regexp in short, is extremely and amazingly powerful in searching and manipulating text strings, particularly in processing text files. One line of regex can easily replace several dozen lines of programming codes.**<br />
**Regex is supported in all the scripting languages (such as Perl, Python, PHP, and JavaScript); as well as general purpose programming languages such as Java; and even word processors such as Word for searching texts. Getting started with regex may not be easy due to its geeky syntax, but it is certainly worth the investment of your time.**

## 1. Regex By Examples

**This section is meant for those who need to refresh their memory. For novices, go to the next section to learn the syntax, before looking at these examples.**

### 1.1 Regex Syntax Summary

---

- **Character:** All characters, except those having special meaning in regex, matches themselves. E.g., the regex x matches substring "x"; regex 9 matches "9"; regex = matches "="; and regex @ matches "@".

- **Special Regex Characters:** These characters have special meaning in regex (to be discussed below): ., +, \*, ?, ^, $, (, ), [, ], {, }, |, \\.

- **Escape Sequences (\char):**
  - To match a character having special meaning in regex, you need to use a escape sequence prefix with a backslash (\). E.g., \. matches "."; regex \+ matches "+"; and regex \( matches "(".
  - You also need to use regex \\ to match "\" (back-slash).
  - Regex recognizes common escape sequences such as \n for newline, \t for tab, \r for carriage-return, \nnn for a up to 3-digit octal number, \xhh for a two-digit hex code, \uhhhh for a 4-digit Unicode, \uhhhhhhhh for a 8-digit Unicode.
- **A Sequence of Characters (or String):** Strings can be matched via combining a sequence of characters (called sub-expressions). E.g., the regex Saturday matches "Saturday". The matching, by default, is case-sensitive, but can be set to case-insensitive via modifier.

- **OR Operator (|):** E.g., the regex four|4 accepts strings "four" or "4".

- **Character class (or Bracket List):**

  - [...]: Accept ANY ONE of the character within the square bracket, e.g., [aeiou] matches "a", "e", "i", "o" or "u".
  - [.-.] (Range Expression): Accept ANY ONE of the character in the range, e.g., [0-9] matches any digit; [A-Za-z] matches any uppercase or lowercase letters.
  - [^...]: NOT ONE of the character, e.g., [^0-9] matches any non-digit.
  - Only these four characters require escape sequence inside the bracket list: ^, -, ], \\.

- **Occurrence Indicators (or Repetition Operators):**

  - +: one or more (1+), e.g., [0-9]+ matches one or more digits such as '123', '000'.
  - \*: zero or more (0+), e.g., [0-9]\_ matches zero or more digits. It accepts all those in [0-9]+ plus the empty string.
  - ?: zero or one (optional), e.g., [+-]? matches an optional "+", "-", or an empty string.
  - {m,n}: m to n (both inclusive)
  - {m}: exactly m times
  - {m,}: m or more (m+)

- **Meta-characters:** matches a character

  - . (dot): ANY ONE character except newline. Same as [^\n]
  - \d, \D: ANY ONE digit/non-digit character. Digits are [0-9]
  - \w, \W: ANY ONE word/non-word character. For ASCII, word characters are [a-zA-Z0-9_]
  - \s, \S: ANY ONE space/non-space character. For ASCII, whitespace characters are [ \n\r\t\f]

- **Position Anchors:** does not match character, but position such as start-of-line, end-of-line, start-of-word and end-of-word.

  - ^, \$: start-of-line and end-of-line respectively. E.g., ^[0-9]$ matches a numeric string.
  - \b: boundary of word, i.e., start-of-word or end-of-word. E.g., \bcat\b matches the word "cat" in the input string.
  - \B: Inverse of \b, i.e., non-start-of-word or non-end-of-word.
  - \<, \>: start-of-word and end-of-word respectively, similar to \b. E.g., \<cat\> matches the word "cat" in the input string.
  - \A, \Z: start-of-input and end-of-input respectively.

- **Parenthesized Back References:**
  - Use parentheses ( ) to create a back reference.
  - Use $1, $2, ... (Java, Perl, JavaScript) or \1, \2, ... (Python) to retreive the back references in sequential order.
- **Laziness (Curb Greediness for Repetition Operators):** \*?, +?, ??, {m,n}?, {m,}?

### 1.2 Example: Numbers [0-9]+ or \d+

---

1. A regex (regular expression) consists of a sequence of sub-expressions. In this example, [0-9] and +.
2. The [...], known as character class (or bracket list), encloses a list of characters. It matches any SINGLE character in the list. In this example, [0-9] matches any SINGLE character between 0 and 9 (i.e., a digit), where dash (-) denotes the range.
3. The +, known as occurrence indicator (or repetition operator), indicates one or more occurrences (1+) of the previous sub-expression. In this case, [0-9]+ matches one or more digits.
4. A regex may match a portion of the input (i.e., substring) or the entire input. In fact, it could match zero or more substrings of the input (with global modifier).
5. This regex matches any numeric substring (of digits 0 to 9) of the input. For examples
   - If the input is "abc123xyz", it matches substring "123".
   - If the input is "abcxyz", it matches nothing.
   - If the input is "abc00123xyz456_0", it matches substrings "00123", "456" and "0" (three matches).
   <p>Take note that this regex matches number with leading zeros, such as "000", "0123" and "0001", which may not be desirable.<p/>
6. You can also write \d+, where \d is known as a meta-character that matches any digit (same as [0-9]). There are more than one ways to write a regex! Take note that many programming languages (C, Java, JavaScript, Python) use backslash \ as the prefix for escape sequences (e.g., \n for newline), and you need to write "\\d+" instead.

### 1.3 Code Examples In JavaScript

---

```js
const inStr = 'abc123xyz456_7_00';

// Use RegExp.test(inStr) to check if inStr contains the pattern

console.log(/[0-9]+/.test(inStr)); //  true

// Use String.search(regex) to check if the string contains the pattern
// Returns the start position of the matched substring or -1 if there is no match

console.log(inStr.search(/[0-9]+/)); //  3

// Use String.match() or RegExp.exec() to find the matched substring,
//   back references, and string index

console.log(inStr.match(/[0-9]+/)); // expected output ["123", input:"abc123xyz456_7_00", index:3, length:"1"]
console.log(/[0-9]+/.exec(inStr)); // expected output ["123", input:"abc123xyz456_7_00", index:3, length:"1"]

// With g (global) option

console.log(inStr.match(/[0-9]+/g)); // ["123", "456", "7", "00", length:4]

// RegExp.exec() with g flag can be issued repeatedly.
// Search resumes after the last-found position (maintained in property RegExp.lastIndex).

var pattern = /[0-9]+/g;
var result;
while ((result = pattern.exec(inStr))) {
  console.log(result);
  console.log(pattern.lastIndex);
  // ["123"],  6
  // ["456"], 12
  // ["7"],   14
  // ["00"],  17
}

// String.replace(regex, replacement):

console.log(inStr.replace(/\d+/, '**')); // abc**xyz456_7_00
console.log(inStr.replace(/\d+/g, '**')); // abc**xyz**_**_**
```

### 1.4 Example: Full Numeric Strings ^[0-9]+\$ or ^\d+$

---

1. The leading ^ and the trailing $ are known as position anchors, which match the start and end positions of the line, respectively. As the result, the entire input string shall be matched fully, instead of a portion of the input string (substring).
2. This regex matches any non-empty numeric strings (comprising of digits 0 to 9), e.g., "0" and "12345". It does not match with "" (empty string), "abc", "a123", "abc123xyz", etc. However, it also matches "000", "0123" and "0001" with leading zeros.

### 1.5 Example: Positive Integer Literals [1-9][0-9]_|0 or [1-9]\d_|0

---

1. [1-9] matches any character between 1 to 9; [0-9]_ matches zero or more digits. The _ is an occurrence indicator representing zero or more occurrences. Together, [1-9][0-9]\* matches any numbers without a leading zero.
2. | represents the OR operator; which is used to include the number 0.
3. This expression matches "0" and "123"; but does not match "000" and "0123" (but see below).
4. You can replace [0-9] by meta-character \d, but not [1-9].
5. We did not use position anchors ^ and $ in this regex. Hence, it can match any parts of the input string. For examples

   - If the input string is "abc123xyz", it matches the substring "123".
   - If the input string is "abcxyz", it matches nothing.
   - If the input string is "abc123xyz456_0", it matches substrings "123", "456" and "0" (three matches).
   - If the input string is "0012300", it matches substrings: "0", "0" and "12300" (three matches)!!!

### 1.6 Example: Full Integer Literals ^[+-]?[1-9][0-9]_|0$ or ^[+-]?[1-9]\d_|0$

---

1. This regex match an Integer literal (for entire string with the position anchors), both positive, negative and zero.
2. [+-] matches either + or - sign. ? is an occurrence indicator denoting 0 or 1 occurrence, i.e. optional. Hence, [+-]? matches an optional leading + or - sign.
3. We have covered three occurrence indicators: + for one or more, \* for zero or more, and ? for zero or one.

### 1.7 Example: Identifiers (or Names) [a-zA-Z\_][0-9a-zA-Z_]_ or [a-zA-Z_]\w\_

---

1. Begin with one letters or underscore, followed by zero or more digits, letters and underscore.
2. You can use meta-character \w for a word character [a-zA-Z0-9_]. Recall that meta-character \d can be used for a digit [0-9].

### 1.8 Example: Image Filenames ^\w+\.(gif|png|jpg|jpeg)$

---

1. The position anchors ^ and $ match the beginning and the ending of the input string, respectively. That is, this regex shall match the entire input string, instead of a part of the input string (substring).
2. \w+ matches one or more word characters (same as [a-zA-Z0-9_]+).
3. \. matches the dot (.) character. We need to use \. to represent . as . has special meaning in regex. The \ is known as the escape code, which restore the original literal meaning of the following character. Similarly, \*, +, ? (occurrence indicators), ^, $ (position anchors) have special meaning in regex. You need to use an escape code to match with these characters.
4. (gif|png|jpg|jpeg) matches either "gif", "png", "jpg" or "jpeg". The | denotes "OR" operator. The parentheses are used for grouping the selections.
5. The modifier i after the regex specifies case-insensitive matching (applicable to some languages like Perl and JavaScript only). That is, it accepts "test.GIF" and "TesT.Gif".

### 1.9 Example: Email Addresses ^\w+([.-]?\w+)_@\w+([.-]?\w+)_(\.\w{2,3})+$

---

1. The position anchors ^ and $ match the beginning and the ending of the input string, respectively. That is, this regex shall match the entire input string, instead of a part of the input string (substring).
2. \w+ matches 1 or more word characters (same as [a-zA-Z0-9_]+).
3. [.-]? matches an optional character . or -. Although dot (.) has special meaning in regex, in a character class (square brackets) any characters except ^, -, ] or \ is a literal, and do not require escape sequence.
4. ([.-]?\w+)\* matches 0 or more occurrences of [.-]?\w+.
5. The sub-expression \w+([.-]?\w+)\* is used to match the username in the email, before the @ sign. It begins with at least one word character [a-zA-Z0-9_], followed by more word characters or . or -. However, a . or - must follow by a word character [a-zA-Z0-9_]. That is, the input string cannot begin with . or -; and cannot contain "..", "--", ".-" or "-.". Example of valid string are "a.1-2-3".
6. The @ matches itself. In regex, all characters other than those having special meanings matches itself, e.g., a matches a, b matches b, and etc.
7. Again, the sub-expression \w+([.-]?\w+)\* is used to match the email domain name, with the same pattern as the username described above.
8. The sub-expression \.\w{2,3} matches a . followed by two or three word characters, e.g., ".com", ".edu", ".us", ".uk", ".co".
9. (\.\w{2,3})+ specifies that the above sub-expression could occur one or more times, e.g., ".com", ".co.uk", ".edu.sg" etc. <br />

**Exercise: Interpret this regex, which provide another representation of email address: ^[\w\-\.\+]+\@[a-zA-Z0-9\.\-]+\.[a-zA-z0-9]{2,4}$.**

### 1.10 Example: Swapping Words using Parenthesized Back-References ^(\S+)\s+(\S+)$ and $2 $1

---

1. The ^ and $ match the beginning and ending of the input string, respectively.
2. The \s (lowercase s) matches a whitespace (blank, tab \t, and newline \r or \n). On the other hand, the \S+ (uppercase S) matches anything that is NOT matched by \s, i.e., non-whitespace. In regex, the uppercase meta-character denotes the inverse of the lowercase counterpart, for example, \w for word character and \W for non-word character; \d for digit and \D or non-digit.
3. The above regex matches two words (without white spaces) separated by one or more whitespaces.

4. Parentheses () have two meanings in regex:

   - to group sub-expressions, e.g., (abc)\*
   - to provide a so-called back-reference for capturing and extracting matches.

5. The parentheses in (\S+), called parenthesized back-reference, is used to extract the matched substring from the input string. In this regex, there are two (\S+), match the first two words, separated by one or more whitespaces \s+. The two matched words are extracted from the input string and typically kept in special variables $1 and $2 (or \1 and \2 in Python), respectively.
6. To swap the two words, you can access the special variables, and print "$2 $1" (via a programming language); or substitute operator "s/(\S+)\s+(\S+)/$2 $1/" (in Perl).

### 1.11 Example: HTTP Addresses ^http:\/\/\S+(\/\S+)\*(\/)?$

---

1. Begin with http://. Take note that you may need to write / as \/ with an escape code in some languages (JavaScript, Perl).
2. Followed by \S+, one or more non-whitespaces, for the domain name.
3. Followed by (\/\S+)\*, zero or more "/...", for the sub-directories.
4. Followed by (\/)?, an optional (0 or 1) trailing /, for directory request.

### 1.12 Example: Regex Patterns in JavaScript

---

```js
let ISO_DATE_REGEXP =
  /^\d{4,}-[01]\d-[0-3]\dT[0-2]\d:[0-5]\d:[0-5]\d\.\d+(?:[+-][0-2]\d:[0-5]\d|Z)$/;
let URL_REGEXP =
  /^[a-z][a-z\d.+-]*:\/*(?:[^:@]+(?::[^@]+)?@)?(?:[^\s:/?#]+|\[[a-f\d:]+])(?::\d+)?(?:\/[^?#]*)?(?:\?[^#]*)?(?:#.*)?$/i;
let EMAIL_REGEXP =
  /^(?=.{1,254}$)(?=.{1,64}@)[-!#$%&'*+/0-9=?A-Z^_`a-z{|}~]+(\.[-!#$%&'*+/0-9=?A-Z^_`a-z{|}~]+)*@[A-Za-z0-9]([A-Za-z0-9-]{0,61}[A-Za-z0-9])?(\.[A-Za-z0-9]([A-Za-z0-9-]{0,61}[A-Za-z0-9])?)*$/;
// Match both uppercase and lowercase letters, single-quote but not double-quote

let NUMBER_REGEXP = /^\s*(-|\+)?(\d+|(\d*(\.\d*)))([eE][+-]?\d+)?\s*$/;

let DATE_REGEXP = /^(\d{4,})-(\d{2})-(\d{2})$/;

let DATETIMELOCAL_REGEXP =
  /^(\d{4,})-(\d\d)-(\d\d)T(\d\d):(\d\d)(?::(\d\d)(\.\d{1,3})?)?$/;

let WEEK_REGEXP = /^(\d{4,})-W(\d\d)$/;

let MONTH_REGEXP = /^(\d{4,})-(\d\d)$/;

let TIME_REGEXP = /^(\d\d):(\d\d)(?::(\d\d)(\.\d{1,3})?)?$/;
```

## 2. Regular Expression (Regex) Syntax

A Regular Expression (or Regex) is a pattern (or filter) that describes a set of strings that matches the pattern. In other words, a regex accepts a certain set of strings and rejects the rest.

A regex consists of a sequence of characters, metacharacters (such as ., \d, \D, \s, \S, \w, \W) and operators (such as +, \\\*, ?, |, ^). They are constructed by combining many smaller sub-expressions.

### 2.1 Matching a Single Character

---

The fundamental building blocks of a regex are patterns that match a single character. Most characters, including all letters (a-z and A-Z) and digits (0-9), match itself. For example, the regex x matches substring "x"; z matches "z"; and 9 matches "9".

Non-alphanumeric characters without special meaning in regex also matches itself. For example, = matches "="; @ matches "@".

### 2.2 Regex Special Characters and Escape Sequences

---

**Regex's Special Characters**
These characters have special meaning in regex (I will discuss in detail in the later sections):

- metacharacter: dot (.)
- bracket list: [ ]
- position anchors: ^, $
- occurrence indicators: +, \\\*, ?, { }
- parentheses: ( )
- or: |
- escape and metacharacter: backslash (\\)

**Escape Sequences**
The characters listed above have special meanings in regex. To match these characters, we need to prepend it with a backslash (\), known as escape sequence. For examples, \\+ matches "+"; \\[ matches "["; and \\. matches ".".

Regex also recognizes common escape sequences such as \n for newline, \t for tab, \r for carriage-return, \nnn for a up to 3-digit octal number, \xhh for a two-digit hex code, \uhhhh for a 4-digit Unicode, \uhhhhhhhh for a 8-digit Unicode.

**EXAMPLE**

```js
// come back fill up wih code
```

### 2.3 Matching a Sequence of Characters (String or Text)

---

**Sub-Expressions**  
A regex is constructed by combining many smaller sub-expressions or atoms. For example, the regex Friday matches the string "Friday". The matching, by default, is case-sensitive, but can be set to case-insensitive via modifier.

### 2.4 OR (|) Operator

---

You can provide alternatives using the "OR" operator, denoted by a vertical bar '|'. For example, the regex four|for|floor|4 accepts strings "four", "for", "floor" or "4".

### 2.5 Bracket List (Character Class) [...], [^...], [.-.]

---

A bracket expression is a list of characters enclosed by [ ], also called character class. It matches ANY ONE character in the list. However, if the first character of the list is the caret (^), then it matches ANY ONE character NOT in the list. For example, the regex [02468] matches a single digit 0, 2, 4, 6, or 8; the regex [^02468] matches any single character other than 0, 2, 4, 6, or 8.

Instead of listing all characters, you could use a range expression inside the bracket. A range expression consists of two characters separated by a hyphen (-). It matches any single character that sorts between the two characters, inclusive. For example, [a-d] is the same as [abcd]. You could include a caret (^) in front of the range to invert the matching. For example, [^a-d] is equivalent to [^abcd].

Most of the special regex characters lose their meaning inside bracket list, and can be used as they are; except ^, -, ] or \\.

- To include a ], place it first in the list, or use escape \\].
- To include a ^, place it anywhere but first, or use escape \\^.
- To include a - place it last, or use escape \\-.
- To include a \\, use escape \\\\.
- No escape needed for the other characters such as ., +, \*, ?, (, ), {, }, and etc, inside the bracket list
- You can also include metacharacters (to be explained in the next section), such as \w, \W, \d, \D, \s, \S inside the bracket list.

### 2.6 Metacharacters ., \w, \W, \d, \D, \s, \S

---

A metacharacter is a symbol with a special meaning inside a regex.

- The metacharacter dot (.) matches any single character except newline \n (same as [^\n]). For example, ... matches any 3 characters (including alphabets, numbers, whitespaces, but except newline); the.. matches "there", "these", "the ", and so on.
- \w (word character) matches any single letter, number or underscore (same as [a-zA-Z0-9_]). The uppercase counterpart \W (non-word-character) matches any single character that doesn't match by \w (same as [^a-zA-Z0-9_]).
- In regex, the uppercase metacharacter is always the inverse of the lowercase counterpart.
- \d (digit) matches any single digit (same as [0-9]). The uppercase counterpart \D (non-digit) matches any single character that is not a digit (same as [^0-9]).
- \s (space) matches any single whitespace (same as [ \t\n\r\f], blank, tab, newline, carriage-return and form-feed). The uppercase counterpart \S (non-space) matches any single character that doesn't match by \s (same as [^ \t\n\r\f]).

           \s\s       # Matches two spaces
           \S\S\s     # Two non-spaces followed by a space
           \s+        # One or more space
           \S\s\S+    # Two words (non-spaces) separated by a space

### 2.7 Backslash (\\) and Regex Escape Sequences

---

Regex uses backslash (\) for two purposes:

1. for metacharacters such as \d (digit), \D (non-digit), \s (space), \S (non-space), \w (word), \W (non-word).
2. to escape special regex characters, e.g., \. for ., \+ for +, \* for \*, \? for ?. You also need to write \\ for \ in regex to avoid ambiguity.
3. Regex also recognizes \n for newline, \t for tab, etc.

Take note that in many programming languages (C, Java, Python), backslash (\) is also used for escape sequences in string, e.g., "\n" for newline, "\t" for tab, and you also need to write "\\" for \\. Consequently, to write regex pattern \\ (which matches one \) in these languages, you need to write "\\\\" (two levels of escape!!!). Similarly, you need to write "\\d" for regex metacharacter \d. This is cumbersome and error-prone!!!

### 2.8 Modifiers

---
