
### Facial Keypoint Detection

    This is the general pipeline for the problem.

    1. Load Keypoints

        First of all we load the keypoints from csv file. There are 28 keypoints for every single image. 
    
    2. Create Facial Keypoint Dataset Class

        We create the dataset class. We read the image and store in the dictionary with the corresponding
        keypoints.
    
    3. Create Transform Classes

        We define Normalize class which normalizes image by dividing 255. We convert image to gray scale.
        Also we normalize the keypoints by substracting -100 and dividing with the 50.

        We define Rescale class which rescales the image to 250x250. We also scale the keypoints to the
        appropriate range.

        We define RandomCrop class which crops image randomly. In our example it is 224x224.

        We define ToTensor class which converts image(numpy ndarray) to Pytorch tensor. We also convert
        keypoints numpy array to Pytorch tensor as well.

    4. Define DataLoader objects
        
        [Pytorch Data Loader Tutorial](https://pytorch.org/tutorials/beginner/data_loading_tutorial.html)


        We define the data loader objects. We seperate 10% of the data for the validation. We set batch
        size to 64.

    5. Define the Convolutional Neural Network

        We define the regressor CNN model. Model is basically:

        (CONV->BN->ReLU->MaxPool) * 3 -> (Linear->BN->ReLU->Dropout) * 2 -> Linear

        Kernel sizes, linear units and dropout rates can be found in the notebook.

    6. Define the loss function and the optimizer

        We define MSELoss function and the Adam optimizer with the default parameters.

    7. Train model

        We train the model for 50 epochs.

    8. Test Model

        We test our trained model on validation images and visualize the predictions.
