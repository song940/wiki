---
title: Sed
date: '2020-12-27T18:34:08.000Z'
icon: icon-sed
background: bg-red-400
tags:
  - editor
  - replace
  - text
  - utility
categories:
  - Linux Command
intro: >
  [Sed](https://www.gnu.org/software/sed/manual/sed.html) is a stream editor,
  this sed cheat sheet contains sed commands and some common sed tricks.
---

# sed

## Getting started {.cols-3}

### Sed Usage

Syntax \`\`\`shell script $ sed \[options\] command \[input-file\]

```text
With pipeline
```shell script
$ cat report.txt | sed 's/Nick/John/g'
```

\`\`\`shell script $ echo '123abc' \| sed 's/\[0-9\]+//g'

```text
### Option Examples {.col-span-2}

| Option | Example                                    | Description                             |
| ------ | ------------------------------------------ |---------------------------------------- |
| `-i`   | sed -ibak 's/On/Off/' php.ini              | Backup and modify input file directly   |
| `-E`   | sed -E 's/[0-9]+//g' input-file            | Use extended regular expressions        |
| `-n`   | sed -n '3 p' config.conf                   | Suppress default pattern space printing |
| `-f`   | sed -f script.sed config.conf              | Execute sed script file                 |
| `-e`   | sed -e 'command1' -e 'command2' input-file | Execute multiple sed commands           |
{.show-header}


### Multiple commands
```shell script {.wrap}
$ echo "hello world" | sed -e 's/h/H/g' -e 's/w/W/g'
Hello World
```

Use `-e` to execute multiple sed commands

### Sed script

\`\`\`shell script $ echo 's/h/H/g' &gt;&gt; hello.sed $ echo 's/w/W/g' &gt;&gt; hello.sed $ echo "hello world" \| sed -f hello.sed Hello World

```text
Use `-f` to execute sed script file



### Examples

```shell script
$ sed 's/old/new/g' file.txt
$ sed 's/old/new/g' file.txt > new.txt

$ sed 's/old/new/g' -i file.txt
$ sed 's/old/new/g' -i.backup file.txt
```

See: [Sed examples](sed.md#sed-examples)

## Sed commands {.cols-3}

### Commands {.col-span-2}

| Command | Example | Description |
| :--- | :--- | :--- |
| `p` | sed -n '1,4 p' input.txt | Print lines 1-4 |
| `p` | sed -n -e '1,4 p' -e '6,7 p' input.txt | Print lines 1-4 and 6-7 |
| `d` | sed '1,4 d' input.txt | Print lines except 1-4 |
| `w` | sed -n '1,4 w output.txt' input.txt | Write pattern space to file |
| `a` | sed '2 a new-line' input.txt | Append line after |
| `i` | sed '2 i new-line' input.txt | Insert line before |

{.show-header}

### Space commands

| Command | Description |
| :--- | :--- |
| `n` | Print pattern space, empty pattern space, and read next line |
| `x` | Swap pattern space with hold space |
| `h` | Copy pattern space to hold space |
| `H` | Append pattern space to hold space |
| `g` | Copy hold space to pattern space |
| `G` | Append hold space to pattern space |

See also: [File spacing](sed.md#file-spacing)

### Flags

\`\`\`shell script $ sed 's/old/new/\[flags\]' \[input-file\]

```text
---

| Flag             | Description                                 |
| ---------------- |-------------------------------------------- |
| `g`              | Global substitution                         |
| `1,2...`         | Substitute the nth occurrence               |
| `p`              | Print only the substituted line             |
| `w`              | Write only the substituted line to a file   |
| `I`              | Ignore case while searching                 |
| `e`              | Substitute and execute in the command line  |


### Loops commands

| Command    | Description                                                        |
| ---------- |------------------------------------------------------------------- |
| `b label` | Branch to a label (for looping)                                    |
| `t label` | Branch to a label only on successful substitution<br>(for looping) |
| `:label`  | Label for the b and t commands (for looping)                       |
| `N`        | Append next line to pattern space                                  |
| `P`        | Print 1st line in multi-line                                       |
| `D`        | Delete 1st line in multi-line                                      |



### Misc Flags
| Flag             | Description                                 |
| ---------------- |-------------------------------------------- |
| `/ | ^ @ ! #`    | Substitution delimiter can be any character |
| `&`              | Gets the matched pattern                    |
| `( ) \1 \2 \3` | Group using `(` and `)`.<br>Use `\1`, `\2` in replacement to refer the group|




Sed examples {.cols-3}
----------



### Replacing text {.row-span-2}

Replace all occurrences of a string
```shell script
$ sed 's/old/new/g' file.txt
```

Replace only the nth occurrence of a string \`\`\`shell script $ sed 's/old/new/2' file.txt

```text
Replace replace a string only on the 5th line
```shell script
$ sed '5 s/old/new/' file.txt
```

Replace "world" with "universe" but only if the line begins with "hello" \`\`\`shell script $ sed '/hello/s/world/universe/' file.txt

```text
Remove "\" from the end of each line
```shell script
$ sed 's/\\$//' file.txt
```

Remove all whitespace from beginning of each line \`\`\`shell script $ sed 's/^\s\*//' file.txt

```text
Remove comments. Even those that are at the end of a line
```shell script
$ sed 's/#.*$//' file.txt
```

### Search for text

Search for a string and only print the lines that were matched \`\`\`shell script $ sed -n '/hello/p' file.txt

```text
Case insensitive search
```shell script
$ sed -n '/hello/Ip' file.txt
```

Search for a string but only output lines that do not match \`\`\`shell script $ sed -n '/hello/!p' file.txt

```text
### Appending lines

Append line after line 2
```shell script
$ sed '2a Text after line 2' file.txt
```

Append line at the end of the file \`\`\`shell script $ sed '$a THE END!' file.txt

```text
Append line after every 3rd line starting from line 3
```shell script
$ sed '3~3a Some text' file.txt
```

### Numbering {.col-span-2}

Number line of a file \(simple left alignment\) \`\`\`shell script $ sed = file.txt \| sed 'N;s/\n/\t/'

```text
Number line of a file (number on left, right-aligned)
```shell script
$ sed = file.txt | sed 'N; s/^/   /; s/ *\(.\{6,\}\)\n/\1  /'
```

Number line of file, but only print numbers if line is not blank \`\`\`shell script $ sed '/./=' file.txt \| sed '/./N; s/\n/ /'

```text
Count lines (emulates "wc -l")
```shell script
$ sed -n '$='
```

### Prepending lines

Insert text before line 5 \`\`\`shell script $ sed '5i line number five' file.txt

```text
Insert "Example: " before each line that contains "hello"
```shell script
$ sed '/hello/i Example: ' file.txt
```

### Deleting lines

Delete line 5-7 in file \`\`\`shell script $ sed '5,7d' file.txt

```text
Delete every 2nd line starting with line 3
```shell script
$ sed '3~2d' file.txt
```

Delete the last line in file \`\`\`shell script $ sed '$d' file.txt

```text
Delete lines starting with "Hello"
```shell script
$ sed '/^Hello/d' file.txt
```

Delete all empty lines \`\`\`shell script $ sed '/^$/d' file.txt

```text
Delete lines starting with "#"
```shell script
$ sed '/^#/d' file.txt
```

### File spacing

Double space \`\`\`shell script $ sed G

```text
Delete all blank lines and double space
```shell script
$ sed '/^$/d;G'
```

Triple space a file \`\`\`shell script $ sed 'G;G'

```text
Undo double-spacing
```shell script
$ sed 'n;d'
```

Insert a blank line above line which matches "regex" \`\`\`shell script $ sed '/regex/{x;p;x;}'

```text
Insert a blank line below line which matches "regex"
```shell script
$ sed '/regex/G'
```

Insert a blank line around line which matches "regex" \`\`\`shell script $ sed '/regex/{x;p;x;G;}'

\`\`\`

## See also {.cols-1}

* [sed cheatsheet](https://gist.github.com/ssstonebraker/6140154) _\(gist.github.com\)_

