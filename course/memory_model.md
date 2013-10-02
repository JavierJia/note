# Resources
http://www.ics.uci.edu/~guoqingx/courses/295/fall13/

## L1 cache is used by one core. L2 cache is shared by multiple cores inside one Processor

* Memory consistency models
* Cache consistency models

## Reading of Chapter 3 Memory consistency
* Problem: out-of-order execution in one core will confusing condition statement in other cores.
    * Reordering reason: 
        * Store-store reordering: the later one may have better chance to hit the cache. 
        * Load-load reordering
        * Load-store 
* Memory Consistency model --> MC model
* Sequential consistency
* conherence 
    
