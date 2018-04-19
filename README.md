本项目以同步到码云，方便访问github速度慢的朋友们
[https://gitee.com/gunslinger/XPS15-9560-High-Sierra](https://gitee.com/gunslinger/XPS15-9560-High-Sierra)

# 提示

- 可直接更新到10.13.4 (必须使用新版Clover v4424)
> 本教程的Clover配置文件仅适用于我提供的Clover(v4424)。如果要自行更新Clover请自己折腾！

## 本机配置

- CPU：Intel I7 7700HQ
- 内存：原装16G 2400MHz DDR4
- 硬盘：三星PM961 NVMe 512G
- WIFI网卡：DW1830
- 屏幕分辨率：1080p(提供的Clover已添加支出4k屏kext，无需担心~)

### 关于WIFI网卡问题

原装配的killer网卡是无解的！请用usb网卡或者直接换一个免驱的吧qwq

若使用DW1830，你可以尝试加天线来增强2.4Ghz WIFI的稳定性

## 使用情况

- 除了下面问题以外，其他全部都能用！

### 已知问题

- 雷电3接口不支持热插拔
- 读卡器无法使用(BIOS禁用可以省电)
- 独显无法使用(由于使用了Nvidia Optimus技术隔壁linux也是无解)
- 触摸板与windows系统下比较还是差一点

## kext更新

请查看commit来了解我更新了哪些kext(更新系统前请保持驱动最新，以免出现不支持)

---

# 以下为不完全教程

# 第一步：安装

## 全新安装(大概流程)

1. 制作启动U盘和启动-[教程](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/) (系统镜像请自己找，随便找一个懒人包也行。使用懒人包的请把我提供的Clover覆盖懒人包里面的)
2. 安装MacOS
3. 把Clover安装到硬盘EFI中(详细教程自己找)

#### 注意

- 安装在SSD中最好使用APFS，你可以先转换一下(貌似安装时也会转换)。若安装在HDD中请不要使用(非常非常慢)
- 进入系统后`不要`急急忙忙登陆你尊贵的AppleID(请看第3步)

接下来看第二步

## 从老版本系统上更新

1. 备份好三码(SN码、BSN码、UUID码)
2. 替换成我的Clover
3. 把三码填回去新的Clover配置文件里
4. 更新MacOS

# 第二步：安装kext

> RehabMan建议将部分注入的kext放入到/S/L/E中，已获得更接近白苹果的驱动加载方式

## 以下方法二选一

### 1.安装kext到Clover

1. 把`Post-install/kexts`文件夹里面的全部kext复制到`EFI/clover/kexts/Other`中

> 由于kext并非安装到SLE中，请删掉`LiluFriend.kext`

> 非4K屏用户请删除`CoreDisplayFixup.kext`

### 2.安装kext到SLE(推荐)

> 必须使用`Kext Utility`等kext安装工具来安装，不然出问题了不要找我=w=

1. 把`Post-install/kexts`文件夹里面的全部kext扔进软件里

> 4K屏用户请把`Post-install/4K-kexts`里的kext扔进软件里

# 第三步：登陆你的AppleID(不用白果三码)

警告：不完成该步骤，登录AppleID将会面临封号的风险

使用白果三码注意机子型号要匹配！

> 请保证目前你的电脑没有登陆过AppleID，关于如何重设AppleID请看[这里](https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/)

打开工具：`Clover Configurator`
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

# 第五步：防止蓝牙WIFI异常

1. `系统偏好设置` - `节能` - `电源适配器` - `关闭显示器` 时间调长一点，最好调成`永不`
2. 在`节能`里两个卡片里的电能小憩设置都`关掉`

> 要不然你就等着痛苦吧

## 补救方法

重启 or 睡眠(等电源灯关掉后再按一下启动)

# 选做：解决触控板设置空白

> 注意：某些组合功能键会无法使用

> 教程内容来自[@jardenliu](https://github.com/jardenliu)

### 替换驱动

1. 把`Post-install/touchpad/ApplePS2SmartTouchPad.kext`替换`VoodooPS2Controller.kext`

### 设置手势

1. `系统偏好设置`-`键盘`-`快捷键`-`启动台与程序船坞`,设置`显示启动台`快捷键，设置时，四指下滑。
2. `系统偏好设置`-`键盘`-`快捷键`-`调度中心`,设置`显示通知中心`快捷键，设置时，双指从触摸板右边缘往左滑。

### 手势说明
- 双指左边缘往右滑，最小化当前窗口
- 双指上边缘往下滑，最大化当前窗口 
- 双指右边缘往左滑，显示通知中心
- 三指上下左右滑，分别对应 `调度中心`, `应用程序窗口`, `向右移动一个空间`, `向左移动一个空间`。（偶尔误触）
- 四指上下左右滑，分别对应 `显示桌面`, `显示启动台`, `后退`, `前进`
- （个人使用的手势，可以根据个人喜好自行设置）

# 系统小版本更新(仅针对驱动安装在SLE用户)

1. 更新前请把我提供的`CLOVER/kexts/Other`里的kext复制到`EFI/clover/kexts/Other`中，在更新完毕后即可删掉。
2. 请使用`Kext Utility`修复权限并建立缓存(针对kext安装在SLE)

> 可用命令`sudo kextcache -i /`替代

> 小版本更新可能因为clover或kext问题而导致启动不了，请更新clover和kext

# 尾巴

这破系统已经浪费里我许多时间，但是换回来的使用体验是值得的

我遇到的坑都在这里都告诉大家了

希望能对许多小伙伴有帮助

欢迎各位小伙伴们来帮我完善～

---
# 特别感谢
- [@RehabMan](https://github.com/RehabMan)、[tgmac](https://www.tonymacx86.com/members/tgmac.928166/)提供的教程和有关文件
- [blazinsmokey](https://www.tonymacx86.com/members/blazinsmokey.1188623/)解决了wifi睡眠后无法使用的问题
- [@jardenliu](https://github.com/jardenliu)提供的触摸板魔改版驱动支持多触控手势