# docker安装

1. 安装gnome终端

   ```shell
   sudo apt install gnome-terminal
   ```

2. 卸载适用于 Linux 的 Docker Desktop 的技术预览版或测试版

   ```shell
   sudo apt remove docker-desktop
   ##彻底删除
   rm -r $HOME/.docker/desktop
   sudo rm /usr/local/bin/com.docker.cli
   sudo apt purge docker-desktop
   ```

3. 安装依赖环境

   ```shell
   #官方的方法
   ##添加docker的GPG密钥，成功后会在相应的路径里面生成密钥
   sudo apt-get update
   sudo apt-get install ca-certificates curl gnupg
   sudo install -m 0755 -d /etc/apt/keyrings
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   sudo chmod a+r /etc/apt/keyrings/docker.gpg
   
   ##添加源
   echo \
     "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
     "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
     sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   sudo apt-get update
   ##如果更新源出现错误，将/etc/apt/sources.list.d/docker.list删除掉
   
   #另外一种方法
   ##添加依赖
   sudo apt-get update
   sudo apt-get install apt-transport-https
   sudo apt-get install ca-certificates
   sudo apt-get install curl
   sudo apt-get install gnupg-agent
   
   ##添加密钥
   ###官方源
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ###中科大源
   curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
   ###清华源
   curl -fsSL https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
   ###检查秘钥是否安装成功
   sudo apt-key fingerprint 0EBFCD88
   
   ##添加软件源 推荐使用密钥和软件源一致
   ###中科大源
   sudo add-apt-repository \   
   "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu \   
   $(lsb_release -cs) \   stable"     
   ###清华源
   sudo add-apt-repository \  
   "deb [arch=amd64] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu \  
   $(lsb_release -cs) \  stable"
   ```

4. 下载docker

   ```shell
   wget -c https://desktop.docker.com/linux/main/amd64/docker-desktop-4.16.1-amd64.deb
   ```

5. 安装docker

   ```shell
   sudo apt-get install ./docker-desktop-<version>-<arch>.deb
   ###如果遇到如下报错，使用如下指令
   '''
   Some packages could not be installed. This may mean that you have
   requested an impossible situation or if you are using the unstable
   distribution that some required packages have not yet been created
   or been moved out of Incoming.
   The following information may help to resolve the situation:
   
   The following packages have unmet dependencies:
    docker-desktop : PreDepends: init-system-helpers (>= 1.54~) but 1.51 is to be installed
   E: Unable to correct problems, you have held broken packages.
   '''
   wget http://ftp.kr.debian.org/debian/pool/main/i/init-system-helpers/init-system-helpers_1.60_all.deb
   sudo apt install ./init-system-helpers_1.60_all.deb
   ##然后在安装
   sudo apt-get install ./docker-desktop-<version>-<arch>.deb
   ```

6. 验证

   ```shell
   docker compose version  #Docker Compose 的版本信息
   docker --version #显示安装的版本号
   docker version #输出包括客户端和服务器端的详细版本信息
   ```

   