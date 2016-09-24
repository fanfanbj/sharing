#Docker存储方式实践分享
# 第一部分 问题诊断


WAS Server标准日志文件startServer.log和native_stderr.log没有更加详细的错误信息。最后功夫不负有心人， 在configuration目录下找到可以定位错误的信息 =_=!：

![image](https://github.com/fanfanbj/sharing/blob/master/Picture2.jpg)

文件访问IO异常，查看相应目录文件的属性：

![image](https://github.com/fanfanbj/sharing/blob/master/Picture3.jpg)

到现在为止，可以初步判断是Docker存储方式(storage drive)在镜像容器分层管理上的问题。
![image](https://github.com/fanfanbj/sharing/blob/master/Picture4.jpg)
为了验证我们的推断，我们做了如下几方面的尝试：
![image](https://github.com/fanfanbj/sharing/blob/master/sharing-layers.jpg)
Docker存储方式提供管理分层镜像和Docker容器自己的可读写层的具体实现。最初Docker仅能在支持AUFS文件系统的ubuntu发行版上运行，但是由于AUFS未能加入Linux内核，为了寻求兼容性、扩展性，Docker在内部通过graphdriver机制这种可扩展的方式来实现对不同文件系统的支持。


