title: Android 8.0 Oreo 新特性及 API 简介
date: 2017-08-23 11:00:00
tags: [Android]
categories: Android
---

> 经过4个DeveloperPreview 版本之后，google 在8月22日正式面向全球发布了Android 8.0 版本，取名『Oreo』。Android 8.0 为用户带来了诸如画中画 (Picture in picture)、自动填充 (Autofill)、免安装应用 (Instant Apps)、Google Play 保护机制 (Google Play Protect) 以及更快的启动时间等诸多新功能。到今年年底，国内一些硬件厂商都会计划新设备升级至Android8.0 Oreo。

## Android 8.0 Oreo 的新特性

### 画中画 (Picture-in-picture)

PIP 功能让用户能够以任意窗口大小同时进行两项任务的操作。该功能需要APP适配多窗口分屏模式（Multi-window）。
![](http://ov4i8xc7p.bkt.clouddn.com/17-8-23/46128014.gif)

### 通知 Notification

**[通知channel]** ：Android 8.0 引入了通知渠道（Channel）的新特性，将应用通知分门别类管理，用户可以针对不同的通知消息单独设置通知优先级和提醒方式。

<img src="http://ov4i8xc7p.bkt.clouddn.com/17-8-23/69524188.jpg" width=400 algh/>
> Google 应用的通知设置

<img src="http://ov4i8xc7p.bkt.clouddn.com/17-8-23/83461351.jpg" width=400 />
> Google 地图的通知设置

**通知角标（Notification dot）**：
之前的原生版本 Android 版本中，桌面启动器是不支持通知角标的（国内厂商有定制化支持），只能通过一些第三方桌面启动器（如Nova Launcher）实现。Android 8.0 开始，应用可以在启动器图标上显示通知圆点来提示用户，但这个圆点角标和 iOS 上那个有所不同——它仅提示用户该应用有通知，不会显示具体的通知数量。

**延时通知**：Android 8.0 引入了另一种通知处理操作——延时通知。当我们暂时不便处理某条应用通知时，只需要在该条通知上清扫，点击出现的时钟图标，即可让这条通知暂时从通知栏消失，在设定好的时间后再回来。

<img src="http://ov4i8xc7p.bkt.clouddn.com/17-8-23/23031752.jpg" width=400 />
<img src="http://ov4i8xc7p.bkt.clouddn.com/17-8-23/6200.jpg" width=400 />
> 延时通知

### 自动填充框架 (Autofill framework)

Android8.0 提供了系统几全局自动填写框架。简化了用户设置一台新设备以及同步密码的过程。需要用到表格数据的应用可为自动填充框架进行优化，密码管理应用通过新的 API 接口，能够让用户在自己最喜欢的应用中使用密码自动填充服务。

<img src="http://ov4i8xc7p.bkt.clouddn.com/17-8-23/71537178.jpg" width=400/>
> 系统的自动填充设置


### 最大屏幕宽高比

Android 8.0 引入了 `maxAspectRatio` 属性, 可以设置 App 级别的屏幕宽高比。


## 系统优化

### 新的 StrictMode 监控

Android 8.0 (API level 26) 增加了 3 个新的 StrictMode 检查类型:

- detectUnbufferedIo() 检查没有使用buffer读写数据
- detectContentUriWithoutPermission() 检查没有获取相关权限的情况下，调用app之外的Activity
- detectUntaggedSockets() 检查debug时没有使用 setThreadStatsTag(int) 标记网络请求流量

### 缓存数据

Android 8.0（API Level 26）引入了新的应用文件缓存方式。每个APP会分配一个磁盘空间配额（disk space quota）用于缓存，通过`getCacheQuotaBytes(UUID)`获取。

如果系统需要释放磁盘空间，会从最接近分配配额的app开始删除缓存文件。如果app缓存的文件大小在配额之下，如果系统清理空间时，这些文件不会最先被删除。如果系统决定删除应用内缓存文件，会按照时间顺序，先删除最旧的缓存。

系统提供了两个新的API，用于应用控制缓存行为：

- StorageManager.setCacheBehaviorAtomic()： 一个目录和它的内容作为一个原子单元被删除。
- setCacheBehaviorTombstone(File, boolean)：不会删除目录中的文件，但会把文件大小截断为0bytes，作为一个空文件。

如果需要分配一个大文件缓存，推荐使用新的API `allocateBytes(FileDescriptor, long)`，可以在需要时，自动清理其他app的缓存，释放空间。

### 新增权限

- The ANSWER_PHONE_CALLS permission 使 app 可以编程应答电话。
- The READ_PHONE_NUMBERS permission 读取设备的电话号码。

这些权限定义在PHONE权限组中，均被定义为危险权限。

### 系统优化

为了提升系统的性能体验，Android 8.0引入了新的并发压缩垃圾回收机制，代码局部化优化（code locality）等优化手段，加速了启动时间。OS 和 APP 都能获得较好的性能体验。

### Java 语音支持

- java.time from OpenJDK 8.
- java.nio.file and java.lang.invoke from OpenJDK 7.

### 后台限制

Android 8.0 对后台定位和扫描WiFi增加了限制，改变了应用在后台的运行模式。

后台服务限制：处于空闲状态时，应用可以使用的后台服务存在限制。

广播限制：除了有限的例外情况，应用无法为隐式广播注册接收器。

---
[通知channel]:https://developer.android.com/guide/topics/ui/notifiers/notifications.html#ManageChannels


