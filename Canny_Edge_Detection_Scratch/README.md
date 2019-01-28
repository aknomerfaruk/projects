Canny detection algorithm:
1. **Noise reduction.** To remove noise, the image is smoothed by Gaussian blur with the ![sigma](https://latex.codecogs.com/gif.latex?%5Csigma%20%3D%201.4). The sum of the elements in the Gaussian kernel equals $1$. <br><br>

2. **Calculating gradients.** When the image $I$ is smoothed, the derivatives ![g_x](https://latex.codecogs.com/gif.latex?G_x) and ![g_y](https://latex.codecogs.com/gif.latex?G_y) w.r.t. x and y are calculated. It can be implemented by convolving I with Sobel kernels ![K_x](https://latex.codecogs.com/gif.latex?K_x) and ![K_y](https://latex.codecogs.com/gif.latex?K_y), respectively: 
$$ K_x = \begin{pmatrix} -1 & 0 & 1 \\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{pmatrix}, K_y = \begin{pmatrix} 1 & 2 & 1 \\ 0 & 0 & 0 \\ -1 & -2 & -1 \end{pmatrix}. $$ 
Then, the magnitude $G$ and the slope $\theta$ of the gradient are calculated:
$$ |G| = \sqrt{I_x^2 + I_y^2}, $$
$$ \theta(x,y) = arctan\left(\frac{I_y}{I_x}\right)$$<br><br>

3. **Non-maximum suppression.** For each pixel find two adjacent pixels. If the magnitude of the current pixel is greater than the magnitudes of the adjacents, nothing changes, otherwise, the magnitude of the current pixel is set to zero.<br><br>

4. **Double threshold.** The gradient magnitudes are compared with two specified threshold values. The gradients that are smaller than the low threshold value are suppressed (setting to 0); the gradients higher than the high threshold value are marked as strong ones and the corresponding pixels are included in the final edge map. All the rest gradients are marked as weak ones and pixels corresponding to these gradients are considered in the next step.<br><br>

5. **Edge tracking by hysteresis.** Since a weak edge pixel caused from true edges will be connected to a strong edge pixel, pixel $w$ with weak gradient is marked as edge and included in the final edge map if and only if it is involved in the same blob (connected component) as some pixel $s$ with strong gradient. In other words, there should be a chain of neighbor weak pixels connecting $w$ and $s$ (the neighbors are 8 pixels around the considered one).
