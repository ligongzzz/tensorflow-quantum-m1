# Tensorflow Quantum for M1 Mac
This tutorial will teach you how to build and install [tensorflow quantum](https://github.com/tensorflow/quantum) on M1 Mac.

----
# Install

## Install Tensorflow for ARM Mac OS
### Install Conda
Firstly, you should install a virtual environment on your mac. You can use [miniforge](https://github.com/conda-forge/miniforge) to create a virtual environment with arm version of Python 3.8.

### Install Tensorflow for Mac OS
[Click here](https://github.com/apple/tensorflow_macos/releases/download/v0.1alpha2/tensorflow_macos-0.1alpha2.tar.gz) to download the latest version of tensorflow_macos. Unzip it and cd into the `arm64` folder.

Activate the python environment you have just created. Use `pip install --no-dependencies xxx` to install all of the wheels, where `xxx` denotes the name of the packages in the folder.

## Build
You can choose to build or download the built version of tensorflow-quantum.
### Install Bazel for ARM Mac OS
[Click here](https://github.com/erwincoumans/bazel/releases/download/bazel-3.7.1-mac-arm64/bazel-3.7.1-mac_arm64.zip) to download the built version of Bazel-3.7.1. __DO NOT__ install bazel directly through Homebrew. After downloading, move the unzipped file to `/usr/local/bin/`.

### Clone this Repo
You can choose to clone this repo or clone the official repo of tensorflow quantum. There are something you need to change in the official version.

- Change `3.1.0` to `3.7.1` in `.bazelversion`.
- Remove `tensorflow==2.4.1` in `requirements.txt`.
- Change `pip show tensorflow` to `pip show tensorflow-macos` in `configure.sh` (line 76).

(If you use the code in this repo, you do not need to modify the above parts.)

### Build
Open Terminal and cd into the folder of this repo.
```
python3 -m pip install -r requirements.txt
./configure.sh

bazel build -c opt --cxxopt="-O3" --cxxopt="-march=native" --cxxopt="-D_GLIBCXX_USE_CXX11_ABI=0" release:build_pip_package

bazel-bin/release/build_pip_package /tmp/tfquantum/
```

## Install
If you don't want to build tensorflow quantum by yourself, you can simply download the built wheel from "Release" in this repo.

If you have built it, cd into `/tmp/tfquantum/`.

Then use `pip3 install tensorflow_quantum-0.5.0-cp38-cp38-macosx_11_0_arm64.whl` to install it.

Now you can test it with the [tutorial](https://tensorflow.google.cn/quantum/overview) of tensorflow quantum.