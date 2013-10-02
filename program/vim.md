# code style:
artistic style
    http://astyle.sourceforge.net/install.html

# auto indent
using "=" to format indent, wrap it with the range where to start and where to end

Here is the command to auto indent all

    gg=G
    
Here is the command to indent from the current line to 38th line
    
    =38

# using this vim-autoformat
https://github.com/Chiel92/vim-autoformat

# using cscope
```Bash
cscope -Rb  # at top level
```
In vim Ctrl+\s will list all the reference

## cmd of cscope list:
```bash
find . -name "*.h" -o -name "*.c" -o -name "*.cc" > cscope.files
cscope -bkq -i cscope.files
```
## input date:
```
:r !date
```
