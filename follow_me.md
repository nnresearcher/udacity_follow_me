# 1.My network architecture


| layers        | output shape           | depth  |
| ------------- |:-------------:| -----:|
| input layer | 160 * 160 | 3 |
| 4*4 layer | 160 * 160 | 64 |
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


# 3. Convolution\encoder\decoder function

In the begining using 4*4 convolution layer is in order to extract feature from picture,and we can know the classification of each pixel from 1*1 convolution layer . 

Encoder is extracting information usually form a low-rank vector .Decoder is uses the information to extract the low-rank processing information, which can then be mixed with other information

We use encoder to extract something we fouce on in the picture , in this project we fouce on people ,encoder layer would ignore any other function in the picture for example tree.And using decoder layer to recover the infomation ,but now somethig infomation would disappear.

# 4. model function

Because this topic fouce on people,we can see the train data's masks is fouce on people,so this model can use in identify people not any other for example we could not identify tree.

