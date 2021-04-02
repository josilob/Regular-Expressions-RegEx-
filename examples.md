Examples on the string:
'The fat cat ran down the street.
It was searching for a mouse to eat.'

`/cat/g` -flag 'g' stands for global (or matchAll vs single match)

Case insensitive:
`/the/i` (matches single case insensitive 'the')

`/e+/g` (match 1 or more of the preceeding token, 'e' in this case)

`/ea?/g` (match character 'a' optionally, if it is there right after char 'e')

`/re\*/g` (match zero or more - letter 'r' by itself + 'ree' in street)

`/.at/g` (match everything at that spot, except a new line - 'fat','cat','eat')

`/\./g` - selects all periods (backslash cancels)
`/.\./g` - selects any character that comes before period

`/\w/` - Match any word character (alphanum + underscore)
`/\W/` - Match everything that is not alphanumeric character
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

`/^T/g` - Match the beginning of the line