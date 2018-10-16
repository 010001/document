manjaro 无效或已损坏的软件包

问题如下：

安装typora失败，原因如下：

typora: signature from "lilac (build machine) <lilac@build.archlinuxcn.org>" is unknown trust



解决方法为：

[archlinuxcn]
SigLevel = Optional TrustedOnly
#SigLevel = Never
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch

修改/etc/pacman.conf，将原有的SigLevel=××××××注释掉，添加SigLevel = Never即可。
所有的SigLevel都要修改！
如果害怕安全问题，可以在搞定这个包之后，再取消注释，恢复原来的SigLevel