---
id: 18_regex
title: Regular Expression
sidebar_label: Regular Expression
slug: /Advanced Python/18_regex
---

---

A Regular Expression (RegEx) is a special sequence of characters which helps us to match, search and find a pattern. Python has a built-in module called `re` which supports RegEx fully. A combination of functions in this library with special patterns help us to use this module efficiently.

#### Metacharacters

Metacharacters are the characters with special meaning.

| Character | Description | Example |
|:-:|:-:|:-:|
| [...] | A set of characters | "[a-zA-Z]" |
| [^...] | A set of characters not mentioned in brackets | "[^a-zA-Z]" |
| \ | Signals a special sequence | "\d" |
| . | Any character | "l..e" |
| * | Zero or more occurrences | "a*" |
| + | One or more occurrences | "a+" |
| ? | Zero or One occurrence | "a?" |
| ^ | Starts with | "^This" |
| $ | Ends with | "end$" |
| {} | Exactly matches the specified number of occurrences | "a{3}" |
| \| | Either or | a\|b |
| () | Capture and group | "(\W)" |


#### Special Sequences

A special sequence is a character followed by `\` which has a special meaning.

| Character | Description | Example |
|:-:|:-:|:-:|
| \d | Returns a match where the string contains digits (0-9) | "\d" |
| \D | Returns a match where the string **DOES NOT** contains digits | "\D" |
| \s |	Returns a match where the string contains a white space character | "\s" | 	
| \S | Returns a match where the string **DOES NOT** contain a white space character | "\S" |
| \w | Returns a match where the string contains any word characters (0-9a-zA-Z) | "\w" | 	
| \W | Returns a match where the string **DOES NOT** contain any word characters | "\W" |
| \A | Matches the beginning of the string | "\AThe" |
| \Z | Matches the end of the string | "end\Z" |

#### Sets

A set is list of characters inside a `[]` with special meaning.

- `[bfo]`: returns a match where one of the mentioned characters (here is 'b', 'f' or 'o') is available
- `[a-z]`: returns a match for any alphabetically between a to z
- `[^bfo]`: returns a match where there are any other characters **EXCEPT** a, r, and n 	
- `[379]`:	eturns a match where one of the mentioned digits (here is 3, 7 or 9) is available 	
- `[0-9]`: returns a match for any digit between 0 and 9 	
- `[1-4][0-9]`: returns a match for any two-digit numbers from 10 and 49 	
- `[a-zA-Z]`: returns a match for any alphabetical character between a and z, lower case OR upper case 	

### RegEx Fnctions

The `re` module provides various functions to match, search and find a pattern.

- `match`: matches pattern to the string
- `search`: searches and returns the first occurrence of pattern in a string
- `findall`: returns a list containing all matched patterns
- `sub`: replaces one or more matches with a string
- `split`: returns a list where the string has been split at each match

#### The Match Function

This function tries to match a pattern to a string.
`re.match(pattern, string, flags=0)`

- `pattern`: The RegEx which should be matched
- `string`: This the string in which the specified pattern should be searched or matched.
- `flags`: RegEx modifiers

The methods which help us to extract the `match` outputs are:

- `matchObj.start()`: the start position of matched object
- `matchObj.end()` the end position of matched object
- `matchObj.groups()`: a tuple of all matched objects
- `matchOj.group(n)`: nth matched object
- `matchOj.string`: returns the string passed into the function
- `matchOj.span()`: returns a tuple of start and end position of matched object

```
import re

string = "This is a tesT to sHow how RegEx works."
pattern = r'\w+'

match_obj = re.match(pattern, string)
print(match_obj)


(output): <re.Match object; span=(0, 4), match='This'>
```

#### The Search Function

This Function searches and returns the first occurrence of pattern in a string.
`re.search(pattern, string, flags=0)`

- `pattern`: The RegEx which should be matched
- `string`: This the string in which the specified pattern should be searched or matched.
- `flags`: RegEx modifiers

The methods which help us to extract the `search` outputs are:

- `searchObj.start()`: the start position of searched object
- `searchObj.end()` the end position of searched object
- `searchObj.groups()`: a tuple of all searched objects
- `searchObj.group(n)`: nth searched object
- `searchObj.string`: returns the string passed into the function
- `searchObj.span()`: returns a tuple of start and end position of searched object

```
import re

string = "This is a tesT to sHow how RegEx works."
pattern = r'([a-z]+[A-Z])'

match_obj = re.search(pattern, string)

print(match_obj)


(output): <re.Match object; span=(10, 14), match='tesT'>
```

#### Search Vs. Match

The `match` checks for the match only at the beginning of the string, while `search` checks the whole the string.

#### RegEx Modifiers (Option Flags)

The modifiers are specified as an optional flag. By applying OR (`|`), it is possible to apply several modifiers simultaneously.

- `re.I`: performs case-insensitive matches
- `re.L`: interprets words according to the current locale.
- `re.M`: makes $ match the end of a line (not just the end of the string) and makes ^ match the start of any line (not just the start of the string)
- `re.S`: makes a period match any character, including a newline


#### The Findall Function
The `findall` returns a list containing all matched patterns.

`re.findall(pattern, string)`

- `pattern`: The RegEx which should be matched
- `string`: This the string in which the specified pattern should be searched or matched.


```
import re

string = "This is a tesT to sHow how RegEx works."
pattern = r'([A-Z][a-z]+)'

findall_obj = re.findall(pattern, string)

print(findall_obj)


(output): ['This', 'How', 'Reg', 'Ex']
```

#### The Sub Function (Search and Replace)

The `sub` function will replace all the pattern occurrences in the string with desired choice(`repl`). Maximum number of replacement can change by assigning value to `max` flag.

`re.sub(pattern, repl, string, max=0)`

Example:
```
import re

string = "This is a tesT to sHow how RegEx works."
pattern = r'\s'
repl = '*'

new_string = re.sub(pattern, repl, string)

print(new_string)


(output): This*is*a*tesT*to*sHow*how*RegEx*works.
```

#### The Split Function

The `split` function returns a list where the string has been split at each match.

`re.split(pattern, string)`

- `pattern`: The RegEx which should be matched
- `string`: This the string in which the specified pattern should be searched or matched.

Example:
```
import re

string = "This is a tesT to sHow how RegEx works."
pattern = r'[A-Z]'

new_string = re.split(pattern, string)

print(new_string)


(output): ['', 'his is a tes', ' to s', 'ow how ', 'eg', 'x works.']
```
