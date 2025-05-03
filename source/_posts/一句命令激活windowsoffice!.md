---
title: 一句命令激活windows/office!
---

服务器地址：[http://kms.03k.org](https://link.zhihu.com/?target=http://kms.03k.org)([点击检查是否可用](https://link.zhihu.com/?target=https://03k.org/go/kmscheck.php))；

服务作用：在线激活windows和office

适用对象：VOL版本的windows和office

适用版本：截止到win10和office2016的所有版本

**使用方法：**

一般来说，只要确保的下载的是VL批量版本并且没有手动安装过任何key，你只需要使用管理员权限运行cmd执行一句命令就足够：



```js
slmgr /skms kms.03k.org
```

这句命令的意思是，把kms服务器地址设置（set kms）[为kms.03k.org](https://link.zhihu.com/?target=http://xn--kms-c88d.03k.org/)，设置成功如下：

![img](https://cdn.jsdelivr.net/gh/markruan/cloudimg/picx/v2-d8a336947d6ef894a8aa1dee0fdb3d29_720w.jpeg)

然后一句命令手动激活：

```
slmgr /ato
```

![img](https://cdn.jsdelivr.net/gh/markruan/cloudimg/picx/v2-1e1623924cda1dbcbae37003287965c6_720w.jpeg)

这句命令的意思是，马上对当前设置的key和服务器地址等进行尝试激活操作。kms激活的前提是你的系统是批量授权版本，即VL版，一般企业版都是VL版，专业版有零售和VL版，家庭版旗舰版OEM版等等那就肯定不能默认直接用kms激活。

**一句命令激活office**

首先你的office必须是vol版本，否则无法激活。

找到你的office安装目录，比如C:\Program Files (x86)\Microsoft Office\Office16

64位的就是C:\Program Files\Microsoft Office\Office16

office16是office2016，office15就是2013，office14就是2010.

然后目录对的话，该目录下面应该有个OSPP.VBS。

接下来我们就cd到这个目录下面，例如（请更改为自己的实际安装目录）：

```
cd "C:\Program Files (x86)\Microsoft Office\Office16"
```

如果你不知道你的office装在哪个目录，可以打开一个程序比如word，然后用打开任务管理员右键选择“打开文件所在的位置”。

然后执行注册kms服务器地址：

```
cscript ospp.vbs /sethst:kms.03k.org
```

/sethst参数就是指定kms服务器地址。

一般ospp.vbs可以拖进去cmd窗口，所以也可以这么弄：

```
cscript "C:\Program Files (x86)\Microsoft Office\Office16\OSPP.VBS" /sethst:kms.03k.org
```

一般来说，“一句命令已经完成了”，但一般office不会马上连接kms服务器进行激活，所以我们额外补充一条手动激活命令：

```
cscript ospp.vbs /act
```

如果提示看到successful的字样，那么就是激活成功了，重新打开office就好。

![img](https://cdn.jsdelivr.net/gh/markruan/cloudimg/picx/v2-faad272e9d7552d6709c96d4e9a57d94_720w.webp)

如果遇到报错，请检查：

检测KMS服务器是否挂了点我

KMS OK正常KMS BOOM挂了

还有kms的ip你ping下是不是跟页面的一样

上面还有检测的时间

1、你的系统/office是否是批量VL版本

2、是否以管理员权限运行cmd

3、你的系统/office是否修改过key/未安装gvlk key

4、检查你的网络连接

5、本地的解析不对,或网络问题（点击检查服务器是否能连上）

6、根据出错代码自己搜索出错原因

0x80070005错误一般是你没用管理员权限运行CMD