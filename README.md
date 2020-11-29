<h1>Multi Threaded Proxy Server with and without Cache</h1>

This project is implemented using `C` and Parsing of HTTP referred from <a href = "https://github.com/vaibhavnaagar/proxy-server"> Proxy Server </a>


## Index

- [Project Theory](https://github.com/Lovepreet-Singh-LPSK/MultiThreadedProxyServerClient#project-theory)
- [How to Run](https://github.com/Lovepreet-Singh-LPSK/MultiThreadedProxyServerClient#How-to-Run)
- [Demo](https://github.com/Lovepreet-Singh-LPSK/MultiThreadedProxyServerClient#Demo)
- [Contributing](https://github.com/Lovepreet-Singh-LPSK/MultiThreadedProxyServerClient#contributing)

## Project Theory

[[Back to top]](https://github.com/Lovepreet-Singh-LPSK/MultiThreadedProxyServerClient#index)

##### Introduction
Face Recognition is a process of face detection and then classifying the faces into different classes. The methods used in this case are based on the application of Viola-Jones, for detecting the face using cascade classifier, and Eigen Faces algorithm, for face classification and it is based on the PCA algorithm. PCA is known as Principal component analysis which in other words is feature reduction or dimensionality reduction algorithm.

##### Basic Working Flow of the Proxy Server:
![](https://github.com/Lovepreet-Singh-LPSK/MultiThreadedProxyServerClient/pics/UML.JPG)

##### How did we implement Multi-threading?
- Used Semaphore instead of Condition Variables and pthread_join() and pthread_exit() function. 
- pthread_join() requires us to pass the thread id of the the thread to wait for. 
- Semaphore’s sem_wait() and sem_post() doesn’t need any parameter. So it is a better option. 


##### Motivation/Need of Project
- To Understand → 
  - The working of requests from our local computer to the server.
  - The handling of multiple client requests from various clients.
  - Locking procedure for concurrency.
  - The concept of cache and its different functions that might be used by browsers.
- Proxy Server do → 
  - It speeds up the process and reduces the traffic on the server side.
  - It can be used to restrict user from accessing specific websites.
  - A good proxy will change the IP such that the server wouldn’t know about the client who sent the request.
  - Changes can be made in Proxy to encrypt the requests, to stop anyone accessing the request illegally from your client.
 
##### OS Component Used ​
- Threading
- Locks 
- Semaphore
- Cache (LRU algorithm is used in it)

##### Limitations ​
- If a URL opens multiple clients itself, then our cache will store each client’s response as a separate element in the linked list. So, during retrieval from the cache, only a chunk of response will be send and the website will not open
- Fixed size of cache element, so big websites may not be stored in cache. 

##### How this project can be extended? ​
- This code can be implemented using multiprocessing that can speed up the process with parallelism.
- We can decide which type of websites should be allowed by extending the code.
- We can implement requests like POST with this code.


# Note :-
- Code is well commented. For any doubt you can refer to the comments.

![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/haarlike.png)

These features help the machine to understand the features of the image. For.ex. The edge feature has a one-sided dark and the other is light, This filter is, therefore, good at edge detection like the nose, lips line, etc. To obtain the feature value these features are placed over the region in the sliding rectangle and the sum in the light region is subtracted from the sum of pixels in the dark region.
##### Haar-Like Features application:→

![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/haar-app.png)   
![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/haar-app1.png)

##### Integral Image:→
![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/ii.png)
​Integral image is used to obtain the values of Haar-like feature values because otherwise, it is computationally very expensive to calculate it, because of the large number of image pixels.
##### Training:→
The algorithm in training is setting a minimum threshold to determine whether something can be classified as a feature or not. The computation can be really expensive depending on the different possible combinations of features for each region of the sliding rectangle.
![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/cascade.png)

For each region, a linear combination of the weak classifiers(on the right) is obtained toform a strong classifier(on the left). AdaBoost is used forthis task. Adaboost works like,first we classify images using important feature acc. to us. The images for whichclassification is the wrong Adaboost uses another feature to classify wrong classified images, giving more importance to the wrong classified images. In other words, increasing the weight for these images in the overall algorithm. Similarly, we will go for the next feature and at last giving larger weight to the last image. Thus Adaboost forms the classifier from these Weak classifiers.
- Cascading:→
​It is a hack to increase the speed and accuracy of Boosting. 
![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/cascade-window.png)
The feature is looked in the sub-window on the image and if Feature-i (Fi) is not present in this window then that sub-window is rejected and the process stopped for that window thus preventing further checking of the features. Since we have to do it for each feature it may be slow without Cascading.

##### How the Eigen-Faces algorithm classifies the Faces ​ (All images are obtained from my code of Facial Recognition*)​ :
##### Training:→
- 1.) ​ Suppose we have M images of dimensions NxN.

![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/faces1.png) 
![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/faces2.png)

- 2.) Then the images are flattened and stored into an array of ​ images​ .
- 3.) Now, we calculate the average of all the images with shape (N​ *N,1). This average image is the so-called average face.

![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/avg.png) 

- 4.) Now, this average image is subtracted from all the Images to obtain a difference matrix.
- 5.) The shape of the difference matrix is (N*N, M).
- 6.) Now, the Covariance matrix is obtained from the difference matrix by multiplying its transpose with itself.
- 7.) The eigenvectors and eigenvalues of the matrix are obtained. Eigenvectors will determine the direction of maximum variability in the space. Therefore, top k eigenvectors are picked up from the obtained vectors by using the eigenvalues.

