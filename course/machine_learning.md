# Machine Learning note

* [2013 Fall syllable](http://sli.ics.uci.edu/Classes/2013F-273a)
* [2012 Fall syllable](http://sli.ics.uci.edu/Classes/2012F-273a)
* [Alex Ihler](http://www.ics.uci.edu/~ihler/)
* [Piazza](https://piazza.com/class/hlr1ws3vto25yy)
* [Project](http://www.kaggle.com/)
* [Octave](http://www.gnu.org/software/octave/support.html)
## Thu Sep 26 13:57:23 PDT 2013

* Supervised
    * Regression vs Classification
* Unsupervised
* Semi-Supervised
* Reinforcement


Overfitting : 
good at training data, bad at test data

## Tue Oct  1 14:05:50 PDT 2013
K Nearest Neighbor

*Regression
*Classification

Y = (Σ y of nearest_set(x))/ K

The bigger the K is, the smooth the Y it is. But if K is too big, Y will be too far away from the training data.

### locality weighted variant:
Give the nearer neighbor higher weight.


## Midterm review
### K-NN
* In general: Nearest-neighbor classifier produces piecewise linear decision boundaries
* Regression: Avg( yi in |y|^k)
* Classification: Vote in sign (K)
* Increasing K : less emphasis on individual points
* Extensions:
   * weighted distance , the nearer point have more vote

### Bayes 
* P(y|x) => P(x|y)P(y)
* Multiple valuse lead to a full combination of values, is the overfiting case in Bayes model
* If the features are indepedent of each other => Naive bayes model

### Decision trees
* Multiple children VS binary tree
* "Complexity": depth
* Regression: change the leaf value from class label to real value
* Learning:
   * Leaf node
      * Classification: choose the majority
      * Regression: avg value
   * Non-leaf node
   * Learning score:
      * Information gain
   * Stop criteria:
      * Information gain threshold ? Not a good idea
      * Grow a large tree and then prune back. ( How to ? )
      * Other controls
         * Maximum depth
         * Minimum # parent data




