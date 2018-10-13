## GR5293_A1

***
Name: yk2805_Patrick_kmeans.README
Subject: GR_5293 Assignment1
Date: 10-12-2018
Format: python 3.6
***

Required Packages:
- opencv-python
- numpy
- pandas

Required Parameters:
- None

Howto: after installing all packages, python yk2805_Patrick_kmeans.py 

Logic Structure:
1. Initialization
    1. Load the image to variable 'orig' 
      1. (orig = cv2.imread('./face_d2.jpg'))
      2. The dimension of image is loaded into variable 'shape' (300,251,3)
    2. Set the variable K (number of clusters) as 8.
    3. Display the original image for 5 seconds. (Name: 'Original')
2. Gaussian Filter
    1. Implement GaussianBlur with kernel size (5,5), store the result in variable 'ab'
      1. (ab = cv2.GaussianBlur(orig, (5,5), 0)
    2. For KMeans, reshape ab from a 3D matrix (300,250,3) to a 2D matrix (75300,3) 'Z'.
      1. (Z = np.float32(ab.reshape(-1,3)))
    3. Implement KMeans in Z, and get the results (variable 'ret', 'label', 'center')
      1. variable 'criteria': If 50 iterations has passed, or if accuracy of epsilon 0.05 is reached, stop.
        1. (criteria = (cv2.TERM_CRITERIA_EPS + cv2.TERM_CRITERIA_MAX_ITER, 50, 0.05))
      2. Initial centers are decided by opencv's pp_center algorithm. (Arthur2007)
      3. 10 attempts with different initial labeling will be performed.
      4. (ret, label, center = cv2.kmeans(Z, K, None, criteria, 10, cv2.KMEANS_PP_CENTERS))
      5. Results:
        1. variable 'label': label array for each pixels in Z.
        2. variable 'center': cluster center array.
    4. Reshape label to show the filtered & kmean image
      1. Convert the label array so that each pixel's color matches the cluster center's color.
        1. (img = np.uint8(center)\[label.flatten()\])
      2. Reshape the image and label according to 'shape'.
        1. (img = img.reshape((shape)), label = label.reshape((shape\[0\], shape\[1\])))
      
      
 
