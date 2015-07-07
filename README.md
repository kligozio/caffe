# Modifications made to Visual Studio and a Windows Build
I followed [Neil Shao's Blog](https://initialneil.wordpress.com/2015/01/11/build-caffe-in-windows-with-visual-studio-2013-cuda-6-5-opencv-2-4-9/) to get started 

## Preqequisites
1.  Install Boost 1.0.56.  
2.  Install CUDA 7.0
3.  Install OpenCV (need version)
4.  (Optional) Install Anaconda Python

## Environment
### Build Tools
1.  BOOST_1_56_0=c:\toolkits\boost_1_56_0
2.  OPENCV_X64_VS2013_2_4_11=c:\toolkits\opencv\build
3.  PATH=%PATH%;%OPENCV_HOME%\build\x64\vc12\bin;%BOOST_1_56_0%\lib64-msvc-12.0;%OPENCV_X64_VS2013_2_4_11%\x64\vc12\bin
4.  (Optional) ANACONDA_PATH=c:\Anaconda

### Python
CAFFE_HOME=c:\home\projects\caffe\ 
PATH=%PATH%;%CAFFE_HOME%\bin\py;%CAFFE_HOME%\bin\py\caffe;%CAFFE_HOME%\3rdparty\lib

If you'd like to run python from the command line, add
PYTHONPATH=%ANACONDA_PATH%\Lib;%CAFFE_HOME%\bin\py

In Visual Studio, right-click Search Paths and Add Folder to Search Path.  This needs to match PYTHON_PATH, so find your anaconda lib folder and your bin\py folder.

# Caffe

Caffe is a deep learning framework made with expression, speed, and modularity in mind.
It is developed by the Berkeley Vision and Learning Center ([BVLC](http://bvlc.eecs.berkeley.edu)) and community contributors.

Check out the [project site](http://caffe.berkeleyvision.org) for all the details like

- [DIY Deep Learning for Vision with Caffe](https://docs.google.com/presentation/d/1UeKXVgRvvxg9OUdh_UiC5G71UMscNPlvArsWER41PsU/edit#slide=id.p)
- [Tutorial Documentation](http://caffe.berkeleyvision.org/tutorial/)
- [BVLC reference models](http://caffe.berkeleyvision.org/model_zoo.html) and the [community model zoo](https://github.com/BVLC/caffe/wiki/Model-Zoo)
- [Installation instructions](http://caffe.berkeleyvision.org/installation.html)

and step-by-step examples.

[![Join the chat at https://gitter.im/BVLC/caffe](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/BVLC/caffe?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Please join the [caffe-users group](https://groups.google.com/forum/#!forum/caffe-users) or [gitter chat](https://gitter.im/BVLC/caffe) to ask questions and talk about methods and models.
Framework development discussions and thorough bug reports are collected on [Issues](https://github.com/BVLC/caffe/issues).

Happy brewing!

## License and Citation

Caffe is released under the [BSD 2-Clause license](https://github.com/BVLC/caffe/blob/master/LICENSE).
The BVLC reference models are released for unrestricted use.

Please cite Caffe in your publications if it helps your research:

    @article{jia2014caffe,
      Author = {Jia, Yangqing and Shelhamer, Evan and Donahue, Jeff and Karayev, Sergey and Long, Jonathan and Girshick, Ross and Guadarrama, Sergio and Darrell, Trevor},
      Journal = {arXiv preprint arXiv:1408.5093},
      Title = {Caffe: Convolutional Architecture for Fast Feature Embedding},
      Year = {2014}
    }