- The eigenvectors (eigenfaces in this case) obtained are:

![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/eigfaces1.png) 
![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/eigfaces2.png)

- 8.) Then, Training images are expressed as the linear combination of these top K eigenfaces. Weights for each image are stored in a weight array.

- Testing: ​ Now, for testing an image, the image is flattened and the average face of training images is subtracted. Then weights for the test image are obtained. Then the distance of the weights of the test image is calculated from the weights of the training images. The label corresponding to the training image, from which the distance of weights is minimum, is given to the test image and thus the image is classified.

- Results and Observations : ​ (Images are classified with Label too in the code*)
![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/test.png) 

The algorithm is tested on different values of K i.e. no. of eigenfaces to be taken for linear combination. The graph I got is:

![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/graph_acc.png) 

Although, Graph changes with each run of the algorithm because of random shuffling of images and thus splitting into training and testing sets. But in all graphs, it can be seen that the algorithm performs fairly good even on a small no. of images for the value of k which is between k=5 and k=80. It can be observed that Algorithm accuracy got peaks at some values of K and give almost the same performance at higher values of K.

**NOTE** `Further in more detail is explained within the code`

## Train your own Haar-Cascade Classifier

[[Back to top]](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition#index)

**NOTE** Haar-Cascade classifier training is done using OpenCV methods `opencv_createsamples`, `opencv_traincascade`. But These methods aren't available in the Opencv which is installed using `python`. So, First we need to install full version of Opencv, using `CMake`, to utilize the functions for training.

#### Steps to follow to install Full-OpenCV:
- 1.) <a href = "https://cmake.org/install/">Install CMake-Gui on Windows/Linux</a>
- 2.) Clone OpenCV repo:
```bash
$ git clone https://github.com/opencv/opencv.git
$ mkdir build
$ cmake-gui
```
- 3.) Now CMake-Gui will be opened like:

![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/cmake.png) 

- 4.) Select Source Code Directory in Cmake-Gui to the directory of OpenCV cloned folder (Created In Step 2).
- 5.) Select Build Binaries Directory in Cmake-Gui to the directory build we created (Created In Step 2).
- 6.) Select Configure in Cmake-build and select Visual Studio in the dropdown menu (I selected Sublime in the Pic):

![](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/pics/bin.png) 

- 7.) Now, Press Generate to generate the files in the build directory.
- 8.) Go to the directory build now (build created in step 2).
- 7.) Now, Search for `createsamples` in this directory and open the location of the `createsamples`.

#### Training Classifier:

**NOTE** Now `opencv_createsamples` and `opencv_traincascade` is available to use in the build directory somewhere(You can search).

- 1.) Create Positive and Negative Images for training.

**NOTE** Positive images will contain faces (In face recognition) and negative images will contain images having no face.
- 2.) Label the positive images using <a href="https://www.makesense.ai/">MakeSense.Ai</a>.
- 3.) After Labelling all the positive images manually you will get a csv file like <a href = "https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/blob/master/yalefaces/yalefaces.csv">CSV File</a>
- 4.) Now, create a txt file for negative images contating names of the negative images only.
**NOTE** CSV file for positive images also contain the labels of the image. OpenCV training cascade doesn't require it. So, make sure that csv file contatins the row enteries like `pos/pos-1.pgm 2 0 0 100 40 1 1 80 60`. where `pos/pos-1.pgm` is the path of the image, In `2 0 0 100 40 1 1 80 60` Where `2` is the no. of faces and from `0 0 100 40` `0 0` as Top left coordinate of the rectangle drawn around face using `MakeSense.Ai` and `100 40` is the width and height of the rectangle. All of this information will be extracted automatically from `MakeSense.Ai`. Only make the order as `path num_objects x y w h` for CSV file.
- 5.) Now we have positive images and negative images with their CSV and txt(containing path of the -ve images only) files respectively.
- 6.) Now, run `opencv_createsamples -info yalefaces.info -num 550 -w 48 -h 24 -vec yalefaces.vec`. MakeSure you have conerted .csv file to .info file.
- 7.) Now, run `opencv_createsamples -vec yalefaces.vec -w 48 -h 24`.
- 8.) Now, run `opencv_traincascade -data data -vec yalefaces.vec -bg negative.txt -numPos 500 -numNeg 500 -numStages 10 -w 48 -h 24 -featureType LBP`.
- 9.) Now in our data folder, we have cascade.xml , which is our final cascade and can be used for face detection. It also contains stage wise xml files after each stage. In my case i trained a HOG-feature classifier which can be found in <a href = "https://github.com/Lovepreet-Singh-LPSK/Face-Recognition/tree/master/trained_model_yalefaces_HOG">Cascade Classifier</a>

**NOTE** Now to use your own classifier for face detection use `cascade.xml` file in the method of:

`import cv2`
`face_cascade = cv2.CascadeClassifier('cascade.xml')`

## Contributing

[[Back to top]](https://github.com/Lovepreet-Singh-LPSK/Face-Recognition#index)

Feel free to add some useful. 

**NOTE** A great IDEA ~~ U can Implement on large dataset and implement in real-time. We can do it together, Just contact on `lpsk5713@gmail.com` or `lovepreetsingh786kota@gmail.com`.

#### Enjoy CODE and pull requests are highly appreciated.