# STBA
This is a C++ implementation of our ECCV 2020 paper - ["Stochastic Bundle Adjustment for Efficient and Scalable 3D Reconstruction"](https://arxiv.org/abs/2008.00446) by Lei Zhou, Zixin Luo, Mingmin Zhen, Tianwei Shen, Shiwei Li, Zhuofei Huang, Tian Fang, Long Quan.

## About


### Benchmark on [1DSfM dataset](http://www.cs.cornell.edu/projects/1dsfm/)
![1DSfM](doc/1DSfM.jpg)


### Benchmark on [KITTI dataset](http://www.cvlibs.net/datasets/kitti/eval_odometry.php)
![KITTI](doc/KITTI.jpg)


### Benchmark on Large-Scale dataset
![largs_scale](doc/large_scale.jpg)



## Usage

### Requirements

* Eigen3
* OpenMP 

### Code version

This repository currently comprises two versions of codes ```0.0.0``` and ```1.0.0``` which go into the ```master``` and ```1.0.0``` branches, respectively.
The ```0.0.0``` codes are based on the plain workflow of an Levenberg-Marquardt solver, while the ```1.0.0``` codes are based on the implementation suggested by [[1] Bundle Adjustment Rules](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.222.3253&rep=rep1&type=pdf) and are supposed to be more computation and memory efficient. You can try different implementations by checking out different branches.

### Build
 
 ```
 cd STBA
 mkdir build && cd build
 cmake ..
 make
 ```

### Run

* Download the sparse reconstruction results of the [COLMAP dataset](https://colmap.github.io/datasets.html) (e.g., Gerrard Hall).
* Unzip the compressed file and three files can be found in the `sparse` folder: `cameras.txt`, `images.txt` and `points3D.txt`.
* ``` cd STBA/build ```
* ``` ./STBA <path_to_cameras.txt> <path_to_imagess.txt>  <path_to_points3D.txt> <output_folder>```
* Run ```./STBA --help``` to see more options.
	* `--iteration`: Set the maximum number of iterations.
	* `--cluster`: A STBA option which sets the maximum cluster size for stochastic graph clustering.
	* `--inner_step`: A STBA option which sets the number of inner iterative steps.
	* `--thread_num`: Set thread number for OpenMP parallel computing.
	* `--radius`: Set the initial radius of trust region for the trust region solvers.
	* `--loss`: Set the type of robust loss function. Currently, `Huber` and `Cauchy` loss functions are supported.
	* `--noise`: The magnitude/sigma of random Gaussian noise which will be added to track positions and camera centers for testing the bundle adjustment algorithms.
	* `--lm`: Use Levenberg-Marquardt solver.
	* `--dl`: Use DogLeg solver.

### TODO

* Add parallel support to version ```1.0.0```, particularly the function ```StochasticBAProblem::EvaluateCamera()```.



## Credit

This implementation was developed by [Lei Zhou](https://zlthinker.github.io/). Feel free to contact Lei for any enquiry.

## Reference

[1] Engels, Chris, Henrik Stewénius, and David Nistér. "Bundle Adjustment Rules." Photogrammetric computer vision, 2(2006).
