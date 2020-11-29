# EFI

## Hardware List
- CPU: AMD R5 3600
- 主板: 微星B450M MORTAR MAX
- GPU: 讯景RX5700 XT (非公版)

## 系统
- Big Sur 11.0

## 遇到的坑
- [安装过程中30后鼠标卡住](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/extended/userspace-issues.html#frozen-in-the-macos-installer-after-30-seconds)
- [iCloud 服务“无法联系服务器”](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#fixing-rom)

## 登录 iCloud 遇到【无法联系服务器】的解决办法:Fixing En0
**1. 一般情况我们的 `En0` 是这样的，`build-in/内建` 下方没有打勾，说明不是内建（这里以我的博通无线网卡为例)**
[![DsiAHS.jpg](https://s3.ax1x.com/2020/11/27/DsiAHS.jpg)](https://imgchr.com/i/DsiAHS)

**2. 按照[教程](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#fixing-en0)**
  - Hackintool >> PCIe >> 导出（文件导出到桌面)
  - 用 `Propertree`打开桌面的 `pcidevices.plist`
  - 在里面找到你的网卡，如果是只是无线网卡根据设备名找 `Network Controller`，如果是以太网的找 `Ethernet Controller`
  (比如我这里是博通无线网卡)
  
  
[![DsFyLV.md.jpg](https://s3.ax1x.com/2020/11/27/DsFyLV.md.jpg)](https://imgchr.com/i/DsFyLV)
  
**3. 复制Controller 的 Key 值， 例如（PciRoot(0x0)/******)**
[![DsFHeK.md.jpg](https://s3.ax1x.com/2020/11/27/DsFHeK.md.jpg)](https://imgchr.com/i/DsFHeK)


**4. 打开 EFI>OC 中的 config.list,  在 DeviceProperties -> Add 新建一个👆 Controller Key 值的 Dictionary, 如下图添加一个键值对:**` built-in` , `01`


[![Dsk1kF.png](https://s3.ax1x.com/2020/11/27/Dsk1kF.png)](https://imgchr.com/i/Dsk1kF)


**5. Save**  

**6. 替换EFI**  

**7. Reboot**  

**8. 检查是否生效**  
[![DsABD0.md.jpg](https://s3.ax1x.com/2020/11/27/DsABD0.md.jpg)](https://imgchr.com/i/DsABD0)


**9. icloud 正常工作**  
[![DsA65F.jpg](https://s3.ax1x.com/2020/11/27/DsA65F.jpg)](https://imgchr.com/i/DsA65F)
