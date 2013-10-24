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
## accurate time:
http://stackoverflow.com/questions/588307/c-obtaining-milliseconds-time-on-linux-clock-doesnt-seem-to-work-properl
```c++
#include <sys/time.h>
void start(){
    gettimeofday(&startTime, NULL);
}

double stop(){
    timeval endTime;
    long seconds, useconds;
    double duration;

    gettimeofday(&endTime, NULL);

    seconds  = endTime.tv_sec  - startTime.tv_sec;
    useconds = endTime.tv_usec - startTime.tv_usec;

    duration = seconds + useconds/1000000.0;

    return duration;
}
```

# trace mem usage:
a brilliant blog: http://stackoverflow.com/questions/63166/how-to-determine-cpu-and-memory-consumption-from-inside-a-process

Virtual Memory currently used by current process:
```c++
#include "stdlib.h"
#include "stdio.h"
#include "string.h"


int parseLine(char* line){
    int i = strlen(line);
    while (*line < '0' || *line > '9') line++;
    line[i-3] = '\0';
    i = atoi(line);
    return i;
}


//Virtual Memory currently used by current process
int getValue(){ //Note: this value is in KB!
    FILE* file = fopen("/proc/self/status", "r");
    int result = -1;
    char line[128];


    while (fgets(line, 128, file) != NULL){
        if (strncmp(line, "VmSize:", 7) == 0){
            result = parseLine(line);
            break;
        }
    }
    fclose(file);
    return result;
}

//Physical Memory currently used by current process:
int getValue(){ //Note: this value is in KB!
    FILE* file = fopen("/proc/self/status", "r");
    int result = -1;
    char line[128];


    while (fgets(line, 128, file) != NULL){
        if (strncmp(line, "VmRSS:", 6) == 0){
            result = parseLine(line);
            break;
        }
    }
    fclose(file);
    return result;
}
```

# Valgra
valgrind --tool=memcheck ./a.out

manule of memcheck:
http://valgrind.org/docs/manual/mc-manual.html

