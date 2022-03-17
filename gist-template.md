# Title (Regexp Guide)

Regular expressions are extremely useful in extracting information from text such as code, log files, spreadsheets, or even documents.

Regular expressions, often shortened to "regex" or "regexp", are patterns that help programmers match, search, and replace text. Regular expressions are very powerful, but can be hard to read because they use special characters to make more complex, flexible matches.

Although used in any computer application or language, within Javascript specifically  regular expressions are objects. The RegExp object has a number of top level methods, and to test whether a regular expression matches a specific string in Javascript, you can use RegExp.test(). To actually extract information from a string using a regular expression, you can instead use the RegExp.exec() call which provides more information about the match in its result.

## Summary

A regular expression is a pattern that describes a set of strings.

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

The components of regular expressions are the Basic Elements that can be used to match to a character you are searching for, and Qualifying Characters to refine the search, comprising the special characters of the keyboard.

These characters are grouped into categories such as Character Classes, Groups, Quantifiers, Backreferences, Anchors, Boundaries, Delimiters, Lookarounds, Modifiers, and others.

To start with:

.       - Any Character Except New Line
\d      - Digit (0-9)
\D      - Not a Digit (0-9)
\w      - Word Character (a-z, A-Z, 0-9, _)
\W      - Not a Word Character
\s      - Whitespace (space, tab, newline)
\S      - Not Whitespace (space, tab, newline)

\b      - Word Boundary
\B      - Not a Word Boundary
\- ^    - Beginning of a String (just the caret)
\- $    - End of a String(just the dollar sign)

[]      - Matches Characters in brackets
[^ ]    - Matches Characters NOT in brackets
|       - Either Or
( )     - Group

Quantifiers:
*       - 0 or More
+       - 1 or More
?       - 0 or One
{3}     - Exact Number
{3,4}   - Range of Numbers (Minimum, Maximum)


### Anchors

Anchors have special meaning in regular expressions. They do not match any character. Instead, they match a position before or after characters:

\- ^ – The caret anchor matches the beginning of the text.

\- $ – The dollar anchor matches the end of the text.

Consider this example:

	let str = 'JavaScript';
	console.log(/^J/.test(str));

The output of this code will return true. 

First we declare a variable of a string we want to test against a regular expression.

In a console log is our test case, which is wrapped in forward slashes to identify it as a regex literal, telling the regex engine to look at what is written between the slashes.

The first character of our test is the CARET ANCHOR, anchoring the beginning of our expression. 

Next is the letter J, followed by .test(str), which is the regex test function testing the parameter in the parentheses, in this case a variable.

We are asking, is the letter J the first character in the variable str? The answer is yes, true. And it would be false if it was a lowercase J because regex is case-sensitive.

If we were to remove the caret and put the dollar sign after the J we would be asking, is J the last letter in the variable str? The answer is no, false, J is not the last letter of Javascript.


### Quantifiers

Quantifiers match a number of instances of a character, group, or character class in a string. A number in curly braces {n}is the simplest quantifier. When you append it to a character or character class, it specifies how many characters or character classes you want to match.

For example, the regular expression /\d{4}/ matches a four-digit number. It is the same as /\d\d\d\d/:

	let str = 'ECMAScript 2020';
	let re = /\d{4}/;

	let result = str.match(re);

	console.log(result);

Output:

	["2020"]

This .match() function is checking for 4 digits in the variable str and returns 4 digits if they are present. From a performance point of view it would actually be better to do /\d\d\d\d\/ because the /\d{4}/ is actually a loop. It loops 4 times.

### Grouping Constructs

Groupings consist of sets and ranges. The square brackets search for any character in a set. For example, [aeiou] matches any of the five characters: 'a', 'e', 'i', 'o' and 'u'. The [...] is called a set.

For example, the regular expression /[cbr]ats/g matches cats, bats, and rats:

	let str = 'How cats, rats, and bats became Halloween animals';
	let re = /[cbr]ats/g;
	let results = str.match(re);

	console.log(results);

Output:

	["cats", "rats", "bats"]

The square brackets can contain character ranges. For example, [a-z] is a character range from a to z. And [0-9] is a digit from 0 to 9.

The [a-zA-Z0-9_] is the same as \w. The [0-9] is the same as \d. As referenced above in components.



### Bracket Expressions

### Character Classes

### The OR Operator

### Flags

### Character Escapes

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
