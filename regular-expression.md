A regular expression is a special string that describes a search pattern. Many of you have surely seen and used them already when typing expressions like ls(or dir) *.txt , to get a list of all the files with the extension txt. Regular expressions are very useful not only for pattern matching, but also for manipulating text. In SRMs regular expressions can be extremely handy. Many problems that require some coding can be written using regular expressions on a few lines, making your life much easier.

# | operator
A regular expression(regex) is one or more non-empty branches, separated by ‘|’. It matches anything that matches one of the branches. The following regular expression will match any of the three words “the”,”top”,”coder”(quotes for clarity).

REGEX is : the|top|coder
INPUT is : Marius is one of the topcoders.
Found the text "the" starting at index 17 and ending at index 20.
Found the text "top" starting at index 21 and ending at index 24.
Found the text "coder" starting at index 24 and ending at index 29.

# +, *, ? operator
A piece is an atom possibly followed by a `*`, `+`, `?`, or bound. An atom followed by `*` matches a sequence of 0 or more matches of the atom. An atom followed by `+` matches a sequence of 1 or more matches of the atom. An atom followed by `?` matches a sequence of 0 or 1 matches of the atom.

REGEX is: (top|coder)+
INPUT is: This regex matches topcoder and also codertop.
Found "topcoder" starting at index 19 and ending at index 27.
Found "codertop" starting at index 37 and ending at index 45.

# {} operator
A bound is ‘{‘ followed by an unsigned decimal integer, possibly followed by ‘,’ possibly followed by another unsigned decimal integer, always followed by ‘}’.If there are two integers, the first may not exceed the second. An atom followed by a bound containing one integer i and no comma matches a sequence of exactly i matches of the atom. An atom followed by a bound containing one integer i and a comma matches a sequence of i or more matches of the atom. An atom followed by a bound containing two integers i and j matches a sequence of i through j (inclusive) matches of the atom.
The following regular expression matches any sequence made of ’1′s having length 2,3 or 4 .

REGEX is: 1{2,4}
INPUT is: 101 + 10 = 111 , 11111 = 10000 + 1111
Found the text "111" starting at index 11 and ending at index 14.
Found the text "1111" starting at index 17 and ending at index 21.
Found the text "1111" starting at index 33 and ending at index 37.

One should observe that, greedily, the longest possible sequence is being matched and that different matches do not overlap. An atom is a regular expression enclosed in ‘()’ (matching a match for the regular expression), a bracket expression (see below), ‘.’ (matching any single character), ‘^’ (matching the null string at the beginning of a line), ‘$’ (matching the null string at the end of a line), a `\’ followed by one of the characters `^.[$()|*+?{\' (matching that character taken as an ordinary character) or a single character with no other significance (matching that character). There is one more type of atom, the back reference: `\' followed by a non-zero decimal digit d matches the same sequence of characters matched by the d-th parenthesized subexpression (numbering subexpressions by the positions of their opening parentheses, left to right), so that (e.g.) `([bc])\1′ matches `bb’ or `cc’ but not `bc’.

The following regular expression matches a string composed of two lowercase words separated by any character.

Current REGEX is: ([a-z]+).\1
Current INPUT is: top-topcoder|coder
I found the text "top-top" starting at index 0 and ending at index 7.
I found the text "coder|coder" starting at index 7 and ending at index 18.
A bracket expression is a list of characters enclosed in ‘[]‘. It normally matches any single character from the list. If the list begins with ‘^’, it matches any single character not from the rest of the list. If two characters in the list are separated by `-’, this is shorthand for the full range of characters between those two inclusive (e.g. ‘[0-9]‘ matches any decimal digit). With the exception of ‘]’,’^’,’-’ all other special characters, including `\’, lose their special significance within a bracket expression.

The following regular expression matches any 3 character words not starting with ‘b’,’c’,’d’ and ending in ‘at’.

Current REGEX is: [^b-d]at
Current INPUT is: bat
No match found.

Current REGEX is: [^b-d]at
Current INPUT is: hat
I found the text "hat" starting at index 0 and ending at index 3.
This example combines most concepts presented above. The regex matches a set of open/close pair of html tags.

REGEX is: <([a-zA-Z][a-zA-Z0-9]*)(()| [^>]*)>(.*)</\1>
INPUT is: <font size="2">Topcoder is the</font> <b>best</b>
Found "<font size="2">Topcoder is the</font>" starting at index 0 and ending at index 37.
Found "<b>best</b>" starting at index 38 and ending at index 49.
([a-zA-Z][a-zA-Z0-9]*) will match any word that starts with a letter and continues with an arbitrary number of letters or digits. 
(()| [^>]*) will match either the empty string or any string which does not contain ‘>’ . 
\1 will be replaced using backreferencing with the word matched be ([a-zA-Z][a-zA-Z0-9]*)

- https://swtch.com/~rsc/regexp/regexp1.html
- http://www.regular-expressions.info/tutorial.html
