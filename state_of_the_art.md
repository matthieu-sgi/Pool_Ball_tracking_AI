# **State of the art : Computer vision**

## Python

### Without IA

I found differents ways to detect object. These aren't really opposite, they can be added to have a better detection.

First of all, we can use edges detection. This technic allows use to get the edges of objects visible on the image. It is only an edge detection matrix. It can work better on a grayscale image (maybe even only on a grayscale image).

You can use the Canny algorithm to detect edges. It is a very famous algorithm. It is based on the Sobel algorithm. It is a multi-step algorithm. First, it applies a Gaussian filter to the image to remove the noise. Then, it calculates the intensity gradients of the image. After that, it applies non-maximum suppression to get rid of spurious response to edge detection. Finally, it applies double threshold to determine potential edges. The first threshold is used to determine the strong edges. The second threshold is used to determine the weak edges. The weak edges are kept only if they are connected to strong edges. The output edges are the connected, strong edges.

