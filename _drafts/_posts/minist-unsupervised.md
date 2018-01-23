---
title: Minist Unsupervised
date: 2018-01-23 19:01:46 +0000
label: Unsupervised Learning with MINIST
---
 **Handwritten Digits** 

Handwritten dataset is made up of 1797 8x8 images. Each image is of a handwritten digit.. In order to utilize the 8 X 8 image it’s transformed into a feature vector of length 64. M o r e i n f o r m a t i o n o n t h e d a t a s e t c a n b e f o u n d h e r e 

Because of the visual nature of it, it is an interesting dataset for the purpose of this assignment. It’s easier to visualise and identify clusters, also it’s much easier to compare the similarity or differences between different clusters or instances by merely looking at the picture of instances. Digit identification information is also available with the dataset which makes it easy to compare different clustering algorithms based on ground truth. The handwritten digits also have some level of ambiguity which makes it difficult for some of the instances to be assigned to the right cluster and helps in bringing out the differences in algorithms. 

The dataset contains the digit associated with the image, but this information is not used in clustering. However I’ve used this value for benchmarking or comparing the algorithms. 

**Clustering** 

The images are first clustered without the dimensionality reduction on the dataset. Then we use dimensionality reduction algorithms. 

To decide the value of number of clusters K, I’ve plotted the sum of distances of samples to their closest cluster centers with increasing number of cluster. 

We can see that there’s not a significant reduction in error after 10, and also since we know the actual number of classes in the dataset as being 10 we choose the value of k as 10. 

**Without dimensionality Reduction** 

**K-means** 

Because of how K-means work it can converge to local mima and initial set of clusters could greatly affect the final clustering. Scikit library has built in implementation to mitigate this by trying several initial sets and select the one with the minimum values of the sum of squared distance between the cluster centers. 

2 

10 images from two of the clusters are shown below ( note that the label do not indicate the actual digits they are just the cluster numbers assigned by the algorithm): 

**Expectation Maximization** 

Two of the clusters from expectation maximization algorithm are given below, we can see that the similar digits are clustered together however some digits are also clustered incorrectly. For examples there’s a 4 in the first cluster while all the other digits seem to be 7. Second cluster has a 3 and a 8 along with all 9s. 

To compare the the two algorithms I’ve split the dataset into training and testing set with 0.25 split. clusters labels are compared with actual labels using adjusted rand score. This is repeated 10 times to average out any anomalies. E xpectation maximisation is found to perform better than K-means with a mean ARI score of 0.72 as compared to 0.68 of k-means. 

The difference in the performance can be a attributed to the way K-means and EM do the cluster assignment. If we look at the incorrectly clustered digits most of them are the ones which resembles another digit closely. For example 9 and 3. K-means does the hard clustering based on L2 norm while EM assigns the clusters based on expectation which seems to perform better in this case. 

3 

kmeans (left) EM (right) 

Some of the assigned cluster boundaries are almost similar for both the algorithms but some are drastically different. This can be seen in the classification as well. EM have classified some of 3 similar to 9 while K-means mostly grouped some of 1 and 4s together. 

**Dimensionality Reduction** 

Dimensionality reduction algorithms PCA, ICA, Randomized Projections and LDA are applied and a scatter plot is plotted comparing showing the scatter of instance variables against two most prominent components. \[ Principal components in case of PCA and LDA\] 

4 

PCA and LDA seems to capture a lot of information that separates out the clusters in the first two principal components . Linear Discriminant Analysis (LDA) tries to identify attributes that account for the most variance between classes. In particular, LDA, in contrast to PCA, is a supervised method, using known class labels. ICA in general is useful for separating out the superimposed signals, however in this dataset there is no obvious additive subcomponents that are maximally independent and so ICA doesn’t seem to capture anything of particular importance. 

On comparing the explained variance ratio for PCA  it’s found that the first first three component account for about 65% of variance. To get a sense of how information is captured in reduced data sets the first 8 PCA reduced components are shown below. 

