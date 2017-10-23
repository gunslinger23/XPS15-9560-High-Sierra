# XPS15-9560-High-Sierra
## 本机配置
- CPU：Intel I7 7700HQ
- 内存：原装16G 2400MHz DDR4
- 硬盘：三星PM961 NVMe 512G(磨人的小妖精)
- 网卡：DW1830
### 配置提示
原装配的killer网卡是无解的！请用usb网卡或者直接换一个吧qwq

## 使用10.13优势
- 苹果终于支持第三方NVMe SSD(原生支持，无需安装任何驱动，对于PM961来说是一件大好事！)
- 采用全新的APFS文件系统(据说是对SSD有神秘加成，HDD最好不要用)

## 使用情况
- 除了触控板无法达到白苹果的体验外，其他基本跟白苹果没啥区别～
- 亮度可以调整保存
### 已知问题
- 无法使用耳机(暂时没弄清楚问题所在)
- 雷电3接口有问题(没有测试过)
- 读卡器无法使用
- 独显无法使用
### 未知问题(没测试)
- HDMI
---
# 安装
## 全新安装
由于我很懒，你们直接参考 [RehabMan](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/) 的教程好了～

教程基本上大同小异，各位请细心参考即可！
#### 注意
- SSD用户最好先把分区转换为APFS(貌似安装时也会转换)
- 进入系统后别急急忙忙登陆你尊贵的AppleID(原因请看下文)

## 从老版本系统上更新
> 如果你想用全新的APFS，建议你还是全新安装好了！(我也是从10.12升级，不知道是不是我的姿势不正确而失败)
#### 依然你还是要尝试就提醒一下你吧
1. 把SSDT补丁、kext和config.plist放到原来的Clover(最好是最新版，旧版不支持10.13)里面即可
 **注意**
 > SMBIOS机型更改为MacBookPro14,3(配置与XPS15 9560更接近，支持KabyLake) 如果你想用自己的config.plist，请注意修改
2. 直接开始你的更新旅程！(遇到坑我也帮不了你QwQ，找大神求助吧)

# kext问题
RehabMan大神推荐将部分注入的kext放入到/S/L/E (或者 /L/E 在 10.11)
周到的我已经把全部能放进/S/L/E的kext全部放好在kext-install文件夹内
### 操作
1. 把S/L/E文件夹里面的全部kext放到/S/L/E中(注意权限问题)
2. 先重启机子以防出问题再接着第三步
3. 打开EFI/clover/kext
  - 1.保留`BrcmFirmwareData.kext` `BrcmPatchRAM2.kext`(2个驱动放在SLE里面会出问题，放在Clover注入才没问题)
  - 2.删掉其余所有kext
  
# 登陆你的AppleID(不用白果三码)
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

# 尾巴
这破系统已经浪费里我许多时间，但是换回来的使用体验是值得的

我只是看国内没人弄才搞里这东西

我遇到的坑都在这里都告诉大家了

希望能对许多正在等待升级10.13的小伙伴有帮助

欢迎各位小伙伴们来帮我完善～

---
# 特别感谢
- [@RehabMan](https://github.com/RehabMan)、[tgmac](https://github.com/RehabMan)提供的有关文件
- [blazinsmokey](https://www.tonymacx86.com/members/blazinsmokey.1188623/)解决了wifi睡眠后很慢的问题
