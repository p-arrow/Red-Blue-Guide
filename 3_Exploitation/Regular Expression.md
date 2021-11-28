*Group of characters describe how to execute specific search*

RegEx | Explanation
----- | -----------
[...] | [a-z], [a-zA-Z0-9], [\d] (single digit), [\s] (white space)
? | matches 0 to 1
\* | matches 0 to many
\+ | matches 1 to many
{min, max} | matches from min to max
(...) | defines matching group, subsequently referred by \1, \2
| | OR logical operator
^ | match at the start of a line
$ | match at the end of a line

**Example: '/^(?=.*\d)(?=.*[A-Za-z])[0-9A-Za-z!@#$%]{8,12}$/'**

- Between start --> ^
- And end --> $
- At least one number --> (?=.*\d)
- At least one letter --> (?=.*[A-Za-z])
- Allowed characters --> [0-9A-Za-z!@#$%]
- Min 8 and max 12 characters --> {8,12}
