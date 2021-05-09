# Basic-CNN-Model-on-Malaria-Dataset-96% accuracy

Link of Dataset : https://www.kaggle.com/iarunava/cell-images-for-detecting-malaria
imported necessary libraries at first like pandas , numpy , os  , glob , matplotlib and many others

Store directry path in variables so that we can extract the file names of the images. Then we extract the file names by using glob library

Split the data into test and train data and then splited the train data into train and validation data.

For Parallely Accessing we use threading library

Now we access the data using imread() 
then resize and interpolate it using cv2.INTER_CUBIC
then make an array using np.array() to make it like an image

then we change the image to (id , img , len(train_data) ) format
so that we can feed in treading library function like futures.ThreadPoolExecutor(max_workers=None) to access the data parallely

we display some random images using random.randint( 0 , train_data.shape[0] , 1) 
we use for loop to extract these random images number 16 times so we get 16 images
plt.subplot(4,4,n) we use to give a number to each subplot

We set hyperparameter values as 
BATCH_SIZE = 64
NUM_CLASSES = 2
EPOCHS = 25
INPUT_SHAPE = (100, 100, 3)
optimizer = Adam 
loss = binary_crossentropy
metrics = [accuracy]

we use decay in learning rate by factor of 0.5 .So, it became half each time VALIDATION Loss doesn't reduce two times conscutively and lr min range was set as 0.000001
and use it in checkpoint

We normalize the data
train_imgs_scaled = train_data / 255.
val_imgs_scaled = val_data / 255.

We encode the labels using 
le = LabelEncoder()
le.fit(train_labels)
train_labels_enc = le.transform(train_labels)

Load Tensorboard to access visuallzation 

MODEL ARCHITECTURE :
We use 3 CNN Layers
each of which are followed by MaxPool layer and Drop out layer which are used for regularization purposes
then we use flatten layer to flatten the data from 3d to 1d
then we use 2 dense layers and each of them is followed by dropout layer
finally we use dense layer which gives prediction results

then we start training 
and then we save the model
