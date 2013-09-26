# Range Search for Decomposable operator
Using key to index the binary tree, pre decomposed the value of each node
    
    Query( T, L, R):
        if T < L :
            return Query(T.right, L, R)
        if T > R :
            return Query(T.left, L, R)
        if R == +inf: // all T.right do not need to visit
            return value(T) op Query(T.left, L, +inf) op value(T.right)
        if L == -inf: // all T.left do not need to visit
            return value(T) op Query(T.right, -inf, R) op value(T.left)
        return value(T) op Query(T.left, L, +inf) op Query(T.right, -inf, R)) 

# Range min
Given an array A and a range [i,j], return the min value of A[x] in this array
## Binary search tree
Value stored in the leaves, build the extra min node as a binary tree.

Each node store the min of the 2 children, and the range of this node.

Space O(2n), speed O(logn)

    RangeMin(T, l, r):
        if T.range out of [l,r]
            return null
        if T.range in [l,r]:
            return T.value
        return min(RangeMin(T.left, l, min(r, T.left.r)),
                   RangeMin(T.right, min(l, T.right.l), r))
        
## Using search table U[i,k]
This search table store the min value of the array from index i to index i+2^k;

query: 
    let $q = floor( log (j-i+1))
    return min ( U[i,q], U[j-2^q, q])
    
Space O(2n), speed O(1)

# Cartesian tree of a tree
It's a binary tree. Each time find a min edge to be a new node of the Cartesian tree, at the same time split the original tree using this edge

# Invertable Bloom Filter
Invertable : can list the items. ( in some probablity)

    Make sum of all key, then wait for some part that |sum|==1, 
    Then we can delete it from the sum, sum--, then there will be
    another sum==1 ... until to very end.

# Fibonacci Heap
Marked node: this node has been delete a child, next time the deletion of it child will split it from the root.
