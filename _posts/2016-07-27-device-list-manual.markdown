---
layout: post
title:  "DeviceList配置注意事项"
date:   2016-07-27 00:00:00
categories: git
---

版本: v1.3  
创建时间: 2016-07-27  
最后更新: 2016-11-21  
 
## IO设备  

### 1 逆向雨棚红灯
  
**OutPort**: 加载IO动态库的延迟时间（秒）。 
 
### 2 正向雨棚红灯
  
**DllName**: IO动态库名称，所有IO设备均使用此动态库。
  
### 3 正向雨棚绿灯  

无特殊说明。 
 
### 4 交通红灯  

无特殊说明。  

### 5 交通绿灯  

无特殊说明。  

### 6 栏杆抬起  

**InPort**: 当使用南昌先锋的智能控制器时，代表串口号。  

### 7 栏杆落下  

**CanFeedBack**: 设置为1时，代表允许用“功能＋栏杆”键禁止自动降杆（即车道流程继续，但栏杆永远打开）  

### 8 雾灯  

无特殊说明。  

### 9 报警器  

无特殊说明。  

### 10 栏杆线圈  

无特殊说明。  

### 11 抓拍线圈  

**UseFlag**: 当车道处于复式收费模式时，该字段不起作用（即在此模式下，车道软件自动禁用抓拍线圈，即使此值为1）。  
**CanFeedBack**: 设置为0时，启用二次抓拍（即出口车道在读卡时再抓拍一次，用于抓拍线圈故障时）  


## 非IO设备  

### 12 IC卡读写器  

无特殊说明。  

### 13 收发卡机  

无特殊说明。  

### 14 票据打印机  

**DeviceType** 和 **Comport**: **当软件采用“计重打印机”的DeviceType和Comport值打印失败时，会用"票据打印机"的DeviceType和Comport再重试一次。**  

### 15 费额显示器  

废弃项目，应配置“**计重费显**”。  

### 16 图像卡  

**InPort**: 设置为1时，则开启证照抓拍功能。  

### 17 字符叠加器  

**DllName**: 当采用南昌先锋的集成字符叠加器的智能控制器时，应与"正向雨棚红灯"的DllName一致；  
**Comport**: 当采用南昌先锋的集成字符叠加器的智能控制器时，应与"栏杆抬起"的InPort一致。  

### 18 语音  

已废弃，**useflag** 应设置为0 。  

### 19 车牌识别设备  

注意：部分车牌识别设备动态库，需要正确配置同名的**ini**文件。   

* 铁岭河05车道等使用的是U创的车牌识别器，需要做如下配置:  
  * 复制 plate_uchuang_ldc200.dll, plate_uchuang_ldc200.ini, wty.dll, wty_config.ini 至 toll 文件夹
  * 配置 plate_uchuang_ldc200.ini 中的“车牌识别器IP地址", 如 192.168.0.109
  * 配置 wty_config.ini 中的本机与车牌识别器连接网卡的IP地址, 如 192.168.0.1

### 20 称重设备  

无特殊说明。  

### 21 计重打印机  

**DeviceType** 和 **Comport**: **当软件采用“计重打印机”的DeviceType和Comport值打印失败时，会用"票据打印机"的DeviceType和Comport再重试一次。**  

### 22 计重费显  

**InPort**: 某些入口车道也用费显（用于交通灯和报警器），此时InPort字段应设置为1 。  

### 23 ETC读写器  

**InPort**: ETC读写器PASM卡槽数，搜林的目前设置为4 。  

### 24 无人发卡机  

**InPort**: 上工位读写器串口号；  
**OutPort**: 下工位读写器串口号。  

### 25 自动卡机线圈  

**bps**: 设置为1时，代表自动卡机线圈与抓拍线圈合用（用于卡机前置于收费亭的情况，此时硬件施工应将卡机线圈同时接到抓拍线圈端子上，目前采用这种接法的有林口01、林口03、柳树03、柴河03、铁岭河05）。  

**注意**：当具备无人值守卡机时，自动卡机线圈车检器利用了"电平模式自动栏杆机"的端子，故此时栏杆机必须采用**脉冲模式**。  

### 26 空  

### 27 卡机语音  

无特殊说明。  

### 28 卡机ETC读写器  

**InPort**: 上工位ETC读写器串口号；  
**InBit**: 下工位ETC读写器串口号；  
**OutPort**: **必须为0**；  
**OutBit**: **必须为0**；   

### 29 车型分类器  

**DeviceType**: 2代表串口设备，其他值代表以太网接口设备；  
**ComPort**: 对于串口设备为串口号，否则忽略；  
**InPort.InBit.OutPort.OutBit**: 对于网络接口设备是IP地址，否则忽略；  
**bps**: 对于串口设备是波特率，对于网络接口设备是端口号。  

* U创车型分类器配置:  
  * dllname: vehtype_uc_g2.dll  
  * 复制 **vehtype_uc_g2.dll** 和 **CarTypeUC** 文件夹至 **toll** 中;  
  * 编辑 **CarTypeUC** 中的 **autovehtypeUC.ini**, 设置正确的设备IP地址, 如设备具有车牌识别功能（可以咨询硬件施工方），则 "G25标记=1", 否则是0； 
* 朗为车型分类器配置:
  * dllname: vehtype_runwell_avc.dll  
  * 复制 vehtype_runwell_avc.dll、HeiAVCConfig.ini、TRP_VPDCommDll.dll、TRP_VPDConfig.ini 四个文件至Toll文件夹;  
  * 编辑 HeiAVCConfig.ini, EnableLPNR = yes, EnableSoftTrigger = no;（可与现场施工人员确认此配置）;  
  * 编辑 TRP_VPDConfig.ini, 将抓拍器IP配置正确（可与现场施工人员确认此IP）;  

