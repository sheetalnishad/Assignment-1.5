Create an m x n matrix with replicate(m, rnorm(n)) with m=10 column vectors of n=10 elements each,
constructed with rnorm(n), which creates random normal numbers.
Then we transform it into a dataframe (thus 10 observations of 10 variables) and perform an algebraic
operation on each element using a nested for loop: at each iteration, every element referred by the two
indexes is incremented by a sinusoidal function, compare the vectorized and non-vectorized form of
creating
the solution and report the system time differences.
Ans.
m &lt;- replicate(10, rnorm(10), simplify = &quot;matrix&quot;) # matrix 10 x 10 with random normal numbers
m
m &lt;- as.data.frame(m) # transforming into data frame
View(m)

library(rbenchmark)
benchmark(
vect = as.vector(m), # vecotrized form
conc = (n &lt;- as.vector(for (i in seq(nrow(m))) {
for (j in seq(ncol(m))) { # nested for
print(2*sin(m[i, j])) # performing algebraic function on each element
}
}))
)
