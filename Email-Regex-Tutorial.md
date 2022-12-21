# Email Regex Tutorial

In this tutorial we will examine a regular expression that is normally used to match, or verify a users email address.

## Summary

Regular expressions can look intimidating, but after we break this down and discuss how all of these pieces fit together to accomplish our task, it should feel a little less daunting.

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

---

Once we break down the regular expression into components we can see the tasks associated with each. Here are some of the common components you will find in regular expressions, followed by examples for our use case.

### Anchors

---

Anchors are special characters that are used to match the position of a character in a string, rather than the character itself.

In regular expressions, there are two types of anchors:

`^` This is the "start of line" anchor. It specifies that the following pattern must start at the beginning of the string being tested.

`$` This is the "end of line" anchor. It specifies that the preceding pattern must end at the end of the string being tested.

Note: There is also a

In our example:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

Note: In regular expressions, the forward slash (/) is often used as a delimiter to indicate the start and end of the expression. While using delimiters is not strictly necessary, it is a common convention that is followed by many programming languages. It can also make it easier to read and understand regular expressions, especially when they contain many special characters and patterns.

You can see following the `/` in our example that there is a special character of `^` which denotes our "start of line" anchor.

At then end of our regex you will also see a `$` before our final deliminter `/`, which denotes our "end of line" anchor.

### Quantifiers

---

Quantifiers are special characters that are used to specify the number of times that a character or pattern should be repeated.

In regular expressions, there are several types of quantifiers:

`-` This is the "zero or more" quantifier. It specifies that the preceding character or pattern can be matched zero or more times. For example, `a\*` would match zero or more "a" characters.

`*` This is the "one or more" quantifier. It specifies that the preceding character or pattern must be matched one or more times. For example, `a+` would match one or more "a" characters.

`?` This is the "zero or one" quantifier. It specifies that the preceding character or pattern can be matched zero or one time. For example, `a?` would match zero or one "a" characters.

`{n}` This is the "exactly n times" quantifier. It specifies that the preceding character or pattern must be matched exactly n times. For example, `a{3}` would match exactly three "a" characters.

`{n,}` This is the "at least n times" quantifier. It specifies that the preceding character or pattern must be matched at least n times. For example, `a{3,}` would match at least three "a" characters.

`{n,m}` This is the "at least n, but not more than m times" quantifier. It specifies that the preceding character or pattern must be matched at least n times, but not more than m times. For example, `a{3,5}` would match at least three "a" characters, but not more than five "a" characters.

In our example:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

`+` This is the "one or more" quantifier. It appears after the first character class, `[a-z0-9_\.-]`, and it specifies that the character class must be matched one or more times. This quantifier is used to match the username part of the email address.

It also appears after the second character class, `[\da-z\.-]`, and it again specifies that the character class must be matched one or more times. This time it is used to match the domain part of the email address, including the subdomain if present.

`{2,6}` - This is the "at least n, but not more than m times" quantifier. It appears after the third character class, `[a-z\.]`, and it specifies that the character class must be matched at least two times, but not more than six times. This quantifier is used to match the top-level domain of the email address (e.g., "com", "edu", "gov").

### Grouping Constructs

---

Grouping constructs in regular expressions are often used to group characters or patterns together and apply quantifiers or other operations to them as a unit. They are an important part of regular expressions and are used to help match complex patterns in strings.

In our example:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

Here, there are three pairs of grouping constructs `()` that are used to group characters or patterns together.

Here is a breakdown of the grouping constructs and their role in the regular expression:

`([a-z0-9_\.-]+)` This group is used to match the username part of the email address. It consists of a character class that matches any lowercase letter, digit, underscore, dot, or hyphen, followed by the "one or more" quantifier `+`. The grouping construct is used to apply the quantifier to the entire character class as a unit.

`([\da-z\.-]+)` This group is used to match the domain part of the email address, including the subdomain if present. It consists of a character class that matches any digit, lowercase letter, dot, or hyphen, followed by the "one or more" quantifier `+`. The grouping construct is used to apply the quantifier to the entire character class as a unit.

`([a-z\.]{2,6})` This group is used to match the top-level domain of the email address (e.g., "com", "edu", "gov"). It consists of a character class that matches any lowercase letter or dot, followed by the "at least n, but not more than m times" quantifier `({2,6})`. The grouping construct is used to apply the quantifier to the entire character class as a unit.

