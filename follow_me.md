# 1.The write-up conveys the an understanding of the network architecture.

The architecture of my network is:

| layers        | dimension           | depth  |
| ------------- |:-------------:| -----:|
| input layer | 160 * 160 | 3 |
| encoder 1 | 80 * 80 | 128 |
| encoder 2 | 40 * 40 | 64 |
| encoder 3 | 20 * 20 | 32 |
| 1 x 1 layer | 20 * 20 | 32 |
| decoder 1 | 40 * 40 | 32 |
| decoder 2 | 80 * 80 | 64 |
| decoder 3 | 160 * 160 | 128 |

Filter sizes are selected by popular numbers. Three encoder layers are having smaller and smaller dimensions since we have stride equals to 2 which always reduce to half of the size. Opposite operations are taken on the three decoder layers.



# 2. The write-up conveys the student's understanding of the parameters chosen for the the neural network.

The Epoch number is selected to be 10 which can be ran within acceptable time and give reasonable result. Batch size was 16 but the result was too bad, so I changed to 32 obtained final score over 0.4. Learning rate is a typical starting value 0.01 which worked well. Others were kept the default values.


# 3. The student has a clear understanding and is able to identify the use of various techniques and concepts in network layers indicated by the write-up.

The 1 by 1 convolution layer should be used as the last layer after normal convolution operations, it also keeps the spatial information compared with Dense layer. 1 by 1 convolution layer is useful when want to know the classification of each pixel instead of the whole image.

A fully connected layer can be used when we want to classify an input in which the spatial information is not important.


# 4. The student has a clear understanding of image manipulation in the context of the project indicated by the write-up.

Details of the image is removed while encoding, and when decoding, the system is trying to recover the information of the original image at its best.


# 5. The student displays a solid understanding of the limitations to the neural network with the given data chosen for various follow-me scenarios which are conveyed in the write-up.

Given the current data, the model would not work for a different object like car or animal. The system needs this kind of data to be trained and tested to follow. The neural network is highly dependent on the data it is being trained on.





## some useful command for this project
Connect to the AWS instance 
>ssh -i "robond.pem" ubuntu@ec2-54-212-223-139.us-west-2.compute.amazonaws.com

Command to upload files to the AWS instance
>scp -i "robond.pem" your_file ubuntu@ec2-54-212-223-139.us-west-2.compute.amazonaws.com:~/.

Command to unzip files to a specific folders
>unzip file.zip -d your_target_folder
