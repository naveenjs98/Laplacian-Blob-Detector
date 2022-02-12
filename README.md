# Laplacian-Blob-Detector

## Step 1: Laplacian of Gaussian Filter
Laplacian filters are used to find edges (areas of rapid intensity changes). In practice, the first derivative Laplacian operator is very sensitive to noise. To remove the effects of noise, the image is smoothened using a Gaussian filter which is then followed by a Laplacian filter.
The formula for Laplacian of Gaussian operation can be found here https://academic.mu.edu/phys/matthysd/web226/Lab02.htm


## Step 2: Build a Laplacian Scale Space, starting with some initial scale and going for n iterations
Filter image with scale-normalized Laplacian at current scale.
We use the above function to generate a Laplacian scale of filters which are then convoluted with the original image to generate scale space.
Save the square of the Laplacian response for the current level of scale space.
We square the convoluted image space in order to convert the negative values to positive values and store it in the scale space.
Increase scale by a factor 𝑘.
The above steps are performed n number of times to create Laplacian scale space with different sigma values. The standard deviation for the nth level is taken as sigma*k^n and the size of each of the filters depends on the standard deviation calculated using the formula sigma*k^n

## Step 3: Perform non-maximum suppression
Non-max suppression is performed in each level of the scale space by analyzing the neighbors of all the elements.

## Step 4: Display resulting circles at their characteristic scales
The blobs have been displayed using circles. The centers of these circles are the points at which the blobs were detected and the radius of the said circle is given by the level of scale space.

## PARAMETERS ASSUMED:
* s (sigma) :  Standard deviation is a representation of the radius of the LoG filter. We varied the values from 0.5 to 1.5 and chose 1.15 as our final sigma value. If the sigma is too low, then we tend to identify too many local blobs and if the sigma is too high then we miss out on a lot of blobs.
* K : Constant multiplier. Chosen to be 1.24
* Threshold :  To detect the maxima. Varied values from 0.005 to 0.05. Chose 0.01 as it gave the optimal values and speed.
* We chose the size of laplacian space as 15 so as to strike a balance between the size of the blobs and the computation time.
