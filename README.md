# Kaiser-garamond window

In the research Finding the best methods for image scaling (https://github.com/garamond13/Finding-the-best-methods-for-image-scaling) I presented the garamond window. Now I will present the new derived window, the kaiser-garamond window.

The kaiser window \
w(x) = `x <= R ? I0(beta * sqrt(1.0 - x * x / (R * R))) / I0(beta) : 0.0`, where I0() is the modified bessel function of the first kind, (beta) is free parameter and R is the kernel radius. Note, division by I0(beta) is only for the normalization. \
at beta=0.0, w(x)=box window

The kaiser-garamond window \
w(x) = `x <= R ? I0(beta * sqrt(1.0 - pow(abs(x) / R, n))) / I0(beta) : 0.0`, where I0() is the modified bessel function of the first kind, (beta) is free parameter, n is free pramenter (n>=0), and R is the kernel radius. Note, division by I0(beta) is only for the normalization. \
at n=2.0, w(x)=kaiser window

It can approximate other windows, approxiations can be scaled to any radius. Here, I will show the test results of approximating some windows using the same settings for all kernels (base=sinc, kernel-blur=1.0, kernel-radius=5.0, antiringing=0.0, light=gamma). The test image, 960x540 will be upscaled to 1920x1080 (all test images were encoded into 4:4:4 video). The table below shows mesured differences in psnr (dB) between a native window and its kaiser-garamond approximation at some (beta) and (n).

| approximation | psnr |
| --- | --- |
| (lanczos) beta=4.5 n=2.2 | 59.9579 |
| (cosine) beta=3.9 n=2.3 | 57.9996 |
| (hann) beta=6.7 n=2.2 | 62.3053 |
| (blackman a=0.16) beta=8.6 n=2.0 | 69.0979 |

Now I will show test results of upscaling the same image as used above, with garamond window, kaiser window and kaiser garamond window. This time antiringing was used. Note, results may not be the very best achievable. (dssim is between the original image and the upscaled image)

| window | radius | dssim |
| --- | --- | --- |
| garamond n=3.5 | 2.5 | 0.0325759 |
| kasier beta=5.8 | 4.1 | 0.0328481 |
| kaiser-garamond beta=16.5 n=4.7 | 3.4 | 0.0325956 |

Note that this is not an extensive research by any means.
