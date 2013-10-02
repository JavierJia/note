# Good reference
Brief one: http://www.ntu.edu.sg/home/ehchua/programming/cpp/gcc_make.html

# Automatic Variables
Automatic Variables
Automatic variables are set by make after a rule is matched. There include:
    $@: the target filename.
    $*: the target filename without the file extension.
    $<: the first prerequisite filename.
    $^: the filenames of all the prerequisites, separated by spaces, discard duplicates.
    $+: similar to $^, but includes duplicates.
    $?: the names of all prerequisites that are newer than the target, separated by spaces.
