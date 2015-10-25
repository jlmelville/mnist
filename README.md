# mnist

mnist is an R package to download the [MNIST database](http://yann.lecun.com/exdb/mnist/), based on 
[a gist by Brendan O'Connor](https://gist.github.com/brendano/39760).

The entire dataset is returned as a single data frame. The first 60,000
instances are the training set, the remaining 10,000 the test set. The pixel
values (integers in the range 0-255) are in columns with name `px1`, `px2`,
`px3` etc. The label representing the numerical value of the digit is in the
`Label` column (which is stored as a factor).

Installing:
```R
install.packages("devtools")
devtools::install_github("jlmelville/mnist")
```

Using:
```R
# fetch the data set from the MNIST website
mnist <- parse_mnist()

# view the fifth digit
show_digit(mnist, 5)

# first 60,000 instances are the training set
mnist_train <- head(mnist, 60000)
# the remaining 10,000 are the test set
mnist_test <- tail(mnist, 10000)

# PCA on 1000 random training examples
mnist_r1000 <- mnist_train[sample(nrow(mnist_train), 1000), ]
pca <- princomp(mnist_r1000[,1:784], scores = TRUE)
# plot the scores of the first two components
plot(pca$scores[,1:2], t='n')
text(pca$scores[,1:2], labels = mnist_r1000$Label, 
     col = rainbow(length(levels(mnist_r1000$Label)))[mnist_r1000$Label])

# save data set to disk
save(mnist, file = "mnist.Rda")
```

## License
This package is licensed under [the MIT License](http://opensource.org/licenses/MIT).

## See Also
[A similar project](https://github.com/xrobin/mnist) by [Xavier Robin](https://github.com/xrobin).
