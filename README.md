```
docker run --privileged -it -p 5000:22 --name cyy_ssh nvcr.io/nvidia/pytorch:23.06-py3 
//apt update
//apt install openssh-server
/etc/init.d/ssh start
//vim /etc/ssh/sshd_config
//PermitRootLogin yes
systemctl enable ssh(忘了)
systemctl start ssh
passwd
ctrl+p+q
docker exec --privileged -it cyy_ssh /bin/bash
ctrl+p+q
docker commit cyy_ssh cyy:v0

docker ps -a
docker stop id
docker rm id

docker run --privileged -it -p 5000:22 --name cyy_to --gpus '"device=1,2"'  -v /data/cyy/tensor_to:/root/tensor_to cyy:v0
systemctl start ssh

C:\Users\c\.ssh\known_hosts
root@172.18.218.133 -p 5000

docker run --privileged -it --name cyy_torch --gpus '"device=1,2"' -v /data/cyy/torch_tensor:/torch_tensor ubuntu:22.04 
docker exec --privileged -it cyy_torch /bin/bash 
apt update
apt install wget
apt install gcc-12
ln -s gcc-12 gcc
apt install g++-12
ln -s g++-12 g++
apt install gdb
wget https://repo.anaconda.com/archive/Anaconda3-2023.07-1-Linux-x86_64.sh
apt install vim
conda create -n torch0 python=3.8(3.10)

https://developer.nvidia.com/cuda-downloads
sh: 1: lsmod: not found:apt install kmod
sh: 1: dkms: not found:apt install dkms
libxml2.so.2: cannot open shared object file: No such file or directory:install libxml2
PATH includes /usr/local/cuda-12.2/bin                   LD_LIBRARY_PATH includes /usr/local/cuda-12.2/lib64     https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html   

conda install cmake ninja
conda install mkl mkl-include
conda install -c pytorch magma-cuda121
git clone --recursive https://github.com/pytorch/pytorch
cd pytorch
git submodule sync
git submodule update --init --recursive
git config --global --add safe.directory /torch_tensor/pytorch
pip install -r requirements.txt
make triton
export USE_ROCM=0
export _GLIBCXX_USE_CXX11_ABI=1
export CMAKE_PREFIX_PATH=${CONDA_PREFIX:-"$(dirname $(which conda))/../"}
export DEBUG=1
export USE_CUDA=1
python setup.py develop

collect2:fatal error: ld terminated with signal 9[Killed]
swapon -s
mkdir -p /torch_tensor/swap
cd /torch_tensor/swap
dd if=/dev/zero of=swapfile bs=1024 count=3145728
sync
mkswap swapfile
swapon swapfile
chmod 600 swapfile
swapon failed:Device or resource busy
swapoff swapfile
swapon swapfile
swapon -s

mkdir tttt
docker run --privileged -it --name tttt -v /data/cyy/tttt:/tttt ubuntu:22.04 
docker exec --privileged -it tttt /bin/bash 

ImportError: /torch_tensor/anaconda3/envs/torch0/bin/../lib/libstdc++.so.6: version `GLIBCXX_3.4.30' not found (required by /torch_tensor/pytorch/torch/lib/libtorch_python.so)
strings /usr/local/cuda-12.2/nsight-systems-2023.2.3/host-linux-x64/libstdc++.so.6 | grep GLIBCXX_3.4.30 
cp /usr/local/cuda-12.2/nsight-systems-2023.2.3/host-linux-x64/libstdc++.so.6 /torch_tensor/anaconda3/envs/torch0/bin/../lib

apt install python3-dbg(3.10，python也要3.10?)
source /usr/share/gdb/auto-load/usr/bin/python3.10-gdb.py 
```

