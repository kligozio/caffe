# Modifications made to Visual Studio and a Windows Build
This uses the *Ceemple OpenCV distribution for Visual Studio* to build Caffe's python bindings.

## Preqequisites

1.  Install the free [Ceemple OpenCV distribution for Visual Studio](https://www.ceemple.com/ceemple-opencv-visual-studio/)
1.  Install [Anaconda Python](https://store.continuum.io/cshop/anaconda/)
1.  Install [CUDA toolkit](https://developer.nvidia.com/cuda-downloads). You need this even if you don't plan to compile for a GPU because the project files reference the CUDA targets even when they don't actually get compiled (of course, you could also edit the project files to removed the references to CUDA targets).

## Environment
### Build Tools

1.  `ANACONDA_HOME=C:\Anaconda` (or where you installed it)
1.  `CAFFE_HOME=c:\my\caffe\project\directory` (where you cloned this project to)

## Overcoming build issues

### glog NuGet package error

The glog NuGet package has an overlay that applies in the wrong location. You 
get a missing library error because of this. Just copy the misplaced *contents*
of the `$(ProjectDir)glog.overlay.../` directory to the
`$(SolutionDir)packages/glog.../` directory and recompile.

### Python python27_d.lib link failure

If you build for debugging, for some reason, the python include files expect
you to want to debug the python executable itself. But, Anaconda doesn't come
with debug libraries. To keep from expecting python debugging when building your
own debugging setup, edit the `C:\Anaconda\include\pyconfig.h` file and comment
out all the code that runs when `_DEBUG` is defined. One place sets up the 
*python27_d.lib* link request and another sets the `#define Py_DEBUG`. Making
this change will keep any code on your development machine from being able to
debug the python executable.

If you actually want to debug python along with your code, the web seems to
think you must build your own *python27_d.lib* from source. If you do this,
don't change the `pyconfig.h` file.

## Using

Currently, only the Python project is operational.

### Python
You must build the pycaffe project.

`PATH=%PATH%;%CAFFE_HOME%\bin\py;%CAFFE_HOME%\bin\py\caffe`

Install the required python libraries.  conda can't find all of these, so there's a combination of conda and easy_install
```
cd %CAFFE_HOME%\python
conda install --file requirements_windows_conda.txt
for /f %i in (requirements_windows_easyinstall.txt) do easy_install %i
```

If you'd like to run python from the command line, add
```
PYTHONPATH=%ANACONDA_HOME%\Lib;%CAFFE_HOME%\bin\py
```

#### For Visual Studio python projects that use pycaffe

In Visual Studio, right-click Search Paths and Add Folder to Search Path.  This needs to match PYTHON_PATH, so find your anaconda lib folder and your bin\py folder.

#### Troubleshooting
I find the easiest way to troubleshoot the python environment is to increase verbosity and try to import caffe.  I.e.,
```
python -vvv
>>> import caffe
```

If the DLL is found but won't load, check (double-check, then triple-check) your path.  You need to verify the initial setup (e.g., OPENCV) paths are correct, along with the Python specific ones.

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