### Character Classes

---

Character classes are a shorthand way to match any character from a set of characters. They can also include pre-defined classes such as:

`\d` any digit (0-9)

`\s` any whitespace character (space, tab, newline, etc.)

`\w` any word character (alphanumeric characters and underscores)

Note: These character classes are case sensitive, so `\d` will only match digits and `\w` will only match alphanumeric characters and underscores. If you want to match both uppercase and lowercase letters, you can use the character class `[a-zA-Z]`.

In our example:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

`\d` This character class matches any digit (0-9). It is used in the bracket expression `[\da-z\.-]` to match the domain part of the email address.

`\.- ` This is a combination of the escape character `\` and the characters `.` and `-`. The `\` is used to treat the `.` and `-` characters literally, rather than as special characters. These characters are used in the bracket expressions `[a-z0-9_\.-]` and `[\da-z\.-]` to match the local part and domain part of the email address.

### Bracket Expressions

---

Bracket expressions are a type of character class that allows you to match any single character from a set of characters or ranges. They are also denoted using square brackets `[]` and can include individual characters or ranges of characters, such as `[abc]` to match the characters `a`, `b`, or `c`, or `[a-z]` to match any lowercase letter. Bracket expressions are a more general form of character class and can include characters that are not part of the predefined character classes.

In our example:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

`([a-z0-9_\.-]+)` This is a bracket expression that matches one or more characters from the set `a-z`, `0-9`, `_`, `.`, or `-`. It is used to match the local part of the email address, which is the part before the `@` symbol. The `+` after the bracket expression indicates that one or more characters from the set should be matched.

`([\da-z\.-]+)` This is another bracket expression that matches one or more characters from the set `\d`, `a-z`, `.`, or `-`. It is used to match the domain part of the email address, which is the part after the `@` symbol and before the `.` symbol. Again, the `+` after the bracket expression indicates that one or more characters from the set should be matched.

`([a-z\.]{2,6})` This is another bracket expression that matches two to six characters from the set `a-z` or `.`. It is used to match the top-level domain of the email address, which is the part after the `.` symbol. The `{2,6}` after the bracket expression indicates that the preceding pattern (in this case, the bracket expression) should be repeated two to six times.

### The OR Operator

---

In regular expressions, the OR operator (also known as the alternation operator) is represented by the vertical bar `|` and is used to match one of several alternative patterns. Essentially, it allows you to specify multiple options for a pattern.

In our example:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

We actually dont use an OR operator in this regex. Instead, the regular expression uses a combination of character classes and bracket expressions to specify the allowed characters in different parts of the email address. The regular expression is designed to match a specific pattern for an email address, rather than multiple alternative patterns.

### Flags

---

Regular expressions have optional flags that allow for functionality like global searching and case-insensitive searching. These flags can be used separately or together in any order, and are included as part of the regular expression.

Here are some common flags you may see in regular expressions:

`i` Makes the pattern case-insensitive.

`m` Treats the input string as multiple lines. Without this flag, the `^` and `$` symbols match the start and end of the entire string, rather than the start and end of a line.

`s` Treats the input string as a single line. With this flag, the . symbol will match any character, including a newline.

`g` Global search. Without this flag, the search will stop after the first match is found. With the g flag, the search will continue until all matches are found.

In our example of:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

Again, we do not use any flags in our example. Instead please take a look at the following example that uses a regular expression flag `i` to make the search case-insensitive.

```
/(?i)bryan/
```

If we were to search a string of "Hello, my name is Bryan." we would have an expected outcome of "Bryan". Even though it is a capitolized name in the string, the flag `i` makes the search case-insensitive.

### Character Escapes

---

In regular expressions, the `\` symbol is used to escape special characters that would otherwise have a special meaning in the regular expression. You also escape certain letters that represent common character classes, such as `\w` for a word character or `\s` for a space.

In our example of:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

`\d` Matches any digit (0-9).

`\w` Matches any word character (`a-z`, `A-Z`, `0-9`, and `\_`).

`\s` Matches any whitespace character (space, tab, newline, etc.).

`\.-` Matches a dot or a hyphen.

`\.[a-z]{2,6}` Matches a dot followed by two to six letters.

### Author

---

Bryan Tempini

I hope this was helpful!

If you would like to get in touch for any reason please contact me on [github](https://github.com/btempini) or by [email](mailto:mistatempini@gmail.com).
