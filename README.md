# Sliced Wasserstein Generative Models<br><i>-- and the application on unsupervised video generation</i>

           
### Papers
* [Sliced Wasserstein Generative Models (CVPR2019)](https://arxiv.org/pdf/1706.02631.pdf)
* [Towards High Resolution Video Generation with Progressive Growing of Sliced Wasserstein GANs (Arxiv)](https://arxiv.org/pdf/1810.02419.pdf) 


## Prerequisites
This repo has been successfully tested on **tensorflow 1.10, cuda 9.0**. 

* Please check the [requirements.txt](https://github.com/musikisomorphie/swd/blob/master/requirements.txt) for more details.

* For the training data such as Cifar10, CelebA, CelebA-HQ, LSUN etc download them on the official website accordingly.

* [TrailerFaces](https://data.vision.ee.ethz.ch/zzhiwu/trailerFaces-tfrecords.zip) (**Note that we tentatively release the tfrecord data to avoid the copyright issue.**)
  * The dataset contains approximately 200,000 individual clips of various facial expressions, where the faces are cropped with 256x256 resolution from about 6,000 high resolution movie trailers on YouTube. We convert them to tfrecord with resolutions range from 4x4 to 256x256. More about the data processing please see [Towards high resolution video generation (Arxiv)](https://arxiv.org/pdf/1810.02419.pdf). 
  

TrailerFaces sample:
![Trailerfaces sample](https://github.com/musikisomorphie/swd/blob/master/progressive_training/trailer_faces_samples.png)

## Standardard Training

### SWAE: it requires some custom ops, which are stored under the [cuda](https://github.com/musikisomorphie/swd/tree/master/standard_training/cuda) folder.
  * Following the instructions in [install](https://github.com/musikisomorphie/swd/blob/master/standard_training/cuda/install), you could compile them by yourself. If you install tensorflow by pip, one potential error can be some source files of tensorflow set the wrong relative path of cuda.h, you just need to manually change them according to your cuda path.
  * Alternatively, you could also use the binary files directly, which is compiled with cuda8.0.
  * Specify DATA_DIR, LOG_DIR and DIR in standard_training/swae_64x64.py, then run
    * cd standard_training/
    * python swae_64x64.py
  
### SWGAN: 
   * Specify DATA_DIR, LOG_DIR and DIR in standard_training/swgan_64x64.py, then run
     * cd standard_training/
     * python swgan_64x64.py   

## Progressive Training

### PG-SWGAN-3D: 
* Specify data_dir, result_dir in progressive_training/config.py, then run
     * cd progressive_training/
     * python train.py   
* We trained our model with 1 TitanXp GPU for roughly 7 days, since our code is built upon progressive growing GAN (https://arxiv.org/pdf/1710.10196.pdf),
the code can be easily adapted to multigpu training on better GPU (See progressive_training/config.py). It is expected that the training speed can be significantly improved.
Here are some sample frames generated by PG-SWGAN-3D:
![PG-SWGAN-3D](https://github.com/musikisomorphie/swd/blob/master/progressive_training/pgswgan_3d.jpg)

* More video comparison, see the following youtube links:
  * PG-SWGAN-3D VS PG-WGAN-3D: See [video1](https://www.youtube.com/watch?v=BvIJk01r9tw)
  * VGAN VS MoCoGAN: See [video2](https://www.youtube.com/watch?v=Q7kUrPTcmdE)
  
### Citation
* If you use this code for your research, please cite our papers.
```
@inproceedings{jqwu&zwhuang2019swgm,
  title={Sliced Wasserstein Generative Models},  
  author={Jiqing Wu, Zhiwu Huang, Dinesh Acharya, Wen Li, Janine Thoma, Danda Pani Paudel, Luc Van Gool},
  booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},
  year={2019}  
}
```

## Acknowledgments
This code borrows from WGAN-GP (https://github.com/igul222/improved_wgan_training) and PGGAN (https://github.com/tkarras/progressive_growing_of_gans). We would like to thank them for the contribution.


