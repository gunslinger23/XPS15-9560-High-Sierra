# 前言
## 本机配置
- CPU：Intel I7 7700HQ
- 内存：原装16G 2400MHz DDR4
- 硬盘：三星PM961 NVMe 512G(磨人的小妖精)
- WIFI网卡：DW1830
- 屏幕分辨率：1080p(提供的Clover已添加支出4k屏kext，无需担心~)

### 关于WIFI网卡问题
原装配的killer网卡是无解的！请用usb网卡或者直接换一个免驱的吧qwq

## 使用10.13优势
- 苹果终于支持第三方NVMe SSD(原生支持，无需安装任何驱动，对于PM961来说是一件大好事！)
- 采用全新的APFS文件系统(对SSD有神秘加成，HDD最好不要用)

## 使用情况
- 除了下面问题以外，其他全部都能用！

### 已知问题
- 雷电3接口不支持热插拔
- 读卡器无法使用(BIOS禁用可以省电)
- 独显无法使用
- 触摸板与windows系统下比较还是差一点
- 插入耳机后在未完全进入睡眠时唤醒会出现无无声(貌似是个bug)

### 未知问题(没测试)
- HDMI

## kext更新
请查看commit来了解我更新了哪些kext

---

# 第一步：安装

## 全新安装(大概流程)
1. [制作启动U盘和启动教程](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/)
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
 **注意**
 > 提供的config.plist中SMBIOS机型更改为MacBookPro14,3(配置与XPS15 9560更接近，支持KabyLake)，修改SMBIOS有风险

# 第二步：安装kext
> RehabMan建议将部分注入的kext放入到/S/L/E中，已获得更接近白苹果的启动方式。
## 以下方法二选一
### 1.安装kext到Clover
1. 把Post-install/SLE-Kexts文件夹里面的全部kext复制到EFI/clover/kext/Other中
> 由于kext并非安装到SLE中，请删掉`LiluFriend.kext`

### 2.安装kext到SLE(推荐)
1. 把Post-install/SLE-Kexts文件夹里面的全部kext复制到/S/L/E中
2. 请使用`Kext Utility`修复权限并建立缓存
3. 先重启机子以防出问题再接着第四步
4. 打开EFI/clover/kext/Other
  - 1.保留`CoreDisplayFixup.kext`(仅针对4K屏用户)
  - 2.删掉其余所有kext
  - 3.把Post-install/CLOVER-Kexts文件夹里的全部kext复制进去(这些kext放在SLE会无法启动)
  
# 第三步：登陆你的AppleID(不用白果三码)
使用白果三码注意机子型号要匹配！否则我也不知道官方会对你的账号做什么 =w=
### 注意
请保证目前你的电脑没有登陆过AppleID
### 开始你的操作
工具：`Clover Configurator V4.53`
1. 打开config.plist
2. SMBIOS栏 在Serial Number隔壁有个Generate New小按钮，按下去随机生成Serial Number(不断按到你乐意停下来为止)
3. Systeam Parameters栏 Custom UUID下也有一个Generate New小按钮，重复
4. Rt Variables栏 ROM下面也有一个Generate New小按钮，重复
5. 保存(废话)

# 第四步：解决二合一耳机接口
1. 解压Post-install/ComboJack Installer.zip (感谢[KNNSpeed](https://www.tonymacx86.com/threads/guide-dell-xps-15-9560-4k-touch-1tb-ssd-32gb-ram-100-adobergb.224486/page-9#post-1539760)提供的补丁)
2. 使用终端cd到ComboJack Installer文件夹
3. 执行命令`./install.sh`(需要输入密码)
4. 重启

### 使用提示
- 插入耳机后弹出提示窗口(根据提示选择你插入的设备类型即可)
- 虽然耳机能用了，不要对耳机音质抱有任何希望！买个DAC才是正解！

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
