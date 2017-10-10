# 1.My network architecture


| layers        | output shape           | depth  |
| ------------- |:-------------:| -----:|
| input layer | 160 * 160 | 3 |
| 4 x 4 layer | 160 * 160 | 64 |
| encoder 1 | 80 * 80 | 64 |
| encoder 2 | 40 * 40 | 64 |
| encoder 3 | 20 * 20 | 128 |
| 1 x 1 layer | 20 * 20 | 256 |
| decoder 1 | 40 * 40 | 128 |
| decoder 2 | 80 * 80 | 64 |
| decoder 3 | 160 * 160 | 32 |


Using 4*4 convolution layer to extract feature from picture in the begin. Filter sizes are selected 64 or 32. In three encoder layers, using stride equal to 2 reduce dimensions. In three decoder layer, I set filters from 128 to 32, from experiment I found if filters set too high all the time it would reduce score of the model,and the dimensions larger and larger opposite to encoder layer.


# 2. Parameters

Appropriate patameter is important , learning_rate could not too big or too small . Batch_size must set to big , and I think epochs should set big than 10. So my parameter is that:
learning_rate = 0.015   
batch_size = 20  
num_epochs = 20

If we increase learning rate we may learn too "fast",it may not help to our model, we hope our error can slide to the bottom of the error. Too larger learning_rate would stride to larger error.

If we reduce bath_size error would instability,suiable batch_size could lead error steady decline or don't rise.

If we reduce epochs ,model may not get enough training chance,model's error would not small enough.

# 3. Convolution\encoder\decoder function

In the begining using 4 x 4 convolution layer is in order to extract feature from picture,and we can know the classification of each pixel from 1 x 1 convolution layer . Using 4 x 4 convolution layer we can  flatten input data into a 2D tensor. This results in the loss of spatial information, because no information about the location of the pixels is preserved.That can help the decoder layer to save the infamation that where the people is.

CNN could identification simple shapes and complex objects reduce noice infomation and save useful infomation.CNN generally classifies small parts of the image into simple shapes like horizontal and vertical lines and simple blobs of colors. The subsequent layers tend to be higher levels in the hierarchy and generally classify more complex ideas like shapes (combinations of lines), and eventually full objects like dogs.

Encoder is extracting information usually form a low-rank vector .Separable Convolutions is a technique that reduces the number of parameters needed, thus increasing efficiency for the encoder network. In this project we use it to reduce our training time,and enhance our model performance.The human body contour and location information would saved and others would be removed.

Decoder is uses bilinear upsampling. Bilinear upsampling is a resampling technique that utilizes the weighted average of four nearest known pixels, located diagonally to a given pixel, to estimate a new pixel intensity value. The weighted average is usually distance dependentThe bilinear upsampling method does not contribute as a learnable layer like the transposed convolutions in the architecture and is prone to lose some finer details, but it helps speed up performance.


We use encoder to extract something we fouce on in the picture , in this project we fouce on people ,encoder layer would ignore any other function in the picture for example tree.And using decoder layer to recover the infomation ,but now somethig infomation would disappear.

# 4. Model function

Because this topic fouce on people,we can see the train data's masks is fouce on people,so this model can use in identify people not any other for example we could not identify tree.

# 5. Future enhancement

Add a classifier model to classifier difference things for example people、car or tree.We can use difference color to fill difference objects.

Add PID control for UAV

# 6. Network architecture

![demo-1](https://github.com/nnresearcher/udacity_follow_me/blob/master/name_of_fig_with_shapes.jpgs)
