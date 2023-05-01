
-->
# WSL2相关
## 安装、配置WSL2
1. 管理员权限运行Powershell

2. Powershell启用WSL2
```
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
3. 重启PC

4. 管理员权限运行Powershell
```
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
5. 重启PC

6. 更改WSL默认版本为WSL2
```
   wsl --set-default-version 2
```
7. 在Windows Store中选择你想要使用的Linux发行版

8. 下载Linux内核更新包，并安装
```
https://learn.microsoft.com/zh-cn/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package
```

## 相关命令

1. 查看所有已安装的Linux发行版的状态
   ```
   wsl -l -v
   ```
2. 更改默认启动的Linux发行版
   ```
   wsl --setdefault <DistributionName>
   wsl -s <DistributionName>
   ```
3. 运行指定的Linux发行版
   ```
   wsl -d <DistributionName>
   ```
4. 打包并导出WSL镜像为tar文件，并存放在当前目录
   ```
   wsl --export <DistributionName> <xxx.tar>
   wsl --export Ubuntu Ubuntu.tar
   ```
5. 手动导入WSL镜像，并设置为WSL2版本
   ```
   wsl --import <DistributionName> <ImportPath> <PathToDistribution\xxx.tar> --version 2
   wsl --import Ubuntu F:\Virtual_Machines G:\Virtual_Machines\Ubuntu.tar --version 2
   ```
6. 更改手动导入WSL的默认启动用户(wsl.conf原本是否存在均可)
   ```
   myUsername=<YourUserName>
   myUsername=csy-wsl
   echo -e "[user]\ndefault=$myUsername" >> /etc/wsl.conf
   wsl --shutdown
   ```
7. 注销WSL发行版
   ```
   wsl --unregister <DistributionName>
   ```

# zsh相关
1. 安装zsh
   ```
   sudo apt install zsh
   ```
2. 安装oh-my-zsh
   ```
   sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
   ```
3. 安装powerlevel10k
   ```
   git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
   sudo vim ~/.zshrc
   ZSH_THEME="powerlevel10k/powerlevel10k"
   ```
4. 安装插件
   1. zsh-autosuggestions
   ```
   git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
   sudo vim ~/.zshrc
   plugins=(
    # other plugins...
    zsh-autosuggestions  # 插件之间使用空格隔开
   )
   source ~/.zshrc
   ```
   2. zsh-syntax-highlighting
   ```
   git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting 
   sudo vim ~/.zshrc
   plugins=(
    # other plugins...
    zsh-syntax-highlighting  # 插件之间使用空格隔开
   )
   source ~/.zshrc
   ```
   3. z
   ```
   sudo vim ~/.zshrc
   plugins=(
    # other plugins...
    z  # 插件之间使用空格隔开
   )
   source ~/.zshrc
   ```

# 软件源更新
1. 更换清华软件源
   https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/


# Qt下载地址
   https://download.qt.io/new_archive/qt/


# Vim相关
 配置文件路径 /etc/vim/vimrc
 set nu
 set cursorline
 set ta...


# Linux C 

## man命令参数
   数字1 -- Linux命令；

   数字2 -- 系统调用；

   数字3 -- 标准C库函数；


# Yoga Info
## 进入BIOS -- F10

## 临时更改启动介质 -- F12

## 硬件信息
AMD Ryzen 7 5800H with Radeon Graphics
SSD -- 1T -- C盘 - 442.54G D盘 - 390.63G Ubuntu - 97.66G
