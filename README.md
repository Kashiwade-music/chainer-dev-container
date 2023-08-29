# chainer-mnist-fpga

## Environment of this container
- Ubuntu: 16.04 LTS (64-bit)
- CUDA: 11.0.3
  - with [CUDA math libraries](https://developer.nvidia.com/gpu-accelerated-libraries), [NCCL](https://developer.nvidia.com/nccl), [cuDNN](https://developer.nvidia.com/cudnn), headers, and development tools for building CUDA images
- Anaconda3: 2023.07-2
- Python: 3.8.17 (Environment setup with Anaconda from `env.yaml`)
  - Chainer: 7.8.1
  - ChainerCV: 0.13.1
  - CuPy (CUDA11.0): 7.8.0
  - Numpy: 1.21.6
  - OpenCV Python: 4.8.0.76
  - Pillow: 10.0.0
  - Matplotlib: 3.2.2
  - SciPy: 1.7.3
- git, zsh, wget

## How to setup environment
- Install Nvidia driver
- Install Docker and [nvidia-container-toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#install-guide)
- Open in container with VSCode (Use Dev Container)
- Set up zsh powerlevel10k (optional)
- Execute command `conda init zsh`
- Execute command `conda env create -f=env.yaml`
- Activate conda environment `conda activate chainer`

## Test if the environment was built correctly
- Execute below command
  ```sh
  wget https://github.com/chainer/chainer/archive/v7.8.1.tar.gz
  tar xzf v7.8.1.tar.gz
  python chainer-7.8.1/examples/mnist/train_mnist.py -g 0
  ```

- Check to see if Chainer is using CuPy. (below is example output)
  ```sh
  Device: @cupy:0
  # unit: 1000
  # Minibatch-size: 100
  # epoch: 20
  
  Downloading from http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz...
  Downloading from http://yann.lecun.com/exdb/mnist/train-labels-idx1-ubyte.gz...
  Downloading from http://yann.lecun.com/exdb/mnist/t10k-images-idx3-ubyte.gz...
  Downloading from http://yann.lecun.com/exdb/mnist/t10k-labels-idx1-ubyte.gz...
  epoch       main/loss   validation/main/loss  main/accuracy  validation/main/accuracy  elapsed_time
  0                       2.29594                              0.1338                    2.4168        
  1           0.189312    0.119008              0.942566       0.9646                    4.01696       
  2           0.0756096   0.100343              0.976183       0.969                     5.2076        
  3           0.0511657   0.0675998             0.983399       0.9796                    6.40066       
  4           0.0345011   0.0628942             0.988415       0.9822                    7.59733       
  5           0.0267106   0.0736203             0.991115       0.9794                    8.82018       
  6           0.023358    0.0722077             0.991982       0.9808                    10.0149       
  7           0.02297     0.0713134             0.992615       0.9831                    11.2177       
  8           0.0189034   0.0774308             0.993932       0.9811                    12.4066       
  9           0.0140125   0.0795618             0.995465       0.9818                    13.6107       
  10          0.0160751   0.0834037             0.994848       0.9815                    14.8193       
  11          0.00969862  0.0923871             0.996749       0.9806                    16.0138       
  12          0.0150301   0.109208              0.995465       0.9805                    17.2148       
  13          0.0104927   0.0887402             0.996915       0.9827                    18.4342       
  14          0.0131343   0.0993166             0.995665       0.9802                    19.6602       
  15          0.0146997   0.0804493             0.995716       0.9825                    20.8654       
  16          0.00734491  0.0857848             0.997766       0.9852                    22.0978       
  17          0.00786814  0.121481              0.997449       0.9778                    23.3313       
  18          0.0100734   0.132682              0.997266       0.9815                    24.5442       
  19          0.00892782  0.106411              0.997266       0.9833                    25.7678       
  20          0.00860138  0.117193              0.997383       0.9827                    27.0023       
  
  ```