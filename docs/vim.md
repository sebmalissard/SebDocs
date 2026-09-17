# Vim

## Entering command mode
```[Esc]``` Exit editing mode. Keyboard keys now interpreted as commands.

## Moving the cursor
```h (or left arrow key)``` Move the cursor left.  
```l (or right arrow key)``` Move the cursor right.  
```j (or down arrow key)``` Move the cursor down.  
```k (or up arrow key)``` Move the cursor up.  
```[Ctrl] + f``` Move the cursor one page forward .  
```[Ctrl] + b``` Move the cursor one page backward.  
```^``` Move cursor to the first non-white character in the current line.  
```$``` Move the cursor to the end of the current line.  
```G``` Go to the last line in the file.  
```nG``` Go to line number ```n```.  
```[Ctrl] + G``` Display the name of the current file and the cursor position in it.

## Entering editing mode
```i``` Insert new text before the cursor.  
```a``` Append new text after the cursor.  
```o``` Start to edit a new line after the current one.  
```O``` Start to edit a new line before the current one.  

## Replacing characters, lines and words
```r``` Replace the current character (does not enter edit mode).  
```s``` Enter edit mode and substitute the current character by several
ones.  
```cw``` Enter edit mode and change the word after the cursor.  
```C``` Enter edit mode and change the rest of the line after the cursor.  

## Copying and pasting
```yy``` Copy (yank) the current line to the copy/paste buffer.  
```p``` Paste the copy/paste buffer after the current line.  
```P``` Paste the copy/paste buffer before the current line.  

## Deleting characters, words and lines
All deleted characters, words and lines are copied to the copy/paste
buffer.

```x``` Delete the character at the cursor location.
```dw``` Delete the current word.
```D``` Delete the remainder of the line after the cursor.
```dd``` Delete the current line.

## Repeating commands
```.``` Repeat the last insertion, replacement or delete command.

## Looking for strings
```/string``` Find the first occurrence of string after the cursor.  
```?string``` Find the first occurrence of string before the cursor.  
```n``` Find the next occurrence in the last search.

## Replacing strings
Can also be done manually, searching and replacing once, and then using ```n``` (next occurrence) and ```.``` (repeat last edit).

```n,ps/str1/str2/g``` Between line numbers ```n``` and ```p```, substitute all (```g```: global) occurrences of ```str1``` by ```str2```.  
```1,$s/str1/str2/g``` In the whole file (```$```: last line), substitute all occurrences of ```str1``` by ```str2```.  

## Applying a command several times - Examples
```5j``` Move the cursor 5 lines down.  
```30dd``` Delete 30 lines.  
```4cw``` Change 4 words from the cursor.  
```1G``` Go to the first line in the file.

## Misc
```[Ctrl] + l``` Redraw the screen.  
```J``` Join the current line with the next one.  
```u``` Undo the last action.

## Exiting and saving
```ZZ``` Save current file and exit vi.  
```:w``` Write (save) to the current file.  
```:w file``` Write (save) to the ```file``` file.  
```:q!``` Quit vi without saving changes.