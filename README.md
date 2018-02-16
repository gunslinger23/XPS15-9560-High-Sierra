本项目以同步到码云，方便访问github速度慢的朋友们
[https://gitee.com/gunslinger/XPS15-9560-High-Sierra](https://gitee.com/gunslinger/XPS15-9560-High-Sierra)

# 提示

- 可直接更新到10.13.3
> 本教程的Clover配置文件仅适用于我提供的Clover(v4334)。如果要自行更新Clover请自己折腾！

## 本机配置

- CPU：Intel I7 7700HQ
- 内存：原装16G 2400MHz DDR4
- 硬盘：三星PM961 NVMe 512G
- WIFI网卡：DW1830
- 屏幕分辨率：1080p(提供的Clover已添加支出4k屏kext，无需担心~)

### 关于WIFI网卡问题

原装配的killer网卡是无解的！请用usb网卡或者直接换一个免驱的吧qwq

## 使用情况

- 除了下面问题以外，其他全部都能用！

### 已知问题

- 触摸板设置空白
- 雷电3接口不支持热插拔
- 读卡器无法使用(BIOS禁用可以省电)
- 独显无法使用(由于使用了Nvidia Optimus技术隔壁linux也是无解)
- 触摸板与windows系统下比较还是差一点

## kext更新

请查看commit来了解我更新了哪些kext(更新系统前请保持驱动最新，以免出现不支持)

---

# 第一步：安装

## 全新安装(大概流程)

1. 制作启动U盘和启动-[教程](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/) (系统镜像请自己找，随便找一个懒人包也行。懒人包请把我提供的Clover覆盖懒人包里面的)
2. 安装MacOS
3. 把Clover安装到硬盘EFI中(详细教程自己找)

#### 注意

- 安装在SSD中最好使用APFS，你可以先转换一下(貌似安装时也会转换)。若安装在HDD中请不要使用(非常非常慢)
- 进入系统后别急急忙忙登陆你尊贵的AppleID(请看第3步)

接下来看第二步

## 从老版本系统上更新(未测试)

> 不想折腾的话，我建议你还是全新安装好了！(我也是想从10.12升级，可能是我的姿势不正确而失败)

#### 依然你还是要折腾就提醒一下你吧

1. 把SSDT补丁、kext和config.plist可继续沿用
2. [Clover](http://sourceforge.net/projects/cloverefiboot/)注意更新到最新版
3. APFS需要UEFI驱动支持，请把CLOVER/drivers64UEFI/apfs.efi添加到你的Clover中

 > 提供的config.plist中SMBIOS机型更改为MacBookPro14,3(配置与XPS15 9560更接近，支持KabyLake)，修改SMBIOS有风险

# 第二步：安装kext

> RehabMan建议将部分注入的kext放入到/S/L/E中，已获得更接近白苹果的启动方式。

## 以下方法二选一

### 1.安装kext到Clover

1. 把`Post-install/SLE-Kexts`文件夹里面的全部kext复制到`EFI/clover/kexts/Other`中

> 由于kext并非安装到SLE中，请删掉`LiluFriend.kext`

2. 打开`EFI/clover/kexts/Other`
  - 把`Post-install/CLOVER-Kexts`文件夹里的全部kext复制进去(这些kext放在SLE会无法启动)

### 2.安装kext到SLE(推荐)

> 强烈推荐使用`Kext Utility`以免去各种麻烦

1. 打开`Kext Utility`把`Post-install/SLE-Kexts`文件夹里面的全部kext扔进软件里等待完成
2. 先重启机子以防出问题再接着第三步
3. 打开`EFI/clover/kexts/Other`
  - 1.保留`CoreDisplayFixup.kext`(非4K屏用户删掉)
  - 2.删掉其余所有kext
  - 3.把`Post-install/CLOVER-Kexts`文件夹里的全部kext复制进去(这些kext放在SLE会无法启动)

# 第三步：登陆你的AppleID(不用白果三码)

使用白果三码注意机子型号要匹配！否则我也不知道官方会对你的账号做什么 =w=

> 请保证目前你的电脑没有登陆过AppleID，关于如何重设AppleID请看[这里](https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/)

### 开始你的操作

工具：`Clover Configurator`
1. 打开config.plist
2. SMBIOS栏 在Serial Number隔壁有个Generate New小按钮，按下去随机生成Serial Number(不断按到你乐意停下来为止)
3. Systeam Parameters栏 Custom UUID下也有一个Generate New小按钮，重复
4. Rt Variables栏 ROM下面也有一个Generate New小按钮，重复
5. 保存重启(废话)

# 第四步：解决二合一耳机接口

1. 解压`Post-install/ComboJack Installer.zip` (感谢[KNNSpeed](https://www.tonymacx86.com/threads/guide-dell-xps-15-9560-4k-touch-1tb-ssd-32gb-ram-100-adobergb.224486/page-9#post-1539760)提供的补丁)
2. 使用终端cd到ComboJack Installer文件夹
3. 执行命令`./install.sh`(提示需要输入密码)
4. 重启

### 使用提示

- 插入耳机后弹出提示窗口(根据提示选择你插入的设备类型即可)
- 睡眠唤醒后请把耳机拔出再插进去重新选择类型使其正常工作
- 虽然耳机能用了，不要对耳机音质抱有任何希望！买个DAC才是正解！

# 系统小版本更新

1. 更新前请删掉你的`EFI/clover/kexts/Other`中所有kext(注意备份)，然后把我提供的`CLOVER/kexts/Other`里的kext复制进去，在更新完毕后即可还原回去。
2. 请使用`Kext Utility`修复权限并建立缓存(针对kext安装在SLE)

> 可用命令`sudo kextcache -i /`替代

### 注意

> kext安装在SLE或Clover里都必须要这样做，防止启动时驱动引发错误而造成的更新文件损坏

# 尾巴

这破系统已经浪费里我许多时间，但是换回来的使用体验是值得的

我遇到的坑都在这里都告诉大家了

希望能对许多正在等待升级10.13的小伙伴有帮助

小版本更新可能因为kext问题而导致启动不了，我会尽力更新一下kext

欢迎各位小伙伴们来帮我完善～

---
# 特别感谢
- [@RehabMan](https://github.com/RehabMan)、[tgmac](https://www.tonymacx86.com/members/tgmac.928166/)提供的教程和有关文件
- [blazinsmokey](https://www.tonymacx86.com/members/blazinsmokey.1188623/)解决了wifi睡眠后无法使用的问题
