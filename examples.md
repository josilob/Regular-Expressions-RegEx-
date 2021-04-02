Examples on the string:
_'The fat cat ran down the street.
It was searching for a mouse to eat.'_

`/cat/g` -flag 'g' stands for global, as matchAll instead of first occurance

`/the/i` -Matches case insensitive 'the'

`/e+/g` -Match 1 or more of the preceeding token, 'e' in this case ()

`/ea?/g` -Match character 'a' optionally, if it is there

`/re\*/g` Match zero or more - letter 'r' by itself + 'ree' in street)

`/.at/g` (match everything at that spot, except a new line - 'fat','cat','eat')

`/\./g` - selects all periods (backslash cancels)
`/.\./g` - selects any character that comes before period

`/\w/` - Match any word character (alphanum + underscore)
`/\W/` - Match everything that is not alphanumeric character
`/\d/` - Match any digit
`/\s/` - Match any form of whitespace there is
`/\S/` - Match everything that is NOT a whitespace

`/\w{4,}/g` - Match any four alphanumerics in a row
`/\w{4,5}/g` - Match between 4 and 5 alphanumerics in a row

/[fc]at/g - Match either 'fat' or 'cat' in a string
/[a-zA-Z]at/g - Match any alphabet letter upper or lowercase before 'at' (fat, cat, eat)

or smaller ranges:
/[a-c]at/g - Matches only 'cat' in this case

## Grouping

`/(t|T)he/g` - Matches 'the' or 'The'

`/(t|e|r){2,3}/g` - Matches 2-3 characters from brackets in a row (tre, et)

`/^T/g` - Match the beginning of the line (works only on 'T'), to enable it on multiline statement, flag 'm' must be added `/^I/gm` - This will match 'I' in 2nd line

`/\.$/g` - Match the dot at the END of the line (add flag 'm' for multiline)

## Lookaheads and Lookbehinds (positive and negative)

`/(?<=[tT]he)./g` - Matches first character of any type right after 'The' or 'the' (two spaces)

`/(?<=![tT]he)./g` - Matches any single character that DOES NOT have 'The' or 'the' preceeding it (note exclamation mark) - opposite from previous example

`/.(?=at)/g` - Matches every character that IS FOLLOWED by 'at' (f-at, c-at, e-at)

`/.(?!at)/g` - inverts previous case (NOT followed by 'at') - everything but fat, cat & eat

Phone Number Example:
`/\d{10}/g` - Match 10 digits in a row (1234567890)
`/\d{3}-?\d{3}-?\d{4}/` Match 10 digits with dashes, optionally (123-456-7890)
`/\d{3}[- ]?\d{3}[- ]?\d{4}/` Match 10 digits with spaces or dashes, optionally (123-456-7890)
`/(\d{3})[- ]?(\d{3})[- ]?(\d{4})/` - Same as previous plus form groups - each set of ()
`/\(?(\d{3})\)?[- ]?(\d{3})[- ]?(\d{4})/` - Matches '(123) 456-7890' format
`/((\+1)[ -])?\(?(\d{3})\)?[- ]?(\d{3})[- ]?(\d{4})/` - Matches '+1 123 456 7890' international format
