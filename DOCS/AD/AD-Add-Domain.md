# Windows Server 2016中添加AD域控制器

AD域控制器一台往往都是不够的，一般都是需要两台或者两台以上，这样不至于一台AD域控制器瘫痪，导致整个架构无法运行，AD域是整个架构的核心；在上个文档中已经说了[如何创建一台AD域](./../../DOCS/AD/AD-Deployment.md)，接下来我们看看如何在现有的AD域中添加域控制器。

## 主题：

- [部署环境](#部署环境)
- [先决条件](#先决条件)
- [安装角色](#安装角色)
- [添加域控制器](#添加域控制器)

## 部署环境

| 编号 | 服务器名称 | IP地址 | 操作系统 |
| :---: | :-----: | :------: | :-----|
| 001 | AD1 | 192.168.100.250 | Windows Server 2016 Datacenter Evaluation |
| 002 | AD2 | 192.168.100.251 | Windows Server 2016 Datacenter Evaluation |

## 先决条件

1、已经有一台AD域控制器，[创建AD域](./../../DOCS/AD/AD-Deployment.md)  
2、设置IP地址，DNS指向第一台域控制器，这里就不多讲了，我只附一张图  
![](./../../IMGS/AD/AD-Add-Domain-1.png)
3、设置计算机名
![](./../../IMGS/AD/AD-Add-Domain-2.png)

## 安装角色

在需要添加为域控制器的服务器上打开“服务器管理器”，点击“添加角色和功能”
![](./../../IMGS/AD/AD-Add-Domain-3.png)
弹出“添加角色和功能向导”，点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-4.png)
安装类型选择“基于角色或基于功能的安装”，点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-5.png)
服务器选择“从服务器池中选择服务器”，选中“AD2”，点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-6.png)
服务器角色选择“Active Directory域服务”，会弹出“添加Active Directory域服务所需的功能？”，点击“添加功能”
![](./../../IMGS/AD/AD-Add-Domain-7.png)
选中“Active Directory域服务”后，点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-8.png)
功能这里直接点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-9.png)
点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-10.png)
确认配置这里将“如果需要，自动重新启动目标服务器”打勾，点击“安装”
![](./../../IMGS/AD/AD-Add-Domain-11.png)
AD域服务角色安装完成，点“关闭”，当然也可以点击“将此服务器提升为域控制器”来添加域控制器，这里不这么做
![](./../../IMGS/AD/AD-Add-Domain-12.png)

## 添加域控制器

回到该服务器的“服务器管理器”，点击“通知”-“将此服务器提升为域控制器”
![](./../../IMGS/AD/AD-Add-Domain-13.png)
部署配置如下  
选择部署操作“将域控制器添加到现有域”选中  
指定此操作的域信息  
域：“contoso.com”  
然后点击“更改”
![](./../../IMGS/AD/AD-Add-Domain-14.png)
输入部署操作的凭据，点击“确定”
![](./../../IMGS/AD/AD-Add-Domain-15.png)
部署配置配置完成，点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-16.png)
域控制器选项这里只配置“键入目录服务还原模式密码”，点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-17.png)
DNS选项这里直接点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-18.png)
其他选项，选择复制自的域控，这里为“AD.contoso.com”，点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-19.png)
指定AD DS数据库、日志文件和SYSVOL的位置都放置D盘，点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-20.png)
确认配置，点击“下一步”
![](./../../IMGS/AD/AD-Add-Domain-21.png)
先决条件检查已通过，点击“安装”
![](./../../IMGS/AD/AD-Add-Domain-22.png)
正在配置
![](./../../IMGS/AD/AD-Add-Domain-23.png)
配置完成后会自动重新启动服务器
![](./../../IMGS/AD/AD-Add-Domain-24.png)
服务器重新启动之后，输入密码，这里需要输入域管理员密码
![](./../../IMGS/AD/AD-Add-Domain-25.png)
进入桌面后，在“服务器管理器”中点“工具”-“Active Directory用户和计算机”
![](./../../IMGS/AD/AD-Add-Domain-26.png)
打开“Active Directory用户和计算机”后，展开contoso.com域，点击“Domain Controllers”可以看到AD1和AD2
![](./../../IMGS/AD/AD-Add-Domain-27.png)
到这里添加域控制器就部署完成了