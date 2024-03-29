ubuntu20安装docker：

参考官网的  https://docs.docker.com/engine/install/ubuntu/

以下apt-get 可以用apt代替

```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

```
sudo apt-get update
```

```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

```
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```
sudo apt-get update
```

```
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

```
sudo docker run hello-world
```

```
#添加docker用户组
sudo groupadd docker  
 #将登陆用户加入到docker用户组中
sudo gpasswd -a $USER docker 
#更新用户组
newgrp docker
 #测试docker命令是否可以使用sudo正常使用
docker ps 
```
