# CT-RED_CNN_tensorflow
Low-Dose CT with a Residual Encoder-Decoder Convolutional Neural Network (RED-CNN)
* RED_CNN
>	* paper :https://arxiv.org/ftp/arxiv/papers/1702/1702.00288.pdf
## I/O (DICOM file -> .npy)
* Input data Directory  
  * DICOM file extension = [<b>'.IMA'</b>, '.dcm']
> $ os.path.join(dcm_path, patient_no, [LDCT_path|NDCT_path], '*.' + extension)
## Network architecture  
![Network architecture](https://github.com/hyeongyuy/CT-RED_CNN_tensorflow/blob/master/img/architecture.JPG)  
* 10 layers (5 conv  + 5 deconv)
* shortcut
* remove pooling operation
* filter size : 96 * 9 + 1* 1(last layer)
* kernel size : 5 * 5
* stride : 1 (no padding)
## Training detail
* patch size : 55 * 55
* augumentation(patch? whole? // patch...)
>   * rotation(45 degrees)
>   * flipping (vertical & horizontal)
>   * scaling (0.5, 2)
* learning rate : 10e-4  (slowly decreased down(?))
* initializer : random Gaussian distribution (0, 0.01)
* loss function : MSE 
* optimizer : Adam 
## Main file(main.py) Parameters
* Directory
> * dcm_path : dicom file directory
> * LDCT_path : LDCT image folder name
> * NDCT_path : NDCT image folder name
> * test_patient_no : test patient id list(p_id1,p_id2...) (train patient id : (patient id list - test patient id list)
> * checkpoint_dir : save directory - trained model
> * test_npy_save_dir : save directory - test numpy file
> * pretrained_vgg : pretrained vggnet directory
* Image info
> * patch_size : patch size 
> * whole_size : whole size
> * img_channel : image channel
> * img_vmax : max value
> * img_vmin : min value
* Train/Test
> * model : red_cnn, wgan_vgg, cyclegan (for image preprocessing)
> * phase : train | test
* others
> * is_mayo : summary ROI sample1,2
> * save_freq : save a model every save_freq (iterations)
> * print_freq : print_freq (iterations)
> * continue_train : load the latest model: true, false
> * gpu_no : visible devices(gpu no)
* Training detail
> * num_iter : iterations (default = 200000)
> * alpha : learning rate (default=1e-4)
> * batch_size : batch size (default=128)
## Run
* train
> python main.py
* test
> python main.py --phase=test
