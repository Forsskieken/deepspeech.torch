# Installation

Note: This installation assumes you are willing to install CUDA 7.5 AND [cudnn](https://developer.nvidia.com/cudnn) R5 (for GPU support which is default). How to install these are
described below.

## Torch and CUDA

To install torch7 follow the guide [here](http://torch.ch/docs/getting-started.html).

You must have CUDA 7.5 or above (build supported by warp-ctc). To install CUDA 7.5:

Download the .run file of your platform [here](https://developer.nvidia.com/cuda-downloads).

Example for Ubuntu 14.04:
```
wget http://developer.download.nvidia.com/compute/cuda/7.5/Prod/local_installers/cuda_7.5.18_linux.run
```
Then install using below commands.
```
sudo chmod +x ./cuda_7.5.18_linux.run
sudo ./cuda_7.5.18_linux.run
```
When prompted with this message I suggest pressing no. Highly recommended to install the latest driver from the nvidia website of your GPU,
but the driver is compatible if you select yes.
```
Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 352.xx? ((y)es/(n)o/(q)uit):
```
Finally modify the .bashrc located at ~/.bashrc, including these lines at the end:
```
export PATH=/usr/local/cuda-7.5/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-7.5/lib64:$LD_LIBRARY_PATH
```
Restart the terminal for changes to take effect.

## Luarocks installs

For CUDA implementation (make sure to install these via luarocks first before installing the warp-ctc library):
```
luarocks install cutorch
luarocks install cunn
luarocks install cunnx
```

To install the Baidu warp-ctc library:
```
luarocks install http://raw.githubusercontent.com/baidu-research/warp-ctc/master/torch_binding/rocks/warp-ctc-scm-1.rockspec
```
Other dependencies can be installed via luarocks:

[Audio Library for Torch](https://github.com/soumith/lua---audio): Audio Library for Torch</a>:

Linux (Ubuntu):
```
sudo apt-get install libfftw3-dev
sudo apt-get install sox libsox-dev libsox-fmt-all
```

```
luarocks install https://raw.githubusercontent.com/soumith/lua---audio/master/audio-0.1-0.rockspec
```

[Optim](https://github.com/torch/optim): numeric optimization package for Torch</a>:
```
luarocks install optim
```

[rnn](https://github.com/Element-Research/rnn): Recurrent Neural Network library for Torch7's nn</a>:
```
luarocks install rnn
```

[lua---nx](https://github.com/clementfarabet/lua---nnx): An extension to Torch7's nn package</a>:
```
luarocks install nnx
```

[xlua](https://github.com/torch/xlua): A set of useful extensions to Lua</a>:
```
luarocks install xlua
```

[CTCHelpers](https://github.com/SeanNaren/CTCHelpers): Collection of modules that are used in Torch CTC network implementations</a>:
```
luarocks install https://raw.githubusercontent.com/SeanNaren/CTCHelpers/master/ctchelpers-scm-1.rockspec
```

It is also suggested to update the following libraries:
```
luarocks install torch
luarocks install nn
luarocks install dpnn
```

## cuDNN

For cuDNN V5 you need to create an account, follow install instructions [here](https://developer.nvidia.com/cudnn). Make sure to install V5.

Once you have completed the above installation, Install lua bindings for [cudnn R5](https://github.com/soumith/cudnn.torch/tree/R5):
```
luarocks install https://raw.githubusercontent.com/SeanNaren/CTCSpeechRecognition/master/rocks/cudnn-scm-1.rockspec
```

Finally clone the repository to access the scripts:

```
git clone https://github.com/SeanNaren/CTCSpeechRecognition.git
```

Main method located at AN4CTCTrain.lua.

Training data is currently the [AN4 Audio database](http://www.speech.cs.cmu.edu/databases/an4/).

The dataset can be downloaded and extracted using the below commands on Linux:

```
wget http://www.speech.cs.cmu.edu/databases/an4/an4_raw.bigendian.tar.gz
tar -xzvf an4_raw.bigendian.tar.gz
```

Within the AN4CTCTrain we specify the file path to the an4 dataset which can be downloaded [here](http://www.speech.cs.cmu.edu/databases/an4/an4_raw.bigendian.tar.gz).

Extract the folder and give the filepath in the AN4CTCTrain.lua script.

**Note that the data has to be converted into wav format, a bash script ConvertAN4ToWav.sh has been included to help with this (place this into the an4 directory then run).**
