# Wildcards

|    Wildcard    |                    Matches                    |
|:--------------:|:---------------------------------------------:|
| ?              | Any single character                          |
| *              | Any strings of characters                     |
| [abc]          | a, b or c                                     |
| [a-c]          | a, b or c                                     |
| [!abc]         | All except a, b or c                          |
| [abc!]         | a, b, c or !                                 |
| [a-zA-Z]       | All lowercase and uppercase letters           |
| [a-zA-Z0-9_-]  | All letters, all digits, underscore and dash  |
| [\!]           | !                                             |

| echo b{ed,olt,ar}s     | beds bolts bars         |
|------------------------|-------------------------|
| echo b{ar{d,n,k},ed}s  | bards barns barks beds  |
| echo {2..5}            | 2 3 4 5                 |
| echo {d..h}            | d e f g h               |
| echo b{o}lt            | b{o}lt                  |