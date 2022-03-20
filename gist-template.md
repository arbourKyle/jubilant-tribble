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
- [Matching a Hex Value](#matching-a-hex-value)
- [Matching an Email](#matching-an-email)
- [Matching a URL](#matching-a-URL)
- [Matching an HTML Tag](#matching-an-HTML-tag)

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
{0}     - Exact Number
{0,10}   - Range of Numbers (Minimum, Maximum)


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

The first token of our test is the CARET ANCHOR, anchoring the beginning of our expression. 

Next is the letter J, followed by .test(str), which is the regex test function testing the parameter in the parentheses, in this case a variable.

We are asking, is the letter J the first character in the variable str? The answer is yes, true. And it would be false if it was a lowercase J because regex is case-sensitive.

If we were to remove the caret and put the dollar sign after the J we would be asking, is J the last letter in the variable str? The answer is no, false, J is not the last letter of Javascript.


### Quantifiers

Quantifiers match a number of instances of a character, group, or character class in a string. A number in curly braces {n} is the simplest quantifier. When you append it to a character or character class, it specifies how many characters or character classes you want to match.

For example, the regular expression /\d{4}/ matches a four-digit number. It is the same as /\d\d\d\d/:

	let str = 'ECMAScript 2020';
	let re = /\d{4}/;

	let result = str.match(re);

	console.log(result);

Output:

	["2020"]

This .match() function is checking for 4 digits in the variable str and returns 4 digits if they are present. From a performance point of view it would actually be better to do /\d\d\d\d\/ because the /\d{4}/ is actually a loop. It loops 4 times.

### Grouping Constructs

Groupings consist of Sets and Ranges. The square brackets search for any character in a set. For example, [aeiou] matches any of the five characters: 'a', 'e', 'i', 'o' and 'u'. The [...] is called a set.

For example, the regular expression /[cbr]ats/g matches cats, bats, and rats. The g at the end is a flag, meaning to search for all matches, without this flag the expressions would only return the first match, 'cats'. In a later section flags will be covered in more detail.

	let str = 'How cats, rats, and bats became Halloween animals';
	let re = /[cbr]ats/g;
	let results = str.match(re);

	console.log(results);

Output:

	["cats", "rats", "bats"]

The square brackets can contain character ranges. For example, [a-z] is a character range from a to z. And [0-9] is a digit from 0 to 9.

The [a-zA-Z0-9_] is the same as \w. The [0-9] is the same as \d. As referenced above in components.


### Bracket Expressions

A bracket expression is a list of characters enclosed by [ and ]. It matches any SINGLE CHARACTER in that list. If the first character of the list is the CARET ANCHOR, then it matches any character NOT in the list, and it is unspecified whether it matches an encoding error.

For example, the regular expression [0123456789] matches any single digit, whereas [^()] matches any single character that is not an opening or closing parenthesis, and might or might not match an encoding error.

Within a bracket expression, a range expression consists of two characters separated by a hyphen. It matches any single character that sorts between the two characters, inclusively.

For example, [a-d] is equivalent to [abcd].

### Character Classes

Certain named classes of characters are predefined within bracket expressions, to use them they are placed within another set of brackets.

[:alnum:]
Alphanumeric characters: [:alpha:] and [:digit:] - this is the same as [0-9A-Za-z].

[:alpha:]
Alphabetic characters: [:lower:] and [:upper:] - this is the same as [A-Za-z].

[:blank:]
Blank characters: space and tab.

[:cntrl:]
Control characters. In ASCII, these characters have octal codes 000 through 037, and 177 (DEL). In other character sets, these are the equivalent characters, if any.

[:digit:]
Digits: 0 1 2 3 4 5 6 7 8 9.

[:graph:]
Graphical characters: [:alnum:] and [:punct:].

[:lower:]
Lower-case letters: a b c d e f g h i j k l m n o p q r s t u v w x y z.

[:print:]
Printable characters: [:alnum:], [:punct:], and space.

[:punct:]
Punctuation characters: ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~.

[:space:]
Space characters: tab, newline, vertical tab, form feed, carriage return, and space.

[:upper:]
Upper-case letters: A B C D E F G H I J K L M N O P Q R S T U V W X Y Z.

[:xdigit:]
Hexadecimal digits: 0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f.

Note that the brackets in these class names are part of the symbolic names, and must be included in addition to the brackets delimiting the bracket expression.

If you mistakenly omit the outer brackets, and search for say, [:upper:], you will get an error.


### The OR Operator

The OR Operator in regex is the pipe symbol you are probably familiar with. And you can use it the same way, but a more in-depth understanding of the regex engine and it's process is needed to use it intelligently, or you may run into problems.

If you want to search for the literal text cat or dog, separate both options with a vertical bar or pipe symbol: cat|dog. If you want more options, simply expand the list: cat|dog|mouse|fish.

The alternation operator has the lowest precedence of all regex operators. That is, it tells the regex engine to match either everything to the left of the vertical bar, or everything to the right of the vertical bar. If you want to limit the reach of the alternation, you need to use parentheses for grouping. If we want to improve the first example to match whole words only, we would need to use \b(cat|dog)\b. This tells the regex engine to find a word boundary, then either cat or dog, and then another word boundary. If we had omitted the parentheses then the regex engine would have searched for a word boundary followed by cat, or, dog followed by a word boundary.

Another example:

^I like (dogs|penguins), but not (lions|tigers).$
This expression will match any of the following strings:

I like dogs, but not lions.
I like dogs, but not tigers.
I like penguins, but not lions.
I like penguins, but not tigers.
However, there is an unintended side-effect of our grouping and alternation, as written above. This pattern will match any combination of the terms we’ve supplied, as expected, but it will also store those matches into match groups for later inspection.

If you don’t want your grouping and alternation to interfere with other numbered groups in your expression, each “or” group must be prefixed with ?: – like so:

^I like (?:dogs|penguins), but not (?:lions|tigers).$

### Flags

Regular expressions may have flags that affect the search.

There are only 6 of them in JavaScript:

i
With this flag the search is case-insensitive: no difference between A and a.

g
With this flag the search looks for all matches, without it – only the first match is returned.

m
Multiline mode , enable an expression to be written over multiple lines for clarity.

s
Enables “dotall” mode, that allows a dot . to match newline character \n.

u
Enables full Unicode support. The flag enables correct processing of surrogate pairs.

y
“Sticky” mode: searching at the exact position in the text.


### Character Escapes

Consider these meta characters:

	. [ { ( ) \ ^ $ | ? * + } ]

Each of these have a specific meaning and use in a regular expression, if you want to use the decimal as a decimal or a period, rather than it's designated regex function, it needs to be ESCAPED with a backslash in front of it.

You are probably familiar with wildcard notations such as the * to select all of soemthing in a file or search for all of something.

The regular expression to find all text files is ^.*\.txt$

Notice how the .text has a backslash before it so that the dot would be a literal dot. The backslash itself is not part of the regular expression and is not included in the search.

Referencing the components above, we can explain this expressions as follows:

Caret anchor, dot is any character, the first character can be anything. The * says any numbers of characters following the first, then .text, with the & anchoring the end saying anything thats ends with letter t.


### Matching a Hex Value

	/^#?([a-f0-9]{6}|[a-f0-9]{3})$/

The first token is the CARET ANCHOR, and then a number sign which is optional because it is followed by a question mark. The question mark tells the parser that the preceding character — in this case a number sign — is optional, but to be "greedy" and capture it if it's there.
Next, inside the first group of parentheses we have an OR OPERATOR in the centre.
The first group in SQUARE BRACKETS matches any alpha or digit, and in CURLY BRACES we have a QUANTIFIER denoting 6 characters.
After the PIPE/OR OPERATOR, we have the same expression with 3 characters instead of 6. Finally, we end the string with a DOLLAR ANCHOR($).

### Matching An Email

	/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

The first token is the CARET ANCHOR. Inside the first group of PARENTHESES, we match one or more alpha, digit, underscore, dot, or hyphen. The dot is escaped to be used in the search. Between the end of SQUARE BRACKETS grouping and the end of expression PARENTHESES we put the + sign to denote the match to be one time. And after the first group is the @ sign.
Next is the domain name, repeating the previous expression for any alpha, digit, underscore, dot, or hyphen; with another escaped dot. After which is a QUANTIFIER denoting two to six letters or dots. This number can be set to any length of domain name that you prefer. Finally, ending the expressing with the DOLLAR ANCHOR ($).

### Matching a URL

	/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
	
After the CARET ANCHOR, the first capturing group between PARENTHESES allows the URL to begin with "http://", "https://", or neither of them, with the question mark after the s to allow URL's that have http or https. The two slashes that follow the http must be escape so that they do not represent another regex expression. Another question mark at the end allows the http to be optional.

Next is the domain name: an expression group that must be familiar by now, searching for alphas, digits, dots, and hyphens. Between that expression group in PARENTHESES and the next is an escaped dot to ensure delimiting between the domain name and the folowing optional files and directories.
Inside the last two PARENTHESES groups, we want to match any number of forward slashes, letters, numbers, underscores, spaces, dots, or hyphens with a QUANTIFIER. This allows multiple directories to be matched along with a file at the end. The stars are used instead of the question mark because the star matches zero or more, not zero or one. If a question mark was to be used there, only one file/directory would be able to be matched.

Then a trailing slash is matched, but it can be optional. Finally we end with the DOLLAR ANCHOR($).


## Author

https://github.com/arbourKyle