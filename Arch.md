# Arch Linux

## UEFI启动前

### 镜像下载

我们可以先从官网上[下载](https://archlinux.org/download/)Arch的镜像

![image-20220627200014004](https://s2.loli.net/2022/06/27/WyDCdnFhoetM7lX.png)

随便选一个即可

下过来之后用rufus烧录一下启动盘，默认选项不用管就行，在第一栏选择自己的u盘，第二栏选择镜像文件，至于是用ISO还是DD模式，我反正用ISO没报错，如果怕出错就用DD，稳定一些

烧完之后插进电脑里，接着我们要使用uefi启动u盘，确保进入BIOS之后设置Security Boot为Disable，即关闭了安全启动模式

- 如果是Win10，那么按着Shift不松点击重启按钮，就可以进入高级启动页面，首先先选择一下疑难解答->高级选项->uefi啥啥的点一下，之后重启再一次同样步骤进入高级启动，接着点击使用设备->USB UEFI啥的，然后在弹出的页面中选择自己的u盘即可
- 如果是其他windows设备，那么就先百度进入BIOS界面，然后找找肯定会有一个Boot Mode的地方将其改为UEFI Only，然后再将类似CSM的地方设置为Enable开启兼容模式，重启之后疯狂按f12，进入一个Boot Menu，然后选择USB HDD什么的，选择自己的U盘即可

### uefi启动

如何判断是否通过uefi启动成功？首先我们会看到grub界面是十分简陋的而不是非常好看的Arch标志内容，类似这样

![img](https://s2.loli.net/2022/06/27/iQyHdNCMPAKh37Z.jpg)

然后就是通过`ls /sys/firmware/efi/efivars`看看这个目录存不存在，如果不存在那么一定不是uefi启动

## 启动盘时期

默认现在我们已经通过uefi从u盘启动，在进入grub之后经过一段时间的乱七八糟内容之后，我们看到了tty1界面

![image-20220627192707793](https://s2.loli.net/2022/06/27/ulKB9Ivg4zYiQMN.png)

### 网络

在进行所有内容之前，我们需要先连接网络，判断一下网络是否被锁了

```text
# rfkill list  
--------------
0: phy0: Wireless LAN
    Soft blocked: yes
    Hard blocked: yes
```

如果出现以上内容，可以调节网卡开关打开它。如果没有开关，那就使用以下命令：

```text
# rfkill unblock wifi
```

![image-20220627193126334](https://s2.loli.net/2022/06/27/5FsaXuzmZyJbMql.png)

这样就是正常的

```text
root@archiso iwctl   //会进入联网模式
[iwd]# help    //可以查看帮助
[iwd]# device list    //列出你的无线设备名称，一般以wlan0命名
[iwd]# station wlan0 scan    //扫描当前环境下的网络，不会回显，但是确实已经扫描到了
[iwd]# station wlan0 get-networks    //会显示你扫描到的所有网络
[iwd]# station wlan0 connect [网络名称]
password:输入密码
[iwd]# exit    //退出当前模式，回到安装模式
```

### SSH

Arch启动盘的安装环境默认就是打开了SSH服务的，因此在设置好网络之后，我们可以直接通过ssh连接方便截图和其他操作

1. 在当前安装环境下输入`passwd` 为当前环境设置密码
2. 执行`ip -brief address`查看当前ip地址
3. `ssh -o StrictHostKeyChecking=no root@<刚刚查看的IP地址>`并输入刚刚设置的密码（或者使用各种ssh连接工具），这时候就可以发现已经连接上了

### 时区

接着设置一下时区吧

![image-20220627193830432](https://s2.loli.net/2022/06/27/nENY2GIT3vfZcpi.png)

### 国内镜像源

`reflector --country China --age 72 --sort rate --protocol https --save /etc/pacman.d/mirrorlist`则将最新的镜像源更新为国内的，保存在/etc/pacman.d/mirrorlist目录下

### 分区

接下来就是重头戏了，我们要正式开始安装，Arch内置了cfdisk工具用于我们的分区工作

为了知道我们应该分区到哪里去，我们需要先通过`fdisk -l`查看一下当前连接的硬盘内容

![image-20220627202158698](https://s2.loli.net/2022/06/27/qrgQu12NTct5bAO.png)

我们要将系统装在SSD上，因此我们选择`cfdisk /dev/sdb`

![image-20220627204624458](https://s2.loli.net/2022/06/27/BVibqMy6PteAUCv.png)

> 上面显示的是我manjaro的分区记录，直接删掉即可，如果本来有什么别的分区，或者根本没有分区，那么先选一下gpt分区表，然后差不多也会进入我这个界面，如果最前面不是free space就将不是的全部delete即可

![image-20220627205032256](https://s2.loli.net/2022/06/27/LDRTrC4yMQGPfUc.png)

删完之后就是这样了

接着选择New，然后输入300M分给启动分区，接着选择Type，选择EFI System

![image-20220627205413197](https://s2.loli.net/2022/06/27/731wHQUdJPsyGbu.png)

![image-20220627205322220](https://s2.loli.net/2022/06/27/3nXG4zIht1bCi8D.png)

然后建立8G的Swap分区和512G的根目录分区

![image-20220627205924144](https://s2.loli.net/2022/06/27/rAnHEuxP9Dedpt8.png)

分完之后选择Write确定分区内容，接着退出Quit，然后可以使用lsblk查看一下是否分区成功了

![image-20220627211828129](https://s2.loli.net/2022/06/27/GVTZtJ5Qr8z4l6a.png)

当然这只是名义上的分完了，想要分区内容有效果，我们还需要指定各分区的文件系统格式

```shell
mkfs.vfat /dev/sdb1
mkswap /dev/sdb2
mkfs.xfs -f /dev/sdb3  # 这里可以不使用xfs的文件系统，btrfs是一个不错的选择
```

![image-20220627212151664](https://s2.loli.net/2022/06/27/73Yfvyejdrgkw1n.png)

![image-20220627212245219](https://s2.loli.net/2022/06/27/3qQ7sKzRjL5BeFO.png)

以上是分区结果

### 安装

分区完成之后，我们就需要正式开始安装系统了，首先我们需要将刚分完的分区挂载上，然后直接在挂载的内容上进行安装

```text
mount /dev/sdb3 /mnt  # 必须先挂载上root分区
mkdir -p /mnt/boot/efi  # 创建启动分区目录
mount /dev/sdb1 /mnt/boot/efi  # 然后是启动分区和swap分区
swapon /dev/sdb2
```

![image-20220627212740439](https://s2.loli.net/2022/06/27/6Xt4xOLMdGUi3hW.png)

然后在挂载上的`/mnt`上安装必要的内容

`pacstrap /mnt linux linux-firmware linux-headers base base-devel vim git bash-completion`

等待ing….完成之后，这样基本的内容就已经安装完了，然后我们生成一下必要的表文件，就可以进入系统了

```text
genfstab -U /mnt >> /mnt/etc/fstab  # 生成文件系统表文件
```

### 新系统

```text
arch-chroot /mnt
```

然后按照惯例设置时区和语言

```text
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
hwclock --systohc  # 时区
vim /etc/locale.gen  # 语言，然后将en_US.UTF-8 UTF-8和zh_CN.UTF-8 UTF-8取消注释
locale-gen  # 生成本地语言信息
```

除此之外，一些个性化的内容也是需要搞上的

```text
vim /etc/locale.conf  # 语言的环境变量
-------------------------
LANG=en_US.UTF-8

vim /etc/hostname  # 主机名
---------------------
archlinux(也可以写成你想要的主机名)

vim /etc/hosts  # Hosts文件
--------------------
127.0.0.1   localhost
::1         localhost
127.0.1.1   archlinux.localdomain archlinux   # 这里的archlinux是主机名
```

### grub

当前我们的系统还是跑在启动盘上的，我们如果想要通过正式启动新系统，安装一个Grub是必要的，因此下一步就是安装并配置grub，并且将其配置到启动分区上

```text
pacman -S grub efibootmgr efivar networkmanager intel-ucode  # 安装相关包
grub-install /dev/sdb  # 安装grub
grub-mkconfig -o /boot/grub/grub.cfg  # 创建配置文件

systemctl enable NetworkManager  # 为了之后启动可以联网
```

然后可以再通过`passwd`设置一下root用户密码，然后就可以重启了！（其他什么事情都不需要改，直接无脑reboot即可）

```text
exit

umount /mnt/boot/efi
umount /mnt  # 记得卸载，注意顺序

reboot
```

> 但是我们会发现，虽然现在看上去很完美，启动也没有什么问题，但是一旦我们将存有新系统的硬盘从当前电脑拔出，再次插入时，会发现怎么也无法在BIOS中找到启动的arch项，如果你那就需要借助安装盘重新对新的电脑进行grub的初始化，从新的电脑中启动安装盘，接着像刚刚一样挂载，安装grub即可（由于之前我们已经在**新系统**中安装过grub了，所以这个过程不需要联网也可）
>
> ```shell
> lsblk -f  # 看一下需要挂载的SSD分区（sdb或sda）
> mount /dev/sdb3 /mnt
> mount /dev/sdb1 /mnt/boot/efi
> swapon /dev/sdb2
> arch-chroot /mnt  # 直接进系统
> grub-install /dev/sdb  # 安装
> grub-mkconfig -o /boot/grub/grub.cfg  # 创建
> # 接着重启即可
> ```
>
> 当然上述方法非常的治标不治本，因此我们急需要一种更加彻底的解决方案
>
> 其实解决的方式非常简单，只需要在`grub-install`时增加一个`--removable`选项即可，详见[官方解释](https://wiki.archlinux.org/title/Install_Arch_Linux_on_a_removable_medium_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))
>
> ```shell
> grub-install /dev/sdb --removeable
> ```

## 无GUI时期

重启系统之后，同样还是通过uefi启动新系统，我们会发现已经需要通过用户名和密码登录了，这时候我们只需要输入root+之前设置的密码即可登录系统，同样的，为了调试和安装的方便，我们同样要对新系统安装ssh

### 联网

当然新开的系统同样是没有网络的，之前我们特地下载了NetworkManager，因此我们现在可以直接通过`nmtui`来进行快速的联网设置，输入之后选择`Activate a connection`即可在简陋的图形化界面进行联网设置

### 国内镜像

和之前一样，先设置一下镜像，以免乱花流量钱

```text
vim /etc/pacman.d/mirrorlist
----------------------
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
Server = http://mirrors.163.com/archlinux/$repo/os/$arch
Server = http://mirrors.aliyun.com/archlinux/$repo/os/$arch

pacman -Syy
```

### SSH

```text
pacman -S openssh
systemctl start sshd
ip -brief address

vim /etc/ssh/sshd_config
--------------------------------------
# 将下列的语句值改为yes
PermitRootLogin yes
```

一气呵成

### 个人用户

```shell
useradd --create-home tsundere  # 用户名
passwd tsundere  # 设置密码
usermod -aG wheel,users,storage,power,lp,adm,optical tsundere  # 授权
```

### ArchLinuxCN

这是中文社区驱动的存储库，还是比较牛逼的，反正配置一下也不会怎么样

```text
vim /etc/pacman.conf
--------------------------------------
# 在最后添加
[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch 

pacman -Sy  # 刷新一下pacman使配置生效
pacman -S archlinuxcn-keyring  # 导入一下GPG key
```

### 显卡声卡驱动

```text
pacman -S xf86-video-intel vulkan-intel mesa
pacman -S alsa-utils pulseaudio pulseaudio-bluetooth cups
```

### 字体

可以选择自己喜欢的字体即可

```shell
pacman -S ttf-dejavu ttf-droid ttf-hack ttf-font-awesome otf-font-awesome  # 英文
pacman -S noto-fonts noto-fonts-extra noto-fonts-emoji noto-fonts-cjk wqy-zenhei wqy-microhei  # 中文
```

接下来我们需要打开字体引擎，是我们下载的字体可以生效

```text
vim /etc/profile.d/freetype2.sh
--------------------------------------------
# 取消注释最后一句
export FREETYPE_PROPERTIES="truetype:interpreter-version=40"
```

### 图形化

终于到了最激动人心的图形化界面阶段，本次我们采用的是KDE桌面，什么牛马Gnome，狗都不用！

```text
pacman -S xorg  # 显示服务X11
pacman -S plasma sddm konsole dolphin ark flameshot  # 从前往后分别是：桌面界面，登录管理器，终端，文件管理器，解压工具，截图工具
systemctl enable sddm  # 设置sddm登录
```

接下来就可以重启啦，不出意外的话就可以看到闪亮亮的新登录页面了

## Plasma时期

在进行接下来所有的工作之前，我们都需要进行一个`sudo pacman -S yay`先把aur的包管理器给他下过来先

### 输入法

Linux最让人头痛的莫过于输入法的各种坑了，想当年琢磨Gnome的输入法的时候就险些被坑的够呛，同时没有输入法显然什么都干不了，因此在正式启动系统，看到桌面之后，所需要做的第一件事就是赶紧将输入法给部署好了。

本次采用的是fcitx5的屌炸天输入法体验，使用起来说起来十分简单，但是真的弄起来也是废了我一番功夫

首先需要下载需要的包

```shell
yay -S fcitx5-im fcitx5-chinese-addons fcitx5-pinyin-zhwiki fcitx5-pinyin-moegirl  # 从前往后，分别是ficitx5本体，可选的一大堆中文输入法和两个字库
```

装好之后不急着启动，我们还需要配置一下配置文件，保证一些奇怪的应用程序里面也可以使用我们的输入法

```shell
vim .xprofile
-------------------------
export QT_IM_MODULE=fcitx
export GTK_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

然后一定要重启，重启之后我们应该会发现任务栏里面有一个键盘图标，咱们右击->Configure然后就会进入输入法的配置界面

![image-20220629040343846](https://s2.loli.net/2022/06/28/YnPDmKevZAsrqjF.png)

然后在下一个页面找到**简体中文（中国）**的一栏，选择pinyin

![image-20220629040540513](https://s2.loli.net/2022/06/28/Sb6ho2Ltne4FA5p.png)

然后点击右下Apply，关闭窗口，在任务栏右击->Restart重启输入法，然后我们就可以快乐的打字了

#### 个性化背景色

除此之外，我们还可以安装`fcitx5-material-color`这个包，他可以让我们的输入法变得更加好看

下完这个包之后，我们只需要修改配置文件，就可以给我们的输入法换种颜色

```text
vim ~/.config/fcitx5/conf/classicui.conf
---------------------------
# 垂直候选列表
Vertical Candidate List=False

# 按屏幕 DPI 使用
PerScreenDPI=True

# Font (设置成你喜欢的字体)
Font="思源黑体 CN Medium 13"

# 主题
Theme=Material-Color-Pink
```

其中主题也有很多种供我们选择

- Material-Color-Pink
- Material-Color-Blue
- Material-Color-Brown
- Material-Color-DeepPurple
- gou weiMaterial-Color-Indigo
- Material-Color-Red
- Material-Color-Teal
- Material-Color-Black
- Material-Color-Orange
- Material-Color-SakuraPink

使用SakuraPink大概是这个效果

![image-20220629041115204](https://s2.loli.net/2022/06/28/6OVvw2Cdl3sHXPy.png)

### Typera+Picgo

为了使笔记能够正常的记下去，因此在进入系统的第一件事不是别的，正是先将该死的Typera准备好了，而这个东西搞得我也是十分头晕，尤其是图床的部署，简直是乱七八糟的错误都来了

首先还是下载一下Typera，要注意的是通过aur下载的链接是指向`typera.io`的，因此有时候会出国内网络无法访问的情况，这时候之前部署的ArchlinuxCN就派上用场了，通过他下过来的包就十分的良好够味

打开Typera，激活之后下一步就是Picgo的部署

一开始我直接通过aur下桌面端的Picgo程序，但是下过来发现找不到调用的接口在哪，而且100多M的大应用显然也不符合我的极简风格，因此找到了发布在npm上的核心版picgo

#### pnpm

由于包在npm上面，因此在下载picgo之前我们还得下一个包管理器

```shell
yay nodejs
yay pnpm
```

其实会惊讶的发现居然不需要下载npm也可以直接使用pnpm了，这也可以算是一个linux包管理机制的用户福利吧

接着我们使用之前还需要先初始化一下pnpm

```shell
pnpm setup
pnpm i -g picgo
```

不知道为什么居然全局安装连sudo都不需要加了，加入第二条指令报错的话可以尝试重启一下，或者检查环境变量`$PNPM_HOME`是否存在

然后我们需要在控制台设置一下上传图床，只需要输入`picgo set uploader`接着选择需求图床即可

![image-20220629043919662](https://s2.loli.net/2022/06/28/jPNzsvxG1dUmpy4.png)

然后我们需要知道下载到的全局picgo跑到哪里去了，因此我们可以使用`echo $PNPM_HOME`或者是`which picgo`查看一下picgo被下载到什么地方去了

![image-20220629043508918](https://s2.loli.net/2022/06/28/UhaIdjQVyz1ck7G.png)

知道了位置，我们直接在Typera里面设置上传命令即可（突然想起来好像也可以直接`picgo u`的说。。。。我是个傻子）

![image-20220629044046803](https://s2.loli.net/2022/06/28/1ujHLnp3k4F7zNa.png)

测试一下即可

### Zsh

美好的终端不能少了Zsh的帮助，这次我不会再用什么牛马Oh my Zsh了，不妨自己从零开始配置一下Zsh的内容

首先当然是是下载和启用

```shell
yay -S zsh zsh-autosuggestions zsh-syntax-highlighting zsh-theme-powerlevel10k zsh-completions
chsh -s /usr/bin/zsh
```

之后我们只需要注销并重新登录，打开终端，就可以进入Zsh的配置页面了

#### 原生配置

由于都是英文，在网上也没找到翻译的比较好的总结，于是不得不自己手动翻译一下

![image-20220628232317060](https://s2.loli.net/2022/06/28/EjCaBD5KwHZbYO6.png)

之后会跳出来四个选项，大概长这样

![image-20220628232607031](https://s2.loli.net/2022/06/28/jYrvcT1xm7swMFH.png)

其选项意思如下

- `1`：设置命令历史记录相关的选项

  - 进入后
  - `1`：shell内最多可以有多少行命令和输出内容（比如Bash默认就是500，这里默认值为1000）
  - `2`：历史记录存放的位置（默认`~/.histfile`）
  - `3`：历史记录文件最多可以存放多少历史命令（默认1000）

- `2`：设置命令补全系统，无脑选1就完了，其正式的翻译如下

  > The new completion system (compsys) allows you to complete commands, arguments and special shell syntax such as variables.  It provides completions for a wide range of commonly used commands in most cases simply by typing the TAB key.  Documentation is in the zshcompsys manual page. If it is not turned on, only a few simple completions such as filenames are available but the time to start the shell is slightly shorter.
  >
  > 新的完成系统（compsys）允许你完成 命令、参数和特殊的shell语法，如变量。 它提供了 在大多数情况下，只需输入TAB键，就可以完成各种常用的命令的编写。输入TAB键即可完成。 文档在zshcompsys手册页中。如果不打开它，只有一些简单的补全功能，如文件名，但启动shell的时间会稍短。

- `3`：设置热键，可以在命令行里面使用vim，实在是太棒了！（进入后选1->v）

- `4`：选择各种常见的选项，只需要选择“On”或者“Off”，这个之后会详细说明，里面给出的内容可以全部设定为开启

- `0`：退出，并使用空白（默认）配置

- `a`：终止设置并退出

- `q`：退出

选完之后就会进入最原始的zsh界面了，接下来我们就来看看刚刚那花里胡哨的操作到底对Zsh干了什么奇怪的事，以及接下来我们应该如何进一步的进行我们自己个性化的操作

#### setopt

在完成了无脑的窗口化选数字设置zsh之后，如果我们现在打开`~/.zshrc`，会发现里面已经多了一些内容了，之后我们 如果对之前配置的内容不满意，只需要删掉这个`.zshrc`文件之后重启终端，之前的选项就会重新出现了

当然，在学习了如何自己手动配置zsh之后，其实我们也不需要这种鸡肋的方式来完成少量的配置工作了，下面是我初始化之后的`zshrc`文件内容

```shell
# Lines configured by zsh-newuser-install
HISTFILE=~/.histfile
HISTSIZE=100000
SAVEHIST=1000
setopt autocd beep extendedglob nomatch notify
bindkey -v
# End of lines configured by zsh-newuser-install
# The following lines were added by compinstall
zstyle :compinstall filename '/home/tsundere/.zshrc'

autoload -Uz compinit
compinit
# End of lines added by compinstall
```

里面有很多我们看不懂的东西，不如我们首先先聚焦于其中的`setopt`这一行，这个`setopt`掌握着zsh的所有启用选项，而每一个选项都对应着一个zsh在shell方面的功能，比如这里面的autocd就可以让我们不借助cd指令直接跳转到某一个目录内，zsh自动帮我们转译了cd指令，而相对应的，对于zsh自带的一些默认开启的选项，我们也可以通过`unsetopt`来取消设置

对于zsh中所有的选项内容，可以通过[zshoptions](https://zsh.sourceforge.io/Doc/Release/Options.html)来获取，或者在命令行输入`man zshoptions`查看，而对于系统默认的配置项，我们可以通过输入`emulate -lLR zsh`查看（如果去掉l选项则是直接恢复默认设置），其中所有的选项均不区分大小写

例举一些有用的配置项

- `NO_CASE_GLOB`TAB补全不区分大小写，比如输入`d<Tab>`可以匹配到`Desktop`

- 历史记录相关，有一大堆选项

  ```shell
  # 多个会话共享历史记录文件
  setopt SHARE_HISTORY
  # 添加历史记录，而非覆盖
  setopt APPEND_HISTORY
  # 立即更新历史记录
  setopt INC_APPEND_HISTORY
  # 去除第一个重复记录
  setopt HIST_EXPIRE_DUPS_FIRST
  # 去除重复记录
  setopt HIST_IGNORE_DUPS
  # 浏览时跳过重复记录
  setopt HIST_FIND_NO_DUPS
  # 去除空白记录
  setopt HIST_REDUCE_BLANKS
  ```

  看上去都挺有用，就都加上了

- `CORRECT/CORRECT_ALL`指令自动更正，减少手误概率

#### 别名

除了正常的alias，zsh同样对别名功能做了一次升级

1. 全局别名，正常的alias只对出现在指令开头的别名有效，比如`alias ll=ls -al`，那么在我们使用的过程中，`ll`就没问题，但是`sudo ll`就会出问题，但是如果我们设置别名时使用`alias -g ll=ls -al`，那么任何指令只要出现了ll都会被替换为`ls -al`
2. `which`显示别名替换，我们可以通过`which ll`来显示`ll`别名代表的含义，但是如果`ll`是全局别名，那么会优先替换`ll`为`ls -al`，使得显示并不正常，我们可以通过转译第一个字符避免意料之外的显示

其他的别名直接迁移即可

```shell
alias tree='tree -a -I .git'
alias -g v='nvim'
alias -g vi='nvim'
alias ls='logo-ls'
alias ll='exa -l --color=auto'
alias la='exa -ahl --color=auto'
alias vz='v ~/.zshrc'
alias sz='exec zsh'
alias zb='neofetch | lolcat'
alias c='clear'
alias df='df -h'
# Git Alias
alias glog='git log --graph --pretty=oneline --abbrev-commit'
alias gac="git add . && git commit -m"
alias gi="git init && gac 'Initialization'"
alias gpm="git push origin master"
alias glm="git pull origin master"
```

#### 指令补全

除了之前配置的通过选项来配置指令之外，zsh强大的指令补全功能还可以玩点更有意思的花样

在此之前，请确保你的`.zshrc`文件存在一行`autoload -Uz compinit && compinit`或者类似脚本，他代表在zsh启动时初始化指令补全系统

可以通过添加两行代码实现部分补全，例如`cd /u/lo/b⇥`会变成`cd /usr/local/bin`

```shell
# 部分补全的建议策略
zstyle ':completion:*' list-suffixes
zstyle ':completion:*' expand prefix suffix
```

最牛逼的还是能够根据已经输入的内容进行历史记录搜索，我们可以在配置文件中加上下述代码

```shell
bindkey "^[[A" history-beginning-search-backward
bindkey "^[[B" history-beginning-search-forward
```

#### 插件部分

我们可以直接搜索插件名称，比如这里的`syntax-highlighting`和`autosuggestions`两个插件，虽然这些都是`oh-my-zsh`内的插件组，但是AUR上面已经有大佬将内容包装完成了，我们只需要直接`yay zsh-[插件名称]`就可以找到相应插件

直接将内容复制到`~/.zshrc`即可

```shell
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/share/zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme
```

接着`source ~/.zshrc`即可进入配置p10k

还有一些不能通过此类方法下载的插件，比如`autojump`，则我们同样要先去下载一下需要的包

```bash
yay autojump  # 选择archlinuxcn那个即可
```

安装之后他会提醒我们

![image-20220629083151508](https://s2.loli.net/2022/06/29/gYK9yR5DzV8wbIa.png)

按照红框框里面的操作将语句粘贴到。`~/.zshrc`里面即可

其他乱七八糟的插件都可以类似完成

### 桌面美化

先来一张预览图

![2022-07-05_16-47](https://s2.loli.net/2022/07/05/HxbPrGXnjWkqylf.png)

#### 主题

主题部分指的是大多数窗口的色调及包括鼠标，图标等一系列总之可以在设置内的Appearence里面可以直接设置的内容

因为可以直接在设置内直接设置，因此这一步相对来说就显得比较简单了，更重要的是几乎所有的主题都可以在[KDE Store](https://store.kde.org/browse/)内直接通过ocs-url直接下载到本地指定的目录，因此甚至不用担心设置内会找不到需求的主题内容

当然其中的问题当然还是有的，在不出意外的正常情况下，只需要针对Appearence中的每一项，去KDE Store内寻找到指定内容的自己喜欢的主题直接点击Install自动下载安装即可，非常省心

![image-20220706001825520](https://s2.loli.net/2022/07/06/DUbEt3cBXjCVGw5.png)

![image-20220706002114939](https://s2.loli.net/2022/07/06/dJsx1qED8HwMFKv.png)

如果觉得KDE Store内浏览速度太慢，或者感觉过于麻烦了，我们甚至可以直接通过设置内右下角的`Get New xxx`来在线加载KDE Store从而方便的下载主题内容

![image-20220706002516204](https://s2.loli.net/2022/07/06/rSaWCnFHhsuRjJ3.png)

当然在设置的过程中还是会遇到很多问题，下面是部分问题解决方案

##### 无法通过网页商店自动安装

具体是会出现类似这样的报错

![image-20220706002846869](https://s2.loli.net/2022/07/06/2hi5QgsJPyafvKo.png)

其实就是ocs-url没有装，`yay ocs-url`装一下就好了

##### Application无法找到在线商店

![image-20220706010330211](https://s2.loli.net/2022/07/06/VGftRok5sudMlFN.png)

这时候可以先`yay kvantum`，这玩意是一个专门的控制器，下载完之后就会多了一个Kvantum Manager，可以通过其对通用的应用程序界面主题做统一调整，里面不仅适配了多种打包类型的应用场景，我们还可以在KDE Store内直接下载配套的主题类型，在Kvantum Manager里面直接导入就行了

##### 配置Global Theme之后桌面不见了

![image-20220706010911592](https://s2.loli.net/2022/07/06/KlDEZkC7xmJWOyo.png)

具体情况估计就是选择了Desktop layout这个选项，这个选项千万不要选，桌面的布局之后通过lette dock设置，现在先不用管，同时这么多选项中其实是可以不配置Global Theme的，因为其就是单纯的包含了一下一套的下面几个选项的内容而已，当然我们也可以通过先设置全局主题之后再进行每一个选项的微调

下面是我的配置：

- Application Style：kvantum -> moe
- Plasma Style：Moe
- Colors：Moe
- Window Decorations：Freeze
- Fonts：Noto Sans
- Icons：Tela pink
- Cursors：Oreo Pink Cursors
- Splash Screen：ArchLinux(Moe)/BeautifulTreeAnimation
- 其他不改动

#### 窗口动画

由于KDE基本定死了几种动画的模式，因此我们自由发挥的空间也相对减少了，最主要的修改就是在Workspace Behavior->Desktop Effects->Appearance内的选项，如果看不懂直接全勾上就完了，之后就会发现窗口的移动，最小化，关闭等等莫名其妙就有了一堆炫酷的 动画效果，还是十分一键懒人模式的

此外窗口的轮转动画需要在设置->Window Management->Task Swicher->main->Visualization->下拉框选择自己喜欢的样式即可（Alt+Tab触发）

#### 布局

说到仿Mac的布局，就不得不提一下著名的Latte Dock了，这个基本上已经可以算是官方唯一指定Dock了，甚至连KDE Store里面都专门给他分了一块叫Latte Theme，可见其的认可度

当然这不是说Plank不能用，只是比起Latte，只能说其认可度还是低了些

在安装完Latte之后（指`yay latte-dock`）只需要控制台直接输latte-dock即可进行首次启动，然后我们会发现屏幕底部出现的标志性的初始dock栏，我们可以通过右击Dock栏->Configure Latte...进入Latte Dock的配置页面

不过在开始正式的Latte Dock布局之前，我们还是需要先将原有的桌面布局给清空一下，初始时原有自带的Breeze全局主题附赠了一个Plasma风格的Panel栏，这种Panel的可定制化程度实在是有限，因此我们直接将其删去，我们只需要在Panel上右击->Enter Edit Mode，之后鼠标移到底部找到More Option->Remove Panel即可

打开配置页之后，我们首先先修改一下桌面的整体布局主题，点击Layouts Editor->Import->Import From KDE Online Store然后搜索自己喜欢的主题即可，我此处选用的是Moe Layout，之后选择到下载过来的主题布局，选择Switch即可应用

当然，默认的布局如果感觉还行那就不用修改了，但是如果需要进行修改的话，尤其是底部的Dock栏，那我们就首先需要对Latte的整体设计做一个了解

##### 原理

Mac最大的一个设计点就是其不同于Windows自己独有的Dock栏，在其中可以放置一些常用的软件便于快捷启动，而大多数系统都存在的Panel则专注于显示当前电脑的各种状态，并且置于整个屏幕的顶端，这样的设计不仅符合用户常识化的应用习惯，更处处体现一股高大上的气息

而Latte进一步对于Dock和Panel添加了更多的个性化设置，同时其结合了KDE原有的小部件，在设置了个性化的Dock和Panel之后，我们就可以在其中添加各种KDE原生的小部件（但是不保证适配性，下一节会提到）

##### 个性化Dock/Panel

不同于原生Plasma桌面的直接右击添加Panel，在Latte中，我们需要在配置文件中，在Layouts Editor->Dock,Panels...->New来添加新的Dock或者Panel，对于每一个Dock/Panel，都可以选择位于屏幕的上下左右四个方位，对于每个方位可以选择两边、中间或者平铺四种布局，还可以给Dock/Panel设置比如响应触摸放大，背景大小，透明度等一系列设置，另外，在Dock或者Panel中可以根据自己喜欢添加各种Plasma原生的Widgets或者是应用，还是十分方便的

#### 部件

KDE另一个强大之处就在于其各种令人眼花缭乱的小部件（Widgets），你可以根据自己的需求将小部件放在桌面上或者是Panel/Dock中，制作精良的小部件会根据用户放置位置的不同呈现出不同的形态，根据用户的行为执行不同的逻辑，展示不同的信息，提供良好的用户交互

然而实测下来，当我们安装了Latte之后，在其设定的Panel/Dock中添加的小部件在高分屏下会显示过小，因此我们在为Latte Dock/Panel添加小部件的过程中，最好借助Latte安装时自带的某些封装部件，在这些Latte原生部件中添加我们个性化的应用或部件

- Latte Tasks，这是Latte自带的专门用来放Dock应用的部件，将其添加到Dock栏中，之后将应用直接拖入Dock，出现+号图标松手则将指定应用添加给Latte Tasks管理，在这其中的应用可以更好的响应用户操作反馈，而且也不会出现图标大小奇怪的问题
- System Tray，这则是Latte用来专门显示系统状态的部件，但是唯一的坏处就是无法自己自定义设置显示的状态内容，也不能为其套娃添加小部件，不过其默认内置的状态也完全够用了，包括显示电量，剪贴板，应用状态等等，基本也已经满足各种需求了

另外我也自己装了几个效果还不错的其他小部件

- Legacy Application Launcher，用于显示主菜单和所有应用，当不想使用键盘时可以直接点点点打开应用和目录
- Event Calendar，集成了时间，天气，倒计时，日期等等部件并显示，等于是一个大杂烩，用于简单的显示还是比较方便的
- Tanslator，不用说了，无敌的翻译部件，再也不用打开网站翻译了
- Compact ShutDown，简单的关机按钮，比原生的关机少了花里胡哨的辅助按钮，符合我的极简风

当然还有很多各种各样功能的部件，不过暂时来说对于我这几个就完全够用了

#### GRUB

虽然作为单系统来说，GRUB的用处是越来越小了，但是并不妨碍我们对其进行美化，同时也是为之后可能安装双系统埋下伏笔

GRUB的主题可以从[pling](https://www.pling.com/browse?cat=109&ord=latest)官网上找到，一般来说，随便选一个下载之后，解压就会看到一个`install.sh`的文件，想办法执行他即可，但是如果想要自己手动配的话也不是不可以，就是步骤稍显麻烦

- 首先将主题解压缩之后整个丢到`/boot/grub/theme`这个目录中
- 然后我们需要知道，grub的执行原理是通过`/etc/default/grub`这个配置文件修改之后通过编译生成的`/boot/grub/grub.cfg`文件来控制真实的grub启动，之前我们通过`grub-install`实际上就是通过自动化的方式生成grub配置文件，之后执行的`grub-mkconfig`指令则是生成`grub.cfg`，知道了这一点，我们也就知道接下来需要修改的文件了
- 修改`/etc/default/grub`，在底部添加`GRUB_THEME="/boot/grub/themes/xxx/theme.txt"`注意一定要是`theme.txt`文件才生效，同时我想让grub的界面必须在经过我选择之后才进入boot，因此我还需要将`GRUB_TIMEOUT`这一配置项改为-1（如果为0则不显示grub）
- 接下来为了避免打和之前一样的一大串指令，我们需要`yay update-grub`把这个脚本下过来
- 接着`update-grub`即可自动生成`grub.cfg`

这样GRUB的主题也就配置完成了



### 系统问题

Linux最重要的就是折腾，因此新系统不可避免的会有一大堆奇奇怪怪的问题，下面列举了个人遇到的问题内容，以下改动如果不生效一律需要重启才会生效

#### 普通用户无法sudo

具体表现是使用`sudo xxx`的时候统一报错`xxx is not in the sudoers file. This incident will be reported`

其实原因也很简单，先用root用户找到`/etc/sudoers`文件，添加`xxx ALL=(ALL:ALL) ALL`即可（可以在任意地方）

#### 无法访问ntfs格式磁盘

刚进入系统的时候其实并不能访问ntfs类型的磁盘内容，因此需要我们下载一个`ntfs-3g`的包即可，`yay -S ntfs-3g`

#### 检测不到声卡

```shell
yay -S alsa-firmware sof-firmware alsa-ucm-conf
```

#### 双系统时间

```shell
timedatectl set-local-rtc 1 --adjust-system-clock
```

#### 代理无效

无论是直接`export ...`还是在`.bashrc/.zshrc`里面添加代理信息都是只应用终端上的，如果只是export甚至一关机就消失了，这是由于Linux加载环境变量的各种规则，想要在应用中同样适用桌面应用内，我们应该改动的是`/etc/environment`的内容

```shell
vim /etc/environment
-------------------------------------
#
# This file is parsed by pam_env module
#
# Syntax: simple "KEY=VAL" pairs on separate lines
#
export https_proxy=http://127.0.0.1:7890
export http_proxy=http://127.0.0.1:7890
export all_proxy=socks5://127.0.0.1:7890
```

#### nvim无法内部复制

鉴于还是nvim比较香，因此这里以nvim为例，vim可行性不得而知

我们需要先下载一个`xsel`，这个东西是为了用于操作linux的剪切板的，之后我们直接打开nvim就会发现居然直接就可以通过`"+y`复制到剪切板了

如果嫌这样还是太麻烦了，那么我们还可以只在配置文件中设置一下剪贴板的`set clipboard=unnamedplus`即可

```text
yay -S xsel
nvim ~/.config/nvim/init.vim
----------------
set clipboard=unnamedplus
```

#### 触摸板轻触无效

直接去设置里面改一下就好了`setting->Input Device->Touchpad->Tap-to-click`设置一下就好了

#### 蓝牙无法搜索

具体表现是蓝牙界面搜索不到内容，其实原因主要还是没有设置开机启动项

```shell
systemctl enable bluetooth
systemctl start bluetooth
```

#### Meta+D仅置顶桌面

 KDE比较恶心的地方就在于默认情况下`Meta+D`只会暂时置顶桌面而不是置顶桌面的同时最小化所有窗口，这就会导致虽然显示桌面了，但是并不能做到像是整理所有窗口的功能，一旦再通过`Alt+Tab`就会一下子一大堆之前的窗口重新冒出来，这显然是不合常理的

首先我们知道，KDE中所有的窗口界面的顶层控制器都是Kwin，因此我们需要针对其进行设置

首先进入设置->Window Management->KWin Scripts->MinimizeAll勾选上，之后进入设置->Shortcuts->Shortcuts->KWin->MinimizeAll修改为自定义快捷键`Meta+D`覆盖掉原本的`Display Desktop`即可

#### 大量打开方式被覆盖

问题的出现是我装了libreOffice之后几乎所有文本文件后缀的文件默认打开方式都变成了它，但是我的真实目的仅是通过它开一些word文件，这种耍流氓的做法让我十分不爽，急于在不删除这个应用的情况下，将乱开应用的问题彻底抹杀

有两种解决方案，第一种针对少量后缀被修改的情况，后一种针对大量后缀均被统一修改的情况

1. 设置->Application->File Associations，接着找到被修改的后缀，在Application Preference Order中调整默认启动应用（注意类别一项可以被展开）
1. 在`/usr/share/application`中找到乱默认启动的应用`xxx.desktop`（比如我就是`libreOffice-xxx.desktop`），注意有些desktop实际上是软链接，最好是通过`ls -al`来找到软链接原出处修改原始配置内容（比如ilbreOffice的真实`.desktop`在`/usr/lib/libreoffice/share/xdg/`这个路径下），之后打开这个文件，删除其中所有的`MIMETYPE`这一配置项，重启系统即可

#### Window Decorations在Chrome显示问题

一般来说就是比如Decorations设置的边缘透明但是Chrome中不显示透明，这时候其实跟系统关系不大，我们需要去Chrome的设置里面->Appearence->Use system title bar and borders勾选即可

如果觉得效果一般也可以设置一个较为理想的Chrome主题

#### VSCode github登录错误

由于vscode本来就在aur和官方库里面没有，同时又由于其实apt内有vscode，而使用apt的Linux系统大多都是Ubuntu，更重要的是Ubuntu默认都是Gnome桌面，导致vscode的登陆必须需要`gnome-keyring`才能正确登录，直接`yay -S gnome-keyring`即可

#### p10k终端图标过小

具体就是命令行前半段系统标志图标和当前家目录图标在高分屏下显示过小，其实就是字体没配对，Settings->Manage Profiles->选择自己的配置文件或者自己新建一个配置文件，Edit->Appearence->Font一栏修改字体为任意带Nerd的字体（如果没有就去下一个，比如`yay hack-nerd-font`）

#### `xdg-open: unexpected option '--'`

这是在ranger使用时打开一些神秘后缀的文件时出现的问题，主要还是ranger奇怪的默认配置文件搞得鬼，于是我们得修改一下其默认的配置文件

首先应当确保你曾经执行过`ranger --copy-config=all`这个指令，即在`~/.config/ranger`下存在几个默认生成的文件（如果没有就执行一下，也很简单）

之后找到生成出来的`rifle.conf`的文件，接着根据不同的要求，会有不同的几种解决方案

1. 只想让指定后缀的文件通过环境变量`$EDITOR`方式打开，则找到第一个出现`!mime ^text, label editor, ext xml|json|csv|tex|py|pl|rb|js|sh|php = ${VISU
   AL:-$EDITOR} -- "$@"`的地方，在php后学着加上所需要的指定后缀，重启ranger即可
2. 想让指定后缀的文件通过非`xdg-open`的指定方式打开，则学着类似`ext exe = wine "$1"`的样子自己写一个规则，满足`ext [后缀] = [打开指令] "$1"`的方式
3. 需要根据不同的需求用不同的方式打开指定后缀文件，则将2指令中的`=`后面改为`ask`，则选定文件之后会询问打开方式
4. 就想用`xdg-open`打开指定后缀文件，则去掉`label open, has xdg-open = xdg-open -- "$@"`一行的两个`-`符号

#### docker启动失败（failed to create endpoint ...）

原因是更新系统之后没重启，重启一下即可

#### 端口占用

1. `lsof -i:[目标端口]`获取占用进程PID，如果没有lsof就下一个`yay lsof`
2. 直接`kill -9 [PID]`即可

#### Nvidia显卡导致窗口动画消失

```shell
yay -S nvidia nvidia-settings lib32-nvidia-utils
```

之后重启电脑即可，详细可以查看https://archlinuxstudio.github.io/ArchLinuxTutorial

#### Nvidia停留在Graphical无法进入图形化

可能是之前使用过了`nvidia-xconfig`命令后移动到了另一台显卡不同的机器上启动，现在只需要删除`/etc/X11/xorg.conf`配置文件重启即可

#### Clash全线超时

其实就是系统时间和远程服务器时间对不上，也就是本地时间不对，可以到http://www.time163.com/看看是不是有问题，然后setting->Date & Time->Set date and time automatically勾选应用即可

#### VNC的爱恨情仇

第一次遇到不支持uefi的主板，没办法，我们只能用极为土味的方法，先把笔记本开在那里然后尝试台式机的远程桌面连接

然后查着查着就找到了VNC，这玩意确实符合我的要求，但是却不符合我这种奇葩的情况，导致出现了一堆问题

1. 获取`tigervnc`直接`yay -S tigervnc`就可以了
2. 接着我们要开启服务端的服务，输入`vncpasswd`设置密码
3. 开启服务端服务`x0vncserver -rfbauth ~/.vnc/passwd -Geometry 1920x1080`后面是连接端的分辨率
4. 新开一个终端然后`ip -brief address `获取本机的ip地址
5. 在本机下载[VNCViewer](https://sourceforge.net/projects/tigervnc/files/stable/1.12.0/)，然后启动之后连接界面上展示的端口和之前获得的ip

看上去似乎很美好，但是实际上你会发现不会有人让你使用`x0vncserver`这玩意开启服务端服务，而且这个模式不仅适配不了分辨率而且控制主机还无法共享剪切板，但是如果你尝试使用`vncserver`直接启动服务，可能就会发现连接的设备永远是只能展示一个带鼠标的黑屏，如何解决这个黑屏就成为了我们研究的关键

1. 其实问题的关键就是我们已经用我们的用户登录了图形化界面，而vnc本身是不支持同一个用户用多个图形化界面的，因此最关键的就是我们要关闭自己电脑的图形化界面开机自启动`sudo systemctl set-default multi-user.target`，设置启动等级为3

   > 之后需要恢复同样只需要`sudo systemctl set-default graphical.target`即可

2. 接着我们使用`vncserver :1`即可

看似很简单，然而花了我一个晚上的时间也不是吹的

#### Nvidia内存错误

新换了一个主板就是带感，赶紧试试可不可以启动系统，结果就给我报了一个内存错误

```shell
[    5.429675] nvidia-nvlink: Nvlink Core is being initialized, major device number 510

[    5.429718] traps: Missing ENDBR: _portMemAllocatorAllocNonPagedWrapper+0x0/0x10 [nvidia]
[    5.429816] ------------[ cut here ]------------
[    5.429817] kernel BUG at arch/x86/kernel/traps.c:252!
[    5.429828] invalid opcode: 0000 [#1] PREEMPT SMP NOPTI
[    5.429830] CPU: 9 PID: 948 Comm: modprobe Tainted: G           OE     5.18.0-arch1-1 #1 b71a70fe104889aac2f32556bc52f649da2881d2
[    5.429832] Hardware name: System76 Oryx Pro/Oryx Pro, BIOS 2021-09-23_b9b0e89 09/23/2021
[    5.429833] RIP: 0010:exc_control_protection+0xc2/0xd0
[    5.429837] Code: 8b 93 80 00 00 00 be f9 00 00 00 48 c7 c7 d3 ab 66 b5 e8 d1 01 50 ff e9 72 ff ff ff 48 c7 c7 ba ab 66 b5 e8 c7 31 fb ff 0f 0b <0f> 0b 66 66 2e 0f 1f 84 00 00 00 00 00 90 66 0f 1f 00 55 53 48 89
[    5.429838] RSP: 0018:ffffa9c3413b3bb8 EFLAGS: 00010002
[    5.429839] RAX: 000000000000004d RBX: ffffa9c3413b3bd8 RCX: 0000000000000027
[    5.429840] RDX: 0000000000000000 RSI: 0000000000000001 RDI: ffff9d195fa616a0
[    5.429841] RBP: 0000000000000003 R08: 0000000000000000 R09: ffffa9c3413b39d8
[    5.429842] R10: 0000000000000003 R11: ffffffffb5ecaa08 R12: 0000000000000000
[    5.429842] R13: 0000000000000000 R14: 0000000000000000 R15: 0000000000000000
[    5.429843] FS:  00007f0aa9bbe740(0000) GS:ffff9d195fa40000(0000) knlGS:0000000000000000
[    5.429844] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
[    5.429845] CR2: 00007f0aa8382000 CR3: 00000001063ce002 CR4: 0000000000f70ee0
[    5.429846] PKRU: 55555554
[    5.429847] Call Trace:
[    5.429848]  <TASK>
[    5.429849]  asm_exc_control_protection+0x22/0x30
[    5.429852] RIP: 0010:_portMemAllocatorAllocNonPagedWrapper+0x0/0x10 [nvidia]
[    5.429920] Code: 08 48 89 d0 48 89 0f 48 c1 e0 17 48 31 c2 48 89 c8 48 c1 e8 05 48 31 c8 48 31 d0 48 c1 ea 12 48 31 d0 48 89 47 08 01 c8 c3 90 <48> 89 f7 e9 38 0f 00 00 0f 1f 84 00 00 00 00 00 48 89 f7 e9 88 0f
[    5.429921] RSP: 0018:ffffa9c3413b3c80 EFLAGS: 00010202
[    5.429922] RAX: ffffffffc1eae5f0 RBX: 0000000000000010 RCX: 0000000000000000
[    5.429923] RDX: 0000000000000000 RSI: 000000000000002c RDI: ffffffffc20f7b70
[    5.429923] RBP: ffffa9c3413b3c98 R08: 0000000000000020 R09: ffffffffc20f7bf0
[    5.429924] R10: ffffffffc20f55d0 R11: 0000000000000000 R12: ffffffffc20f7b70
[    5.429925] R13: 00007f0aa8382dc0 R14: 000055916224ef30 R15: ffffa9c3413b3e20
[    5.429926]  ? portCryptoPseudoRandomGeneratorGetU32+0x30/0x30 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.429991]  _portMemAllocatorAlloc+0x2e/0x170 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.430054]  portCryptoPseudoRandomGeneratorCreate+0x16/0xb0 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.430117]  portCryptoInitialize+0x2a/0x40 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.430182]  portInitialize+0x2b/0x40 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.430246]  coreInitializeRm+0x24/0x90 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.430324]  RmInitRm+0x9/0x20 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.430399]  rm_init_rm+0x9/0x10 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.430472]  nvidia_init_module+0x22e/0x5b0 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.430517]  ? nvidia_init_module+0x5b0/0x5b0 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.430565]  nvidia_frontend_init_module+0x50/0x91 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.430616]  ? nvidia_init_module+0x5b0/0x5b0 [nvidia 5737a4bc014c2c47af46ebdec30e9ee078e09f14]
[    5.430663]  do_one_initcall+0x5a/0x220
[    5.430667]  do_init_module+0x4a/0x240
[    5.430670]  __do_sys_init_module+0x138/0x1b0
[    5.430672]  do_syscall_64+0x5c/0x90
[    5.430674]  ? exc_page_fault+0x74/0x170
[    5.430676]  entry_SYSCALL_64_after_hwframe+0x44/0xae
[    5.430677] RIP: 0033:0x7f0aa9512c3e
[    5.430679] Code: 48 8b 0d 5d b1 0e 00 f7 d8 64 89 01 48 83 c8 ff c3 66 2e 0f 1f 84 00 00 00 00 00 90 f3 0f 1e fa 49 89 ca b8 af 00 00 00 0f 05 <48> 3d 01 f0 ff ff 73 01 c3 48 8b 0d 2a b1 0e 00 f7 d8 64 89 01 48
[    5.430680] RSP: 002b:00007fff39f3cc58 EFLAGS: 00000246 ORIG_RAX: 00000000000000af
[    5.430681] RAX: ffffffffffffffda RBX: 000055916224ebd0 RCX: 00007f0aa9512c3e
[    5.430682] RDX: 000055916224ef30 RSI: 00000000008f1db0 RDI: 00007f0aa7a91010
[    5.430682] RBP: 00007f0aa7a91010 R08: 000055916224eae0 R09: 0000000000000000
[    5.430683] R10: 0000000000000005 R11: 0000000000000246 R12: 000055916224ef30
[    5.430684] R13: 000055916224ed00 R14: 000055916224ebd0 R15: 000055916224ef60
[    5.430685]  </TASK>
[    5.430685] Modules linked in: pcc_cpufreq(-) nvidia(OE+) acpi_cpufreq(-) bnep bridge stp llc btusb btrtl btbcm btintel uvcvideo btmtk videobuf2_vmalloc bluetooth videobuf2_memops videobuf2_v4l2 videobuf2_common ecdh_generic videodev mc snd_sof_pci_intel_tgl snd_sof_intel_hda_common soundwire_intel soundwire_generic_allocation soundwire_cadence snd_hda_codec_realtek snd_sof_intel_hda snd_hda_codec_generic snd_sof_pci snd_sof_xtensa_dsp snd_sof snd_sof_utils snd_soc_hdac_hda iwlmvm snd_hda_ext_core snd_soc_acpi_intel_match snd_soc_acpi joydev intel_tcc_cooling soundwire_bus mousedev ledtrig_audio mac80211 x86_pkg_temp_thermal intel_powerclamp snd_soc_core coretemp snd_compress ac97_bus kvm_intel libarc4 hid_multitouch snd_hda_codec_hdmi 8250_dw spi_nor mei_pxp snd_pcm_dmaengine mei_hdcp ee1004 mtd i915 iTCO_wdt snd_hda_intel kvm intel_pmc_bxt snd_intel_dspcfg iTCO_vendor_support intel_rapl_msr iwlwifi irqbypass snd_intel_sdw_acpi snd_hda_codec crct10dif_pclmul crc32_pclmul
[    5.430709]  ghash_clmulni_intel snd_hda_core iwlmei vfat aesni_intel processor_thermal_device_pci_legacy processor_thermal_device pmt_telemetry snd_hwdep crypto_simd pmt_class cryptd fat intel_cstate r8169 drm_buddy cfg80211 intel_uncore snd_pcm processor_thermal_rfim realtek psmouse ttm processor_thermal_mbox mei_me snd_timer rfkill pcspkr i2c_i801 mdio_devres processor_thermal_rapl intel_lpss_pci spi_intel_pci intel_rapl_common snd libphy intel_lpss drm_dp_helper spi_intel i2c_smbus soundcore int340x_thermal_zone thunderbolt mei i2c_hid_acpi idma64 intel_gtt intel_vsec intel_soc_dts_iosf i2c_hid intel_hid video intel_scu_pltdrv sparse_keymap system76_acpi mac_hid coreboot_table dm_multipath dm_mod ipmi_devintf ipmi_msghandler crypto_user acpi_call(OE) fuse bpf_preload ip_tables x_tables ext4 crc32c_generic crc16 mbcache jbd2 serio_raw atkbd uas libps2 usb_storage usbhid vivaldi_fmap nvme xhci_pci nvme_core crc32c_intel i8042 xhci_pci_renesas serio
[    5.430736] ---[ end trace 0000000000000000 ]---
```

当然上面的错误信息是[网上找的](https://github.com/NVIDIA/open-gpu-kernel-modules/issues/256)，不过具体的表现只能说是大差不差，这个错误的具体反映就是提示`Failed to start Load Kernel Module`之后如果你查看`systemctl status systemd-modules-load.service `就会发现报错是`Main process exited, code=killed, status=11/SEGV`其报错的代号是`11/SEGV`表示内存错误

与此同时tty2是可以正常切换的，伴随着控制台会出现乱七八糟的一大堆`audit`审计错误

解决方式也十分简单，但是对我来说也是花了一个早上加一个下午的时间，总之只需要在grub界面按下`e`然后在类似于`linux /boot/vmlinuz-linux root=UUID=0a3407de-014b-458b-b5c1-848e92a327a3 rw `这一行的末尾加上`ibt=off`接着`ctrl+x`启动即可避免本次启动错误

如果希望永久设置，则可以进入`/etc/default/grub`在`GRUB_CMDLINE_LINUX_DEFAULT=""`内加上`ibt=off`，接着退出后`update-grub`即可，内核的参数设置可以[详见](https://wiki.archlinux.org/title/Kernel_parameters)
