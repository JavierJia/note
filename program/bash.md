# find some files

    find $directory -type f -name "*.in"

# find and replace some part in those files

    find ../src -type f -name "*.cpp" -exec sed -i 's/"util\/Log.h"/"util\/Logger.h"/g' {} \;

# find and grep show file name and lines:

    find ../src/ -type f -name "*.h" -exec grep -Hn "cout" {} \;

# String Manipulate
## replace
replace only first match
```
${string/pattern/replacement}
```
replace all the matches
```
${string//pattern/replacement}
```
