# Linux（ubuntu20.04）下安装python3.7.5环境

## 方案1，编译安装python环境

#### sudo apt install -y gcc make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev



#### sudo apt install -y make build-essential libssl-dev zlib1g-dev libbz2-dev  libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev   xz-utils tk-dev

- #### tar -zxvf Python3.7.5.tgz

- #### cd Python3.7.5

- #### sudo ./configure --enable-optimizations --prefix=/usr/local/python3.7  --with-ssl

- #### make

- #### sudo make install

- #### sudo ln -s -f /usr/local/python3.7/bin/python3.7 /usr/bin/python3.7

- #### sudo ln -s -f /usr/local/python3.7/bin/pip3.7 /usr/bin/pip3.7



## 方案2，安装miniconda3环境

#### 去官网下载镜像 <https://docs.conda.io/en/latest/miniconda.html>

#### 下载完成后输入命令 bash Miniconda3-latest-Linux-x86_64.sh进行安装即可

