# lenovo-小新I2000-hackintosh
## 联想Lenovo小新I2000黑苹果首发体验之旅（基本完美）

#### 写在前面：

**文末有EFI文件可直接拿来使用**

**经过多次版本迭代，EFI文件已趋于完善，请以文末最新版为准！**

<!--more-->

> EFI更新内容：
>
> 修复开机时屏幕上会显示几行代码的问题。
>
> 将编辑器里红色感叹号里的内容修复。

首先，感谢国光的黑苹果安装教程，采用了OpenCore的引导安装方式（如果对EFI文件制作感兴趣，请移步至教程https://apple.sqlsec.com）。
其次，这个EFI引导文件只适用于联想小新i2000，已经验证能够在机器上稳定运行。最后，在制作黑苹果U盘引导镜像时最好使用Monterey版本(只要大版本号是12即可），系统可以在大版本号内进行更新，不用更改EFI文件，但是在跨大版本更新或者降级时，需要对EFI文件进行包括但不限于网卡、蓝牙等驱动的更新，祝有需要的朋友使用愉快。



请注意对比自己的机型，如果不同请谨慎使用

**联想（Lenovo）小新出色版I2000 14英寸超薄本电脑（i7-5500U 4G 8G SSHD 500G HD5500核显 Win8.1）**

笔记本cpu：Broadwell

声卡：ALC235

其余驱动按照教程即可

![联想Lenovo小新I2000黑苹果首发体验之旅01](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8501.png)

<center>联想（Lenovo)小新出色版I2000 示例图片</center>



**未正常运行的模块：**

> 共享模块中可以进行共享网络创建，但是搜不到共享热点。

**能够正常运行的模块：**

> 音频驱动能正常工作（除却基本补丁外，需额外再打一个热补丁）
>
> 蓝牙功能正常
>
> Wi-Fi功能正常
>
> 以太网卡正常
>
> USB正常使用
>
> 能正常识别SATA硬盘、储存正常
>
> 屏幕可正常调节亮度（如果发现屏幕亮度无法调节，请先在设置中对显示器颜色进行校准）
>
> 笔记本键盘、触控板正常
>
> 外接键盘、鼠标正常
>
> 摄像头功能正常
>
> 内存正常
>
> 集显正常
>
> 电池显示正常
>
> 共享模块正常
>
> \``````

按照教程（https://apple.sqlsec.com）
的流程走完，到实际安装黑苹果时遇到了两次卡**[EB|#LOG:EXITBS:START]**，是卡在第一步的白苹果logo，第二次卡在安装MacOS的前一步加载硬盘（界面是MacOS恢复，寻找宗卷），解决办法见下图（以下安装过程的界面图片引自教程）：

进入Bios将你制作的U盘镜像设置为开机启动（因为后面安装过程中电脑会多次重启，每次都要通过U盘引导进苹果系统，建议将U盘设置为第一顺位启动）。

![联想Lenovo小新I2000黑苹果首发体验之旅02](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8502.jpg)

<center>点击BigSur安装（最新版为Monterey)</center>

第一遍进度条：你的EFI文件大概率会是不完美的。

![联想Lenovo小新I2000黑苹果首发体验之旅03](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8503.jpg)

