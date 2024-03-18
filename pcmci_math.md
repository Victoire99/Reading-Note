# Related math 


### Gaussian kernel smoothing

#### smoothing

* data points are averaged with their neighbors in a series (time series or image)
* **mathematical definition**: estimate a real valued function as the weighted average of neighboring observed data, the weight is defined by the kernel.(closer points are given higher weights)
* smooth: the estimated function
* a type of weighted moving average
* Kernel: defines the shape of the function that is used to take the average of the neighborhood points.

#### Gaussian kernel

a shape of a gaussian(normal distribution) curve, b is the length scale for the input space

$$
K(x^*,x_i) = exp(-\frac{(x^*-x_i)^2}{2b^2})
$$
