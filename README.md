# ResU-Net
U-net with backbone ResNet-50 /101 - binary semantic segmentation - Tensorflow 2.x/ Keras

The notebook runs in a google colab environment. The dataset is read from google drive on the specific path (hyperparameter). The path scheme has train and test subfolders. The validation dataset is set up from the train subfolder split ratio (hyperparameter) after shuffling. 

The architecture has two encoder backbones (ResNet-50/101) with the same decoder. The code uses Bilinear upsampling to reconstruct the final mask. The backbones can be load with ImageNet weights for transfer learning. The fine-tuning process uses the exponential schedule learning (10 epochs) for decoder initialization and compiles the model with an SGD optimizer with a learning rate (hyperparameter).

The input has tiles with 500x500 pixels (width, height), and there is an option for data augmentation (random flip, random crop, random brightness, random contrast, rotation of 90 degrees). The crop hyperparameter can be chosen up to 500x500.

There are two options for optimizers: SGD and ADAM. The user chooses learning rate and callback multiply by 0.2 if the validation loss doesn't change after ten epochs. Another useful hyperparameter is the step, which controls the steps on epochs.

The training process can be monitored by tensorboard (metrics, prediction ten images from validation dataset, histogram, and distribution values of weights). There are four losses: dice, Tversky, focal Tversky, and binary cross-entropy + dice.

The model evaluation uses the central crop of the images from the test dataset. 
