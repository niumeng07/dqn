# 学习备忘
## 1. deep_rl: Google Paper [human level contron through deep reinforcement learning]
## 2. dqn_cartpole: [cartpole experiment]
## 3. Gomoku
## 4. berkeley-pacman: berkeley吃豆人RL入门作业
## 5. stanford-autodriver: stanford自动驾驶RL入门作业
## 6. berkeley-cs294
## 7. rl-tensorflow: github.com/MorvanZhou/Reinforcement-learning-with-tensorflow.git

### 1. deep_rl

----- DQN 3.0 -----

This project contains the source code of DQN 3.0, a Lua-based deep reinforcement
learning architecture, necessary to reproduce the experiments
described in the paper "Human-level control through deep reinforcement
learning", Nature 518, 529–533 (26 February 2015) doi:10.1038/nature14236.

To replicate the experiment results, a number of dependencies need to be
installed, namely:
    * LuaJIT and Torch 7.0
    * nngraph
    * Xitari (fork of the Arcade Learning Environment (Bellemare et al., 2013))
    * AleWrap (a lua interface to Xitari)
An install script for these dependencies is provided.

Two run scripts are provided: run_cpu and run_gpu. As the names imply,
the former trains the DQN network using regular CPUs, while the latter uses
GPUs (CUDA), which typically results in a significant speed-up.



----- Installation instructions -----

The installation requires Linux with apt-get.

Note: In order to run the GPU version of DQN, you should additionally have the
NVIDIA® CUDA® (version 5.5 or later) toolkit installed prior to the Torch
installation below.
This can be downloaded from https://developer.nvidia.com/cuda-toolkit
and installation instructions can be found in
http://docs.nvidia.com/cuda/cuda-getting-started-guide-for-linux


To train DQN on Atari games, the following components must be installed:
    * LuaJIT and Torch 7.0
    * nngraph
    * Xitari
    * AleWrap

To install all of the above in a subdirectory called 'torch', it should be enough to run

    ./install_dependencies.sh

from the base directory of the package.


Note: The above install script will install the following packages via apt-get:
build-essential, gcc, g++, cmake, curl, libreadline-dev, git-core, libjpeg-dev,
libpng-dev, ncurses-dev, imagemagick, unzip



----- Training DQN on Atari games -----

Prior to running DQN on a game, you should copy its ROM in the 'roms' subdirectory.
It should then be sufficient to run the script

    ./run_cpu <game name>

Or, if GPU support is enabled,

    ./run_gpu <game name>


Note: On a system with more than one GPU, DQN training can be launched on a
specified GPU by setting the environment variable GPU_ID, e.g. by

    GPU_ID=2 ./run_gpu <game name>

If GPU_ID is not specified, the first available GPU (ID 0) will be used by default.



----- Options ------

Options to DQN are set within run_cpu (respectively, run_gpu). You may,
for example, want to change the frequency at which information is output 
to stdout by setting 'prog_freq' to a different value.
### 2.
### 3. AlphaZero-Gomoku
This is an implementation of the AlphaZero algorithm for playing the simple board game Gomoku (also called Gobang or Five in a Row) from pure self-play training. The game Gomoku is much simpler than Go or chess, so that we can focus on the training scheme of AlphaZero and obtain a pretty good AI model on a single PC in a few hours. 

References:  
1. AlphaZero: Mastering Chess and Shogi by Self-Play with a General Reinforcement Learning Algorithm
2. AlphaGo Zero: Mastering the game of Go without human knowledge

#### Update 2018.1.17: now supports training with PyTorch!

#### Example Games Between Trained Models
- Each move  with 400 playouts:  
![playout400](https://raw.githubusercontent.com/junxiaosong/AlphaZero_Gomoku/master/playout400.gif)
- Each move  with 800 playouts:  
![playout800](https://raw.githubusercontent.com/junxiaosong/AlphaZero_Gomoku/master/playout800.gif)

#### Requirements
To play with the trained AI models, only need:
- Python >= 2.7
- Numpy >= 1.11

To train the AI model from scratch, further need, either:
- Theano >= 0.7 and Lasagne >= 0.1      
or
- PyTorch >= 0.2.0

**PS**: if your Theano's version > 0.7, please follow this [issue](https://github.com/aigamedev/scikit-neuralnetwork/issues/235) to install Lasagne,  
otherwise, force pip to downgrade Theano to 0.7 ``pip install --upgrade theano==0.7.0``

If you would like to train the model using other DL frameworks, such as TensorFlow or MXNet, you only need to rewrite policy_value_net.py.

#### Getting Started
To play with provided models, run the following script from the directory:  
```
python human_play.py  
```
You may modify human_play.py to try different provided models or the pure MCTS.

To train the AI model from scratch, with Theano and Lasagne, directly run:   
```
python train.py
```
With PyTorch, first modify the file [train.py](https://github.com/junxiaosong/AlphaZero_Gomoku/blob/master/train.py), i.e., comment the line
```
from policy_value_net import PolicyValueNet  # Theano and Lasagne
```
and uncomment the line 
```
# from policy_value_net_pytorch import PolicyValueNet  # Pytorch
```
and then execute: ``python train.py``  (To use GPU training, set ``use_gpu=True``)

The models (best_policy.model and current_policy.model) will be saved every a few updates (default 50).

**Tips for training:**
1. It is good to start with a 6 * 6 board and 4 in a row. For this case, we may obtain a reasonably good model within 500~1000 self-play games in about 2 hours.
2. For the case of 8 * 8 board and 5 in a row, it may need 2000~3000 self-play games to get a good model, and it may take about 2 days on a single PC.

#### Further reading
My article describing some details about the implementation in Chinese: [https://zhuanlan.zhihu.com/p/32089487](https://zhuanlan.zhihu.com/p/32089487) 
