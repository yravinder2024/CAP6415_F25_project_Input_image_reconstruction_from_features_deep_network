INPUT IMAGE RECONSTRUCTION FROM FEATURES (DEEP NETWORK)

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

GAN Architecture

Code Link : https://colab.research.google.com/drive/1ID1e71JfYLPWVuf8bHbUh4PImv-ihHH9?usp=sharing

GAN architecture is created which contain two neural network named generator and discriminator. Training begins with generator taking random noise and produce fake sample. Discriminator recieves both real data and generators fake sample and learn to differentiate them as real or fake by minimizing a binary classification loss. then generator is updated to fool the discriminator by vreating fake samples that it can be classified as real which it learns by maximizing the discriminators error. this loop runs for every epoch. both neural network learns and become better every iteration.


Coding Language = python in google colab

pytorch framework

Dataset = Imagenette (Imagenette subset)

Samples = 5000

EPOCH = 30

batch_size = 32

lr = 2e-4

beta1, beta2 = 0.5, 0.999

img_size = 224

img_channels = 3

noise_dim = 100

Model runtime = 35 minutes

avg generator loss = 0.97

avg discriminator loss = 1.25

<img width="1013" height="413" alt="image" src="https://github.com/user-attachments/assets/d26d02cd-6255-4571-9ef8-7f872ed7310e" />

<img width="960" height="682" alt="image" src="https://github.com/user-attachments/assets/b88a4273-d272-4bbd-aaa8-9ef3c18f4cce" />


Diffusion Architecture

Code Link : https://colab.research.google.com/drive/1z2zOHQZPFsUEeFoWqjRHGFvROUaP_wjV?usp=sharing

Diffusion architecture is then created which defines a forward process which add gaussian moise to real data in every timestep until the data becomes nearly pure noise. the model then learns reverse process which predicts how to remove the noise step by step. Each step is denoising until we obtain a realistic image which produce output which is used to compare with the original image.
Training loop was done for 50 Epochs where we calculate loss for training and validation and PSNR and SSIM for every image.

Coding Language = python in google colab

pytorch framework

Dataset = Imagenette (Imagenette subset)

Weights = pretrained stable diffusion components (runwaynl/stable_diffusion_v1.5)

Samples = 5000

EPOCH = 50

batch_size = 32

lr = 1e-4

img_size = 224

img_channels = 3

Model runtime = 2 hours

avg loss = 0.92

![WhatsApp Image 2025-12-08 at 17 41 20_7711b4e6](https://github.com/user-attachments/assets/f515c9f7-41f2-4249-a846-337d806b8b2f)

![WhatsApp Image 2025-12-08 at 17 41 19_d91676cc](https://github.com/user-attachments/assets/9587871c-70cf-4e98-8965-6f2e206178f2)


To evaluate the performance of the GAN and Diffusion architecture, we compare their training time and reconstruction quality using PSNR and SSIM as metrics.The GAN model completed training significantly faster, taking only 35 minutes, whereas Diffusion model took a longer time, taking 2 hours.

Despite its higher computational cost, Diffusion model delivered better output quality. The GAN achieved an average PSNR of 20 dB and SSIM of 0.68, indicating moderate reconstruction. Diffusion model attained a higher PSNR of 27 dB and SSIM of 0.83. When we look at the images we can see Gan produces blurry images and diffusion model give sharp edges almost creating the original image.

GANs are faster and more efficient, while Diffusion models provide higher-quality reconstructions at the cost of longer runtimes.
