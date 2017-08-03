---

title: TensorFlow环境搭建
date: 2017-08-03

---


# Virtualenv
Take following steps to install TensorFlow:
1. Install pip and virtualenv and python3.
2. Create virtual environment.
3. Activate the virtual environment.

```
sudo easy_install pip
sudo pip install --upgrade virtualenv
brew install python3
virtualenv -p python3 tensorflow
```

# TensorFlow
1. Install tensorflow.
```
pip3 install --upgrade tensorflow
```

# Validate Install
```
(tensorflow) ➜  learn_TensorFlow python
Python 3.6.2 (default, Jul 17 2017, 16:44:45)
[GCC 4.2.1 Compatible Apple LLVM 8.1.0 (clang-802.0.42)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
```