The first component plot seems to be highlighting the digit 3 and 4. This also corroborates with the scatter plot where the first principal component is key to separating the digits 4 and 3. The second component seems to be highlighting the digit 0. 

The performance of K-means and EM are compared on the reduced datasets and results are recorded below. 

5 

| --- | --- | --- | --- | --- | --- | --- |
|  							 								 									Algo  								 							 						 |  							 								 									dataset  								 							 						 |  							 								 									homogen eity  								 							 						 |  							 								 									complete ness  								 							 						 |  							 								 									v- measure  								 							 						 |  							 								 									adjusted rand index  								 							 						 |  							 								 									mutual info  								 							 						 |
|  							 								 									K-means  								 							 						 |  							 								 									orig  								 							 						 |  							 								 									0.783  								 							 						 |  							 								 									0.770  								 							 						 |  							 								 									0.776  								 							 						 |  							 								 									0.682  								 							 						 |  							 								 									0.760  								 							 						 |
|  							 								 									K-means  								 							 						 |  							 								 									PCA  								 							 						 |  							 								 									0.756  								 							 						 |  							 								 									0.750  								 							 						 |  							 								 									0.753  								 							 						 |  							 								 									0.691  								 							 						 |  							 								 									0.739  								 							 						 |
|  							 								 									K-means  								 							 						 |  							 								 									ICA  								 							 						 |  							 								 									0.756  								 							 						 |  							 								 									0.750  								 							 						 |  							 								 									0.753  								 							 						 |  							 								 									0.691  								 							 						 |  							 								 									0.739  								 							 						 |
|  							 								 									K-means  								 							 						 |  							 								 									RP  								 							 						 |  							 								 									0.508  								 							 						 |  							 								 									0.507  								 							 						 |  							 								 									0.507  								 							 						 |  							 								 									0.368  								 							 						 |  							 								 									0.485  								 							 						 |
|  							 								 									K-means  								 							 						 |  							 								 									LDA  								 							 						 |  							 								 									0.925  								 							 						 |  							 								 									0.925  								 							 						 |  							 								 									0.925  								 							 						 |  							 								 									0.917  								 							 						 |  							 								 									0.922  								 							 						 |
|  							 								 									EM  								 							 						 |  							 								 									orig  								 							 						 |  							 								 									0.806  								 							 						 |  							 								 									0.791  								 							 						 |  							 								 									0.798  								 							 						 |  							 								 									0.720  								 							 						 |  							 								 									0.785  								 							 						 |
|  							 								 									EM  								 							 						 |  							 								 									PCA  								 							 						 |  							 								 									0.819  								 							 						 |  							 								 									0.818  								 							 						 |  							 								 									0.818  								 							 						 |  							 								 									0.768  								 							 						 |  							 								 									0.810  								 							 						 |
|  							 								 									EM  								 							 						 |  							 								 									ICA  								 							 						 |  							 								 									0.489  								 							 						 |  							 								 									0.128  								 							 						 |  							 								 									0.203  								 							 						 |  							 								 									0.065  								 							 						 |  							 								 									0.125  								 							 						 |
|  							 								 									EM  								 							 						 |  							 								 									RP  								 							 						 |  							 								 									0.536  								 							 						 |  							 								 									0.505  								 							 						 |  							 								 									0.520  								 							 						 |  							 								 									0.365  								 							 						 |  							 								 									0.482  								 							 						 |
|  							 								 									EM  								 							 						 |  							 								 									LDA  								 							 						 |  							 								 									0.950  								 							 						 |  							 								 									0.949  								 							 						 |  							 								 									0.949  								 							 						 |  							 								 									0.949  								 							 						 |  							 								 									0.947  								 							 						 |

In the experiments Random Projection resulted in a projection which doesn’t correlate with the real world classification of data resulting in a low values for both EM as well as K-means. 

LDA tries to identify attributes that account for the most variance between classes. In particular, LDA, in contrast to PCA, is a supervised method, using known class labels. In this case since we have the class labels LDA is able to identify the attributes (pixels in this case) which really differentiate a digit from another one. Which results in it’s exceptional performance. as compared to other methods. 