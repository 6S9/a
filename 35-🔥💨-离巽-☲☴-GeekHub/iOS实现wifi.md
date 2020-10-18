### iOS实现wifi传书功能
https://www.jianshu.com/p/e8b4ae2396cf

CocoaHTTPServer
![](https://upload-images.jianshu.io/upload_images/3094887-e747360de5f213e3.jpg)

### iphone微信聊天记录导出查看方法
https://jingyan.baidu.com/article/4b52d702d60277fc5c774b1a.html

楼月微信聊天记录导出恢复助手

### iOS底层基础知识-文件目录结构
https://www.cnblogs.com/wujy/archive/2016/02/13/5188302.html

一：iOS沙盒知识

出于安全考虑，iOS系统把每个应用以及数据都放到一个沙盒（sandbox）里面，应用只能访问自己沙盒目录里面的文件、网络资源等（也有例外，比如系统通讯录、照相机、照片等能在用户授权的情况下被第三方应用访问
![](https://images2015.cnblogs.com/blog/80291/201602/80291-20160213212622903-985718705.png)

二：iPhone 手机文件目录介绍：

/private/var/ mobile /Media/iTunes_Control/Music】
iTunes上传的多媒体文件（例如MP3、MP4等）存放目录，文件没有被修改，但是文件名字被修改了，直接下载到电脑即可读取。

三：iOS系统目录

1：/Applications/目录存放系统App和从Cydia下载的App，而 /var/mobile/Containers/ 目录存放的则是StoreApp

6：/System/Library: iOS文件系统中最重要的目录之一，存放大量系统组件，其目录结构如下图所示。
![](https://images2015.cnblogs.com/blog/80291/201602/80291-20160213214533419-414534424.jpg)

/System/Library/CoreServices里的SpringBoard.app：iOS中桌面管理器（类似于Windows里的explore），是用户与系统交流的最重要中介。
