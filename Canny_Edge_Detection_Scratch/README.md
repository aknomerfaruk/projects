Canny detection algorithm:
1. **Noise reduction.** To remove noise, the image is smoothed by Gaussian blur with the ![sigma](https://latex.codecogs.com/gif.latex?%5Csigma%20%3D%201.4). The sum of the elements in the Gaussian kernel equals 1. <br><br>

2. **Calculating gradients.** When the image I is smoothed, the derivatives ![g_x](https://latex.codecogs.com/gif.latex?G_x) and ![g_y](https://latex.codecogs.com/gif.latex?G_y) w.r.t. x and y are calculated. It can be implemented by convolving I with Sobel kernels ![K_x](https://latex.codecogs.com/gif.latex?K_x) and ![K_y](https://latex.codecogs.com/gif.latex?K_y), respectively: 

![sobel_filters](https://latex.codecogs.com/gif.latex?K_x%20%3D%20%5Cbegin%7Bpmatrix%7D%20-1%20%26%200%20%26%201%20%5C%5C%20-2%20%26%200%20%26%202%20%5C%5C%20-1%20%26%200%20%26%201%20%5Cend%7Bpmatrix%7D%2C%20K_y%20%3D%20%5Cbegin%7Bpmatrix%7D%201%20%26%202%20%26%201%20%5C%5C%200%20%26%200%20%26%200%20%5C%5C%20-1%20%26%20-2%20%26%20-1%20%5Cend%7Bpmatrix%7D.)

Then, the magnitude G and the slope ![theta](https://latex.codecogs.com/gif.latex?%5Ctheta) of the gradient are calculated:
![magnitude](https://latex.codecogs.com/gif.latex?%7CG%7C%20%3D%20%5Csqrt%7BI_x%5E2%20&plus;%20I_y%5E2%7D%2C)
![angle](https://latex.codecogs.com/gif.latex?%5Ctheta%28x%2Cy%29%20%3D%20arctan%5Cleft%28%5Cfrac%7BI_y%7D%7BI_x%7D%5Cright%29)
<br><br>

3. **Non-maximum suppression.** For each pixel find two adjacent pixels. If the magnitude of the current pixel is greater than the magnitudes of the adjacents, nothing changes, otherwise, the magnitude of the current pixel is set to zero.<br><br>

4. **Double threshold.** The gradient magnitudes are compared with two specified threshold values. The gradients that are smaller than the low threshold value are suppressed (setting to 0); the gradients higher than the high threshold value are marked as strong ones and the corresponding pixels are included in the final edge map. All the rest gradients are marked as weak ones and pixels corresponding to these gradients are considered in the next step.<br><br>

5. **Edge tracking by hysteresis.** Since a weak edge pixel caused from true edges will be connected to a strong edge pixel, pixel w with weak gradient is marked as edge and included in the final edge map if and only if it is involved in the same blob (connected component) as some pixel s with strong gradient. In other words, there should be a chain of neighbor weak pixels connecting w and s (the neighbors are 8 pixels around the considered one).
