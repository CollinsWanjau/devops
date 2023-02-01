# Regular Expressions


## Literal Characters

* The most basic regualr expression consists of a single literal character.

* Such as `a`.It matches the first occurence of that character in the string.
<b>Jack is a boy</b>.

* In a pragramming language, there is usually a function that you can call
to continue searching thru the string.

* Characters with special meaning:
1. `\` - backslash      4. `.` - period/dot     8. `(` & `)` - parenthesis
2. `^` - caret          5. `|` - pipe           9. `[` & `{`
3. `$` - dollar sign    6. `?` 
4. `*`                  7. `+`

* These special charcters are often called <b>metacharacters</b>

## Special Characters

* Note that `1+1=2`, with the backslash ommitted, is a valid regex.

* If you want to match `1+1=2`, the correct regex is `1\+1=2`.

* `1+1=2` would match `111=2` in `123+111=234`, due to the special meaning
of the plus character.

## Character Classes or Character Sets

* With a `character class`, also called `character set`, you can tell the
regex engine to match only one out of several characters.

* If you want to match an `a` or an `e`, use `[ae]`.

* You could use this in `gr[ae]y` to match either `gray` or `grey`.

* You can use hyphen inisde a charcter class to specify a range of charcters.
`[0-9]`.

* You can use more than one range `[0-9a-fA]`

### Negated Characters Classes

* Typing a `^` after the opening `[` negates the character class.

* The result is that char class matches any charcter that is not in the
character class.

* If you do not want a negated class to match  line breaks, you need
to include the line break chars in the class.

`[^0-9\r\n]` matches any charcter that is not a digit or a line break.

* It is important to remember that a negated character class still
must match a character, `q[^u]` means:"a q followed by a character that
is not a u".It does not match the q in the string `Iraq`.

* It does match the q and the space after the q in `Iraq is a country`.

### Metacharacters Inside Character Classes

* The special chars or metachars inside a char class are:
1. Closing bracket(])
2. The Backslash(\)
3. Caret(^)
4. Hyphen

* To include a backslash as a charcter without any special meaing inside
a char class, you have to escape it with `[\\x]` matches a backslash
or an x.

* To include an escaped caret as a literal, place it anywhere except right
after the opening bracket

* `[x^]` - matches an x or a caret.

### Repeating Character Classes

* If you repeat a character class by using the `?, *, +` operators, you're
repeating the entire character class.

* `[0-9]+` - the `+` symbol following the character class specifies that
the preceding pattern should be matched one or more consecutive occurences
This can matche `837` as well as `222`

* If you want to repeat the matched char, rather than the class, you need
to use backreferences.

* `([0-9])\1+` matches `833337`, it matches `3333` in the middle of the
string

* `Backreferences` in regular expressions refer to a way of reusing a
previously matched pattern within the same expression.This is achieved by
capturing the matched text in a capturing group, and then later referencing
the captured text by it's group number.

* Capturing groups are specified  using parentheses `(...)`.Each opening
parenthesis creates a new capturing group, and the group number is derterminied
by the order of the opening parentheses.

* For example, the first capturing group is numbered 1, the second is numbered
2, and so on.

* `(...)\n`, where `n` is the number of the capturing group you want to
reference.

### Optional Items

* The question mark makes the preceding token in the regular expression
optional.`colou?r` matches both `colour` or `color`.

* `Nov(ember)?` - matches `Nov` and `November`.

* `Feb(ruary)? 23(rd)?` - matches `February 23rd`, `Feb 23`, `Febraury 23`,
`Feb 23rd`.

### Important Regex Concept: Greediness

* The question mark is the first metacharacter introduced by this tutorial
that is greedy.

* It gives the regex two choices:
1. Try to match the part the question mark applies to.(The engine always
trys to match that part).

* You can make the question mark lazy by putting a second question mark after
the first.

2. Do not match it.
### Repetition with Star and Plus

* The `*` tells the engine to attempt to match the preceding token zero
or more times.

* The plus tells the engine to attempt to match the preceding token once
or more.

* `<[A-Za-z][A-Za-z0-9]*>` matches an HTML tag without any attributes.

* So it will match a tag like `<B>`.

* When matching <HTML>, the first character class will match `H`.The star
will cause the second character class to be repeated three times, matching
`T`, `M`, `L`.

### Limiting Repetition

* `{min}{max}`

* `{0, 1}` - is the same as `?`.

* `{0,}` - is the same as `*`.

* `{1,}` - is the same as `+`

* `\b[1-9][0-9]{3}\b` - matches a number between 1000 and 9999.

* `\b[1-9][0-9]{2, 4}\b` - matches a number betwwen 100 and 99999.

### Watch Out for The Greediness!

* `<.+>` - When u test it on a string like `This is a <EM>first</EM> test`

* You might expect the regex to match `<EM>` and when continuing after that
match, `</EM>`.

* The regex will match `<EM>first</EM>`.

* The engine here backtracks after reaching the end of the string upto `>`


### Laziness Instead of Greediness

* A quick fix to the `+` greediness is to make the plus lazy instead of
greedy

* You can do that by adding a question mark after the plus in the regex.

* `<.+?>` - This tells the eninge to repeat the dot as few times as possible.

### Shorthand Character Classes

* `\d` - is short for `[0-9]`

* `\w` - stands for "word character".It always matches the ASCII
`[A-Za-z0-9_]`

* `\s` - stands for "whitespace character" - `[ \t\r\n\f]`
The s matches a space, a tab, a carriage return, a line feed or a form feed.

* `\s\d` - matches a whitespace followed by a digit.

* `[\s\d]` - either a whitespace or a digit

### Negated Shorthand Character

* `\D` - same as `[^\d]`
 
* `\W` - same as `[^\w]`

* `\S` - same as `[^\s]`

#### Start of string and End of String Anchors

* Anchors match a position before, after or in between characters.

* The caret `^` matches the position before the first character in the string.

* Applying `^a` to `abc` matches `a`.

* `$` matches right after the last character in the string.`c$` matches `c`
in `abc`, while a$ does not match at all.

#### Using ^ and $ as Start of Line and End of Line Anchors

* If you have a string consisting of multiple liines, like 
`first line\nsecond line`(where \n indicates a line break), it is often
desirable to work with lines, rather than the entire string.

* `^` can match at the start of the string(before the `f` in the above string)
as well as after each line break(between `\n` and `s`).

* Likewise, `$`  still matches at the end of the string (after the last `e`)
, and also before every line break(between `e` and `\n`)

#### Use the Dot Sparingly

* The dot is a very powerful regex metacharacter. It allows you to be lazy.

* Put in a dot and everything matches just fine when you test the regex on
valid data.

* The problem is that the regex also matches in cases where it should not
match.

* Say you want to match a date in mm/dd/yyyy format, but we want to leave
the user the choice of date separators.The quick solution is `\d\d.\d\d.\d\d` .

* Seems at first it matches a date like `02/12/03` just fine.Trouble is:
`02512703` is also considered a valid date by this regualr expression

* In this match, the first dot matched `5`, and the second matched `7`.

* `\d\d[- /.]\d\d[- /.]\d\d`

#### Strings Ending with a Line Break

* `^\d+$` - matches `123` where the subject string is `123` or `123\n`.

#### Zero-Length Regex Matches

* Using `^\d*$` to test if the user entered a number would give undesirable
results.It causes the script to accept an empty string as a valid input.

* The solution is `^\d+$` with the proper quantifier to require at least one
digit to be entered.

#### Advancing After a Zero-Length Regex Match

* If a regex can find zero-length matches at any position in the string,
then it will continue to match the empty string at each subsequent position
until it can no longer match any characters in the string.

* This can result in an infinite loop and cause perfomance issues.To avoid,
this, it is recommended to use a possesive quantifier or an atomic group 
to specify that the match must consume at least one character.

#### Use Parenthesis for Grouping and Capturing

* By placing part of a regular expression inside round brackets or parentheses
, you can group that part of the regular expression together.

* This allows you to apply a quantifier to the entire group or to restrict
alternation to part of the regex.

* Only parentheses are used for grouping.

#### Parenthesis Create Numbered Capturing Groups

* Besides grouping part of a regular expression together, parentheses also
create a numbered capturing group

* It stores the part of the string matched by the part of the regular
expression.

* The regex `Set(value)?` matches `Set` or `SetValue`.

* In the first case, the first (and only) capturing group remains empty.

* In the second case, the first capturing group matches `Value`.

#### Named Capturing Groups and Backreferences

* `(?P<name>group)` - captures the match of `group` into the backreference
"name".

* `name` must be an alphanumeric sequnce starting with a letter.

* `<(?P<tag>[A-Z][A-Z0-9]*)\b[^>]*>.*?</\1>`
