# Regular Expressions
## Anchors
* `^` start of string. Example: `^root` string starts with _root_
* `$` end of string. Example: `4$` string ends with _4_
* `^$` means an empty line

## Ranges
* `[A-Za-z]` any letter
* `[0-9]` any number
* `[a-z_]` any lowercase letter or underscore
* `[349]` matches 3,4,or 9
* `[^4]` not 4. `^` negates the character

## Boundaries
* `\s` whitespace, `\S` not a whitespace
* `\b` word boundary. It can be whitespace, hyphen, etc., `\B` not a word boundary

## Quantifiers
* `u*` matches `u` zero or more times
* `u?` matches `u` zero or only once (optional)
* `u+` matches one or more occurrences of `u`
* `u{3}` matches exactly 3 occurrence of `u`
* `^\s*#` matches a line or part of a line that is commented with `#`

