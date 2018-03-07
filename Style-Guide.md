#When writing code for Oz we follow these rules:#

###General formatting rules:###
- Two spaces, no tabs (for indentation).
- No trailing whitespace. Blank lines should not have any spaces.
- Prefer `and`/`or` over `&&`/`||`.
- Use `my_method(my_arg)` not `my_method( my_arg )` or `my_method my_arg`.
- Use `a = b` and not `a=b`.
- Prefer `method { do_stuff }` instead of `method{do_stuff}` for single-line blocks.
- Put spaces after list items and method parameters (`[1, 2, 3]`, not `[1,2,3]`).

###Rules for Naming:###
Give as descriptive a name as possible, within reason. Do not worry about saving horizontal space as it is far more important to make your code immediately understandable by a new reader. Do not use abbreviations that are ambiguous or unfamiliar to readers outside your project, and do not abbreviate by deleting letters within a word. NEVER use single letter variables (even in loops).

Good:

```
priceCountReader      # No abbreviation.
numErrors             # "num" is a widespread convention.
numDnsConnections     # Most people know what "DNS" stands for.
```
Bad:
```
n                     # Meaningless.
nErr                  # Ambiguous abbreviation.
nCompConns            # Ambiguous abbreviation.
wgcConnections        # Only your group knows what this stands for.
pcReader              # Lots of things can be abbreviated "pc".
cstmrId               # Deletes internal letters.
kSecondsPerDay        # Do not use Hungarian notation.
```

###Final thoughts to keep in mind:###
Code is generally written once, but read many times over. Consider the people who will read your code, and make it look nice for them.
Follow the conventions in the source you see used already.