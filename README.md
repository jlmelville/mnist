# mnist

mnist is an R package to download the 
[MNIST database](http://yann.lecun.com/exdb/mnist/), based on 
[a gist by Brendan O'Connor](https://gist.github.com/brendano/39760).

The entire dataset is returned as a single data frame. The first 60,000
instances are the training set, the remaining 10,000 the test set. The pixel
values (integers in the range 0-255) are in columns with name `px1`, `px2`,
`px3` etc. The label representing the numerical value of the digit is in the
`Label` column (which is stored as a factor).

Installing:
```R
# install.packages("devtools")
devtools::install_github("jlmelville/mnist")
library(mnist)
```

Using:
```R
# fetch the data set from the MNIST website
mnist <- download_mnist()

# view the fifth digit
show_digit(mnist, 5)

# first 60,000 instances are the training set
mnist_train <- head(mnist, 60000)
# the remaining 10,000 are the test set
mnist_test <- tail(mnist, 10000)

# PCA on 1000 random training examples
mnist_r1000 <- mnist_train[sample(nrow(mnist_train), 1000), ]

pca <- prcomp(mnist_r1000[, 1:784], retx = TRUE, .rank = 2)
# plot the scores of the first two components
plot(pca$x[, 1:2], type = 'n')
text(pca$x[, 1:2], labels = mnist_r1000$Label, cex = 0.5,
  col = rainbow(length(levels(mnist_r1000$Label)))[mnist_r1000$Label])

# save data set to disk
save(mnist, file = "mnist.Rda")
```

## License
This package is licensed under 
[the MIT License](http://opensource.org/licenses/MIT).

## See Also
[A similar project](https://github.com/xrobin/mnist) by 
[Xavier Robin](https://github.com/xrobin).

I have similar R packages for the 
[Simulation, Olivetti and Frey Faces](https://github.com/jlmelville/snedata) and
[COIL-20](https://github.com/jlmelville/coil20) datasets.
For doing an embedding, you could give 
[sneer](https://github.com/jlmelville/sneer) a go.
