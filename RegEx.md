## RegEx (Regular Expressions) => Search strings for patterns!!!

JS carries .match method for strings, which is used for matching patterns in a string.
It is basically same method as find in text editors. In JavaScript, it searches for given string with RegEx and returns array of all matches.

```js
str.match(regexp);
```

basic use(counting words in a string):

```js
let str = 'This is a test string';

let matchArr = str.match(/\w+/g); //more about \w+ to come

console.log(matchArr.length); //prints 5
```

Regular expressions are supported in most string functions, one such method is replace():

The `.replace` method is used on strings in JavaScript to replace parts of string with characters. It is often used like so:

```js
const str = 'JavaScript';
const newStr = str.replace('ava', '-');
console.log(newStr);
// J-Script
```

JavaScript has a number of string utility functions. Replace is one of them. The prototype of the replace method is as follows:

```
const newStr = str.replace(regexp|substr, newSubstr|function)
```

replace method acts on a string, and returns a string, taking two parameters (pattern to match and what to replace it with)
The FIRST parameter, can be either a STRING or RegEx

The second parameter could also be a function. To demonstrate it, let's check out an example:

```js
var str = 'This is a test string';

var newStr = str.replace(/\w+/g, function (match) {
	return match.split('').reverse().join('');
});

console.log(newStr); //prints "sihT si a tset gnirts"
```

This example reverses each word, separately in a String.

# Basic Regular Expressions

## Literals

A literal is any character which is evaluated as itself and not in any general form. Thus, `word` is also a valid regular expression which will match only "word".

If you want to replace all instances of a given word in JavaScript, you could do this:

```js
var str =
	'JavaScript is a very popular programming language. javascript is used in web developement. javascript is very easy to learn.';

var newStr = str.replace(/javascript/gi, 'js');

console.log(newStr);

/* prints "js is a very popular programming language. js is used in web developement. js is very easy to learn." */
```

We replaced all occurrences of JavasScript with JS by using the 'g' identifier. which stands for global search (meaning, it searches all occurrences rather than just the first one)

Another identifier is `i`, which stands for case-insensitive search, matching the strings ignoring the case sensitivity.

## Meta-characters

These are used for generic search, such as any digit, character or alpha-numeric character. These are some of the common ones:

- `\d` matches any digit 0-9
- `\w` matches any alpha-numeric character (alphabet a-z, A-Z and digits 0-9)
- `\s` matches any whitespace

Similarly, `\D`, `\W` and `\S `match any non-digit, non-alphanumeric and non whitespace characters, respectively. For example: `\d\d\d` would match any three digits in a row.

## Quantifiers

...are used to quantify any literal or meta-character. It can be used to select multiple occurrences of a given character. There are four types of quantifiers defined in reged:

- `*` is used to match 0 or more occurrences of a given character
- `+` is used to match 1 or more occurences of a given character
- `.` is used to match either no occurrence or 1 occurrence of a given char.
- `{min,max} or {n}` can be used to match a number of occurences in a range or a given number of times n.

An example would be the one we used above to reverse every word in a string.

- `\w+` matches one or more occurrences of an alpha-numeric character( or every word in a string)
- `\w`matches any alpha-numeric character or underscore (same as [a-zA-Z0-9_] )

```js
let str = 'This is    a          string with multiple        whitespaces';
let newStr = str.replace(/\s\s+/g, ' ');
console.log(newStr); // => 'This is a string with multiple whitespaces'
```

## Position meta-characters

...which represent a position. For example `^` represents the start of a line, `$` represents end of a line, and `\b` represents word boundaries.

### [ ] — Character Classes

You can list characters you want to match at a specific position by placing `[` and `]` symbols around these characters. For example, class `[0-9]` matches all digits from 0 to 9. You can also list all digits explicitly: `[0123456789]` — the meaning is the same. You can use dash with letters too, `[a-z]` will match any lowercase Latin character,`[A-Z]` will match any uppercase Latin character and `[a-zA-Z]` will match both.
You can also use `*` after a character class just like after `.`, which in this case means: _“match any number of occurrences of the characters in this class”_

# Examples:

```js
// matches a number, some characters and another number
const reg = /\d.*\d/;
const str = 'Java3foobar4Script';
const newStr = str.replace(reg, '-');
console.log(newStr);
// "Java-Script"
```

The string `3foobar4` matches the regex `/\d.*\d/`, so it is replaced.

What if we wanted to perform replacements at multiple places?
`Regex` already offers that with the `g` (global) flag, and the same can be used with `replace`. Here's how:

```js
const reg = /\d{3}/g;
const str = 'Java323Scr995ip4894545t';
const newStr = str.replace(reg, '');
console.log(newStr);
// JavaScrip5t
// 5 didn't pass the test :(
```

The regex matches parts of the string that are exactly 3 consecutive numbers. `323` matches it, `995` matches it, `489` matches it, and `454` matches it. But the last `5` does not match the pattern. The result is that `JavaScrip5t` shows how the patterns are correctly matched and replaces with the new substring (an empty string).

The case flag - `i` can also be used. This means you can replace case-insensitive patterns. Here's how it is used:

