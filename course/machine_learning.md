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
         * Minimum |data nodes| in parents ( before split). 

### SVM
* From the "better" boundary choose a "best" one
* Find a function to describe the "Best margin"
* "Support Vectors" : data points on margin
   * find margin: 
      * f(x) >= +1, for y(x) = +1
      * f(x) <= -1, for y(x) = -1
      * A lot of different parallel lines.
   * compute the maximum margin one
      * |W| is perpendicular to boundary
      * Choose x0, x1 as two point on the boundary that closest to each other
         * x1 = x0 + r * w ( r is the distance coefficient, W = rw is the Margin) 
      * Given 
         * W x0 + b = -1
         * W x1 + b = +1
         * Then 
         * W (x0 + r * W) + b = +1
         * ==> r = 2/ ||w||^2
         * M = r w = 2 / \sqrt (W^T * W)
         * w = argmin \sum w_j^2
      * Constrained argmin problem.
   
### Linear regression
* Linear function : Y = \theta * X
* gradient descent 
   * MSE: J = 1/m \sum ( y - y^hat ) ^2
   * J -= \alpha * derivative J 
   * For all the data X ( m*f)
      * delta J = 2/m ( Y' - \theta X[M,F]) X[M,F]
* Very general 
* Local minimal
* Need to choose a better Step size
* Online gradient descent
   * Update on each data I
   * Faster, update on each value
   * Not strict "desent"

* 



