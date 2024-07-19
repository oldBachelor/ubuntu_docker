### 在 Ubuntu 上安装 Docker 引擎

具体安装步骤请参考 [官方文档](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)。

请注意，脚本中已替换镜像源，因为官方提供的源可能导致链接超时。

#### 安装步骤：

1. 将以下脚本内容保存到一个文件或者直接拉取，比如 `setup_docker.sh`。

```bash
#!/bin/bash

# Remove existing packages
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do
  sudo apt-get remove $pkg
done

# Update package lists
sudo apt-get update

# Install necessary packages
sudo apt-get install ca-certificates curl

# Configure Docker repository
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker packages
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

2.接着在终端中运行以下命令将其设置为可执行文件

chmod +x setup_docker.sh

3.最后，运行脚本来执行安装 Docker 的操作

./setup_docker.sh
