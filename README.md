# 《Windows 内核安全编程技术实践》

<div align=center>
<img width="150" src="https://user-images.githubusercontent.com/52789403/201465673-01dd7d47-7092-4523-b828-8af16030b979.png" />
</div>

<br><br>

**本书作者：** 王瑞 (LyShark)<br>
**作者邮箱：** me@lyshark.com<br>
**作者博客：** https://lyshark.cnblogs.com<br>

******************************************

## 前言

**关于作者**

野路子出道，自幼热爱计算机技术，尤其喜爱二进制安全方向，并长期致力于信息安全技术研究，自学钻研计算机技术十余年，期间没有任何人给予过任何帮助，遇到问题只能自己想办法，人最困难的时候并不是在学校求学的时光，而是在出现问题时，回头却发现身后空无一人，LyShark知道初学者的困境，并能够感同身受，发布本书只是为了无私帮助更多人，所谓前人栽树后人乘凉，知识需要积累与总结，希望你也能够将所学所想，继续传递下去。

**书籍内容简介**

这是一本`Windows 10 x64`内核安全开发系列丛书，暂且就叫它`《Windows 内核安全编程技术实践》`吧，本书是`LyShark`多年的技术积累编写而成，不同于市面上的多数内核开发系列丛书，本书是以`底层安全`角度为切入点忽略了驱动开发中项目实践部分，`LyShark`发现多数丛书都会携带太多的技术概念，这些概念并不利于技术实践，本书将忽略太多没有意义的专业术语，所有文章均以`实战`角度出发，由简入深`递进`式教学，通过学习本书你可掌握`反内核`工具是如何实现的，这些`技术细节`相信市面上你绝对学不到，或者找到的都是过时的，`LyShark`追求`高质量`文章，保证每一篇文章都是可被直接应用。

**书籍撰写初衷**

某一天，笔者想要实现一款`ARK反内核`工具，在找资料时发现市面上多数ARK工具都经过了`VMP`高强度`加密`，内核代码`尤为宝贵`这一点可以被`理解`，多数有源码的项目也都是`过时的`无法正常使用，故想要将ARK反内核工具功能在最新版本的`Windows 10 x64`系统上面实现，既可以`整理归纳`自己的知识体系，也可以`帮助更多`底层爱好者`学习`内核开发技术，让更多安全爱好者从中受益。

**警告** 

本书内容首发于`博客园`，根据`《中华人民共和国著作权法》`相关规定本人享有`著作权`，本书的发放`仅用于`技术交流学习，本书内容均为`免费`开放，禁止第三方倒卖，如果您在第三方购买到本书请与作者联系，作者`(LyShark)`将追究倒卖者法律责任，纯净的技术交流需要你我共同来维护，感谢您阅读并支持作者的创作。

******************************************

## 书籍目录

 - 第一章：环境配置篇
   - 1.1 WDK8.1 驱动开发环境配置
   - 1.2 WinDBG 配置内核双机调试
   - 1.3 内核测试模式过DSE签名

 - 第二章：基础知识篇
   - 2.1 内核中的链表与结构体
   - 2.2 内核中的自旋锁结构
   - 2.3 内核字符串转换方法
   - 2.4 内核字符串拷贝与比较

 - 第三章：驱动通信篇
   - 3.1 驱动与应用的简单通信
   - 3.2 应用DeviceIoContro开发模板
   - 3.3 通过SystemBuf与内核层通信
   - 3.4 通过ReadFile与内核层通信
   - 3.5 通过PIPE管道与内核层通信
   - 3.6 通过Async反向与内核通信

 - 第四章：驱动读写篇
   - 4.1 内核CR3切换读写内存
   - 4.2 内核MDL读写进程内存
   - 4.3 通过内存拷贝读写内存
   - 4.4 内核R3与R0内存映射拷贝

 - 第五章：内核SSDT解析篇
   - 5.1 内核枚举SSDT表基址
   - 5.2 枚举ShadowSSDT表基址

 - 第六章：内核进程线程篇
   - 6.1 内核中枚举进线程与模块
   - 6.2 监控进程与线程对象操作
   - 6.3 内核监控进程与线程创建
   - 6.4 内核DKOM实现进程隐藏
   - 6.5 内核中实现Dump进程转储
   - 6.6 内核遍历进程VAD结构体
   - 6.7 运用VAD隐藏R3内存思路
   - 6.8 内核摘链DKOM进程隐藏
   - 6.9 内核无痕隐藏自身分析
   - 6.10 内核强制结束进程运行

 - 第七章：内核模块篇
   - 7.1 内核判断驱动加载状态
   - 7.2 内核取ntoskrnl模块基地址
   - 7.3 内核取应用层模块基地址
   - 7.4 内核通过PEB得到进程参数
   - 7.5 断链隐藏驱动程序自身
   - 7.6 内核特征码搜索函数封装
   - 7.7 内核LDE64引擎计算汇编长度
   - 7.8 内核层InlineHook挂钩函数

 - 第八章：内核枚举篇
   - 8.1 内核枚举IoTimer定时器
   - 8.2 内核枚举DpcTimer定时器
   - 8.3 内核枚举PspCidTable句柄表
   - 8.4 内核枚举Minifilter微过滤驱动
   - 8.5 内核特征码扫描PE代码段
   - 8.6 内核枚举LoadImage映像回调
   - 8.7 内核枚举Registry注册表回调
   - 8.8 内核枚举进程与线程ObCall回调

 - 第九章：内核监控篇
   - 9.1 内核监控进程与线程回调
   - 9.2 内核注册并监控对象回调
   - 9.3 内核监视LoadImage映像回调
   - 9.4 内核运用LoadImage屏蔽驱动
   - 9.5 内核监控Register注册表回调
   - 9.6 内核监控FileObject文件回调

 - 第十章：其他篇
   - 10.1 内核封装WSK网络通信接口
   - 10.2 内核封装TDI网络通信接口
