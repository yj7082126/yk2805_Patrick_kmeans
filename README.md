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
    
2. Gaussian Filter & Kmeans
    1. Implement GaussianBlur with kernel size (5,5), store the result in variable 'ab'
        1. (ab = cv2.GaussianBlur(orig, (5,5), 0)
    2. For KMeans, reshape ab from a 3D matrix (300,250,3) to a 2D matrix (75300,3) 'Z'.
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
        2. Reshape the image and label according to 'shape'.
    5. Display the filtered & segmented image for 5 seconds. (Name: 'Kmean,Gfilter')
    
3. Get appropriate layer
    1. For selection of appropriate layer for face, we will define a function that will give the label color closest to caucassian skin color.
        1. Color used: (255, 205, 148) (https://www.color-hex.com/color-palette/737)
        2. The function 'close_to' will get a color pixel and return the 'distance' between the color and our caucassian skin color.
            1. def close_to(x, y, z):
                return np.sqrt(np.power(148-x, 2) 
                            + np.power(205-y, 2) 
                            + np.power(255-z, 2))  
    2. For each cluster, the function will give the distance of the cluster's color to our skin color, which will be stored in variable 'col_list'
    3. The variable 'k_layer' will have the index of the smallest value of 'col_list', which is the layer we are looking for.
    4. Store the pixels of k_layer in variable 'component'.
    5. Display the layer for 5 seconds. (Name: 'Layer' + str(k))
    
4. Get face boundary
    1. Convert all non-black pixels into 1 and others to 0, and store it in variable 'c1'
    2. From c1, get all non-blackk pixel's y and x data and store it in variable 'comp'
    3. Implement function 'get_boundary' that returns the min and max values for x and y in order to create a rectangle boundary.
      
      
 
