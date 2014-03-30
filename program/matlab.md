# split the Xtrain, Ytrain, by Ytrain's value
```
iris=load('data/iris.txt');     % load the text file
X = iris(:,1:2); Y=iris(:,end); % get first two features
XA = X(Y<2,:); YA=Y(Y<2);       % get class 0 vs 1
XB = X(Y>0,:); YB=Y(Y>0);       % get class 1 vs 2
```

# left divide, right divide
```
X * C = Y 
==>
    C = X\Y
    X = Y/C
```

# Initial a string array
```
labels= cell(length(alphas),1);
for i= 1: length(labels)
    labels {i} = sprintf("string:%d", i);
end
```

# log scale X/Y axis
use `semilogx (X,Y)` to log scale X asix
use `semilogy (X,Y)` to log scale Y asix

# group X by Y and plot them
`gscatter(Xtr(:,1),Xtr(:,2),Ytr)`