```js
const reg1 = /\dA/;
const reg2 = /\dA/i;
const str = 'Jav5ascript';
const newStr1 = str.replace(reg1, '--');
const newStr2 = str.replace(reg2, '--');
console.log(newStr1); // Jav5ascript
console.log(newStr2); // Jav--script
```

`..5a..` does not match the first syntax because RegEx is by default case-sensitive. But with the usage of the `i` flag, as seen in the second syntax, the string is as expected - replaced.

Split also uses RegEx. Which means you can split a string not just at substrings that match exact characters, but also patterns.Here's a quick look:

```js
const regex = /\d{2}a/;
const str = 'Hello54 How 64aare you';
console.log(str.split(regex));
// ["Hello54 How ", "are you"]
```

The string was split at 64a because that substring matches the regex specified.
Note that the global flag - `g` - in split is irrelevant, unlike the i flag and other flags. This is because split splits the string at the several points the regex matches.

### Anything inbetween

Match anything: `.*` => match `any character, any number of times`
This is used to find matches STARTING with or ENDING in SOME TEXT.
example: `loadScript.*lua`: matches everything starting with "loadScript" and ending in "lua".
`.*?` => Less greedy version of previous one. It matches first `lua` and stops there.
If the first instance of this RegEx, matched `lua` with more than one occurrance of this string, it would go all the way to the last one.

### Match a Strong Password

The password should:

- have a minimum of 4 characters

```js
/^(?=.{4,}).*$/;
// translates into => “Start from the beginning. Look ahead for 4 characters. Don’t remember the match. Come back to the beginning. Consume all the characters using `.*` and see if you reach the end of the string.”
```

- contain a number

```js
/^(?=.*\d+).*$/;
// translates into => "Start from the beginning of the string `/^`. Look ahead for 0 or more characters `?=.*`. Check if 1 or more numbers follow `\d+`. Once it matches, come back to the beginning (because we were in look ahead). Consume all the characters in the string until end of the string `.*$/`."
```

- contain lowercase

```js
/^(?=.*[a-z]+).*$/;
//translates into => same as previous one with \d being replaced with [a-z] lowercase range
```

- contain uppercase

```js
/^(?=.*[A-Z]+).*$/;
//translates into => sam as before except [a-z] turned into [A-Z]
```

- contain a symbol

```js
One way to match symbols is to place a list of symbols in a character set.
/^(?=.*[-+=_)(\*&\^%\$#@!~”’:;|\}]{[/?.>,<]+).*$/.test(“$”)
// this would take a while to translate, so there's workaround
```

And looks like:

```js
//considers space as symbol
let e1;
e1 = /^(?=.*[^a-zA-Z0-9])[ -~]+$/;
e1.test('_'); //true
e1.test(' '); //true

//does not take space
let e2;
e2 = /^(?=.*[^a-zA-Z0-9])[!-~]+$/;
e2.test(' '); //false
e2.test('_'); //true

//the underscore exception
let e3;
e3 = /^(?=.*[\W])[!-~]+$/;
e3.test('_'); //false
```

Within a character set, `^` negates the character set. That is, `[^a-z]` means, any character other than `a` to `z`. `[^a-zA-Z0-9]` then stands for any character other than lower case alphabets, upper case alphabets, and numerals.

\W could have been used for same, but that would add underscore `_` to the ignore list as well (we want to keep it as valid 'symbol').

#### CharSet Range

The [ASCII table](http://www.asciitable.com/) has 125 characters. zero (0) to 31 are not relevant to us. Space starts from 32 going all the way up to 126 which is tilda(~). The exclamation mark is 33.
So `[!-~]` covers all the symbols, letters and numbers we need.

Bringing it all together, we get this nice looking piece of regular expression
`/^(?=.{5,})(?=.*[a-z]+)(?=.*\d+)(?=.*[A-Z]+)(?=.*[^\w])[ -~]+$/`

This is where the syntax for dynamically building expression object comes in handy. We are going to build each piece separately and assemble them later.

```js
//start with prefix
let p = '^';

//look ahead
// min 4 chars
p += '(?=.{4,})';
// lower case
p += '(?=.*[a-z]+)';
// upper case
p += '(?=.*[A-Z]+)';
// numbers
p += '(?=.*\\d+)';
// symbols
p += '(?=.*[^ a-zA-Z0-9]+)';
//end of lookaheads

//final consumption
p += '[ -~]+';
//suffix
p += '$';

//Construct RegEx
let e = new RegEx(p);
// tests
e.test('aB0#'); //true
e.test(''); //false
e.test('aB0'); //false
e.test('ab0#'); //false
e.test('AB0#'); //false
e.test('aB00'); //false
e.test('aB!!'); //false

// space is in our control
e.test('aB 0'); //false
e.test('aB 0!'); //true
```

We can always rely on `.test()` method tests for a match in a string. `RegEx` constructor automatically adds starting and trailing slashes for us.

To match numbers we used `\\d` instead of the usual `\d`. This is because the variable `p` is just a normal string within double quotes. To insert a backslash, you need to escape the backslash itself.
`\\d` resolves to `\d` within the `RegEx` constructor.