在这会卡第一次**[EB|#LOG:EXITBS:START]，**此时你也可以开启啰嗦模式，安装过程中不再全程GUI界面，屏幕上间歇会疯狂跑代码，同时可以清晰看到具体卡在哪一位置，报什么错。

![联想Lenovo小新I2000黑苹果首发体验之旅04](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8504.png)

将boot－ａｒｇｓ那一项的值改为－ｖ，即可开启啰嗦模式。

用OCAuxiliaryTools这个软件去修改EFI>OC文件下的config.plist文件。

![联想Lenovo小新I2000黑苹果首发体验之旅05](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8505.png)

上图打红叉的那一项不要勾选，这一项意思是在引导中设置默认引导项，字面意思似乎是和开机引导有关。不过不用担心，即使你是在一块硬盘上安装双系统，也可以用下图这个软件设置开机引导界面来切换Windows和ｍac系统。

![联想Lenovo小新I2000黑苹果首发体验之旅06](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8506.png)

在这一步之前是寻找宗卷，大概率还是会卡一次。

![联想Lenovo小新I2000黑苹果首发体验之旅07](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8507.jpg)

<center>最新版为Monterey</center>

解决办法，按照下图勾选，去掉多余的勾选项。

![联想Lenovo小新I2000黑苹果首发体验之旅08](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8508.png)

然后就可以进行下一步了，将你划分出的空闲硬盘抹除成苹果的格式，退出磁盘工具，下面安装就会顺利进行。

![联想Lenovo小新I2000黑苹果首发体验之旅09](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8509.jpg)

![联想Lenovo小新I2000黑苹果首发体验之旅10](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8510.jpg)

![联想Lenovo小新I2000黑苹果首发体验之旅11](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8511.jpg)

![联想Lenovo小新I2000黑苹果首发体验之旅12](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8512.jpg)

<center>最新版为Monterey</center>


![联想Lenovo小新I2000黑苹果首发体验之旅13](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8513.jpg)

<center>最新版为Monterey</center>


![联想Lenovo小新I2000黑苹果首发体验之旅14](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8514.jpg)

<center>最新版为Monterey</center>


![联想Lenovo小新I2000黑苹果首发体验之旅15](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8515.jpg)

<center>最新版为Monterey</center>


![联想Lenovo小新I2000黑苹果首发体验之旅16](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8516.jpg)

![联想Lenovo小新I2000黑苹果首发体验之旅17](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8517.jpg)

![联想Lenovo小新I2000黑苹果首发体验之旅18](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8518.png)

至此，勇敢的少年恭喜你，你的黑苹果已经初步安装成功了，后面跟着系统一步步设置就可以了。

本次EFI引导文件制作是在Windows系统下制作，涉及到的软件和文件都可以在这个https://apple.sqlsec.com 教程中找到，所以不用担心（如果你有一台Mac，那制作EFI引导文件会有更方便的方法。哈？我都有苹果系统了，还装什么黑苹果·······）。

以上就是本次LenovoXiaoxin I2000的黑苹果安装过程，如果你恰巧也是LenovoXiaoxin I2000的使用者，喜欢尝鲜的你，在对Windows审美疲劳时，可以去体验苹果系统。PS冷门机型的EFI引导文件实在太难找了······生活处处是围城。

另附上我的EFI引导文件链接，喜欢偷懒的你可以直接拿去使用，比心。

**最新版：** https://cloud.189.cn/web/share?code=FfuYjy6j6ZJz（访问码：6ke7）



#### 「关于单硬盘安装双系统的一些后话」

第一种方法：Windows启动文件和黑苹果的EFI文件可以放在不同的盘里。Windows默认的ESP大小100Mb，苹果ESP需要200Mb以上（不然在安装苹果系统格式化系统盘时会报错）。单硬盘装好Windows系统后，可以单独划分出一块200Mb大小的空间（命名不要与Windows系统的ESP盘重名），把它格式化成FAT32格式，将制作好的EFI引导文件放入其中，然后再划分一块空间装黑苹果系统，最后用DiskGenius把黑苹果引导添加至开机启动项即可实现开机时双系统选择启动。

> **磁盘划分**
>
> 通过`DiskGenius`的WinPE版，对整个磁盘进行重新划分，建立300MB大小的ESP/MSR分区。
>
> ![联想Lenovo小新I2000黑苹果首发体验之旅19](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8519.png)
>
> ![联想Lenovo小新I2000黑苹果首发体验之旅20](https://cdn.jsdelivr.net/gh/xinzoro/tu_chuang_1/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8520.png)

第二种方法：将Windows启动文件和黑苹果的EFI文件放在同一个ESP里。需要事先划分出300Mb以上的空间，装完Windows系统后再安装黑苹果系统。将黑苹果的EFI引导文件中整个OC文件夹拷贝至ESP文件夹里的EFI文件夹内，然后用DiskGenius把黑苹果引导添加至开机启动项即可实现开机时双系统选择启动。

> ![联想Lenovo小新I2000黑苹果首发体验之旅21](https://cdn.jsdelivr.net/gh/runofftheearth/tu_chuang_2/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8521.png)
>
> ![联想Lenovo小新I2000黑苹果首发体验之旅22](https://cdn.jsdelivr.net/gh/runofftheearth/tu_chuang_2/%E8%81%94%E6%83%B3Lenovo%E5%B0%8F%E6%96%B0I2000%E9%BB%91%E8%8B%B9%E6%9E%9C%E9%A6%96%E5%8F%91%E4%BD%93%E9%AA%8C%E4%B9%8B%E6%97%8522.png)

