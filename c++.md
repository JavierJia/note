# install gcc 4.7

    http://solarianprogrammer.com/2012/04/13/building-gcc-4-7-on-ubuntu-12-04/

# google style
    http://google-styleguide.googlecode.com/svn/trunk/cppguide.xml

# build c++ library
    http://www.faqs.org/docs/Linux-HOWTO/Program-Library-HOWTO.html

# To build a lib:

    g++ file.cpp -o out.a -l somelib will dynamically link somelib, but also libc, libstdc++ etc

    g++ file.cpp -o out.a -l somelib -static will statically link everything.

# print time:
```c++
    #include <ctime>
    time_t     now = time(0);
    struct tm  tstruct;
    char       buf[80];
    tstruct = *localtime(&now);
    // Visit http://www.cplusplus.com/reference/clibrary/ctime/strftime/
    // for more information about date/time format
    strftime(buf, sizeof(buf), "%x %X", &tstruct);
```
