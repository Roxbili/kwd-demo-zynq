# zynq 下运行需要注意的问题

## root下python3.5的问题
1. 在```/usr/bin```下创建软链接，指向conda中的python3.5的可执行文件

## 显示问题
1. 安装vnc
    ```bash
    sudo apt install tightvnserver
    sudo apt install xfce4 xfce4-goodies
    ```

2. 安装字体
    ```bash
    sudo apt-get install xfonts-base
    ```

3. 使用vncserver命令创建vnc，然后kill，然后修改配置文件
    ```bash
    vncserver
    vncserver -kill :1
    vim ~/.vnc/xstartup
    ```
    在最后添加
    ```bash
    startxfce4 &
    ```

4. 给root x-window访问权限(不确定是不是这个修好的，但应该是xhost命令，使用的时候基本都报错，但是莫名其妙好了)
    ```bash
    xhost LOCAL:root
    ```
    备选方案：
    ```bash
    xhost LOCAL:fanding
    xhost + root
    xhost +
    ```