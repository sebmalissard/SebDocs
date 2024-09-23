# Bash

## Operations on variables

Sources:
[[1]](http://wiki.bash-hackers.org/syntax/pe)
[[2]](http://tldp.org/LDP/Bash-Beginners-Guide/html/chap_10.html)

### Variable lenght

```${#VAR}``` Calculate the number of characters in a variable.
```
$ echo ${VAR}
my variable
$ echo ${#VAR}
11
```

### Use a default value

```${VAR:-WORD}``` If VAR is not defined or null, the expansion of WORD is substituted; otherwise the value of VAR is substituted.
```sh
$ echo ${VAR}

$ echo ${VAR:-text}
text
$ VAR="my variable"
$ echo ${VAR:-text}
my variable
```

Useful usage (or use next section method):
```sh
VAR=${VAR:-default_value}
```

### Assign a default value

```${VAR:=WORD}``` If VAR is not defined or null, the expansion of WORD is substituted and assigned; otherwise the value of VAR is substituted.
```sh
$ echo ${VAR}

$ echo ${VAR:=text}
text
$ echo ${VAR}
text
```

### Extract substring

```${VAR:OFFSET:LENGTH}``` Strip a number of characters according the parameters.
```sh
$ echo ${VAR}
my variable
$ echo ${VAR:3:8}
variable
```

### Replace substring

```${VAR/PATTERN/STRING}``` Replace a substring matched by the first pattern found.  
```${VAR//PATTERN/STRING}``` Replace a substring matched by all pattern found.
```sh
$ echo ${VAR}
my variable
$ echo ${VAR/variable/word}
my word
```
