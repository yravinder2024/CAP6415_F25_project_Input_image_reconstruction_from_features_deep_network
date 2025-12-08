ABSTRACT

Image reconstruction has been a challange in the field of computer vision where models which were first 
introduced used take a long time to run and do not recreate the image as high quality as possible. 
As new models were being introduced, different scenario used to take place such as fast run time 
but a blurry image was recreated, long run time but recreated image was better. So, the project uses 
two architectures namely Genertive Adversarial Network (GAN) and Diffusion Model to recreate Images from 
features and compare them to find out which architecture can be used for future work in the line of computer vision.

The Dataset used was ImageNette which contains 10 classes
(tench, English springer, cassette player, chain saw, church, French horn, garbage truck, gas pump, golf ball, parachute).
First we resize it to 256px and then turn it to 224 X 224 resolution. Input is then normalized using ImageNet mean and standard deviation. 
ResNet - 101 is used on the preprocessed data and we use layer3 features to pass it through GAN and diffusion model architectures.


First we created a GAN architecture which contain Genrator which reconstruct the image, Discriminator which checks if the image is real or fake.
Training loop was done for 50 Epochs where we calculate g_loss which find the difference in pixel value of original image and reconstructed image,
d_loss which find the difference between real or fake reconstructed image. Using these two loss we find the accuracy of how accurate GAN has recreated 
the image comared to original image.

Diffusion Model

The GAN architecture run fast but does not give a good accuracy and the reconstructed image is very blurry. But the Diffusion model runs slow but give a 
good accuracy and a better reconstructed image but its computationally expensive.
