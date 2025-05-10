+++
title = "RCE"
icon = "article"
toc = true
+++
# RCE

RCE是什么？

> **RCE**，即**远程代码执行**，是一种严重的安全漏洞。它允许攻击者在目标服务器上远程执行任意代码或操作系统命令，从而可能完全控制受影响的系统。

## eval执行

### 知识

eval函数的语法

```php
eval(string $code): mixed;
```

`$code` 是一个字符串，且必须是有效的 PHP 代码，必须以分号 `;` 结尾，除非代码是一个代码块。

### 题目

![题目.png](https://previewengine.zohopublic.com.cn/image/WD/u4whzafdef893c6b1475a81a20b2790877975?version=1.0&width=2046&height=1536)

![源码.png](https://previewengine.zohopublic.com.cn/image/WD/u4whz384089f4b5dc4e2a8e0f5cafeef934ad?version=1.0&width=2046&height=1536)

### 解题

查看当前目录

![1-1.png](https://previewengine.zohopublic.com.cn/image/WD/u4whzdcdbbbb29d7046cba1f97786fa0c1328?version=1.0&width=2046&height=1536)

没有看到flag，查看上一级的目录

![2-1.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whz1154e39fda694f7fbc0fd56921510e13?orig=true&version=1.0)

发现当中有个falg\_16134，进去

![3-1.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whzb80987b19f86444a9fa79961b3bc3060?orig=true&version=1.0)

## 文件包含

### 题目

![1.png](https://previewengine.zohopublic.com.cn/image/WD/u4whzb24c31a7f2474058a1affb3e235484c1?version=1.0&width=2046&height=1536)

![2.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whz8820c1066a234b219058d9d04c5746ba?orig=true&version=1.0)

### 解题

点开shell,是个一句话木马

![3.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whze4cc4330958747e188d2b0d9b85533f8?orig=true&version=1.0)

题目不让输入flag，也提示了href="shell.txt"，那么?file=shell.txt

![01.png](https://previewengine.zohopublic.com.cn/image/WD/u4whzf91f12bb6a6b41a299127be1060217f7?version=1.0&width=2046&height=1536)

接着用hcakbar



![02.png](https://previewengine.zohopublic.com.cn/image/WD/u4whzed14e1a10667434bb90993591f705c3d?version=1.0&width=2046&height=1536)

## php://input

### 知识

> `phpinfo()` 函数用于输出关于 PHP 配置的大量信息。这些信息涵盖了 PHP 版本、编译选项、服务器环境、PHP 扩展、PHP 常量等众多方面。
>
> `php://` 是 PHP 提供的一种协议流包装器，它可以用于访问各种资源，例如标准输入输出、过滤器等。
>
> `php://input` 是 PHP 中的一个只读流，允许直接访问 HTTP 请求体中的原始数据。

### 题目

![题目2.png](https://previewengine.zohopublic.com.cn/image/WD/u4whzb6a93635baeb44c58d7c63471db4a08a?version=1.0&width=2046&height=1536)

![题目1.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whz55a6f08dbb85426a9d7d0ee023b57d62?orig=true&version=1.0)

### 解题

伪协议，查看phpinfo,php://input是能用的

使用burp伪造，先看一下上级目录

![做1.png](https://previewengine.zohopublic.com.cn/image/WD/u4whze2c5dc64996948f9bcf768fe7e6ff956?version=1.0&width=2046&height=1536)

发现有flag

![做2.png](https://previewengine.zohopublic.com.cn/image/WD/u4whz2336a01e10784476b448aa63b9b0102e?version=1.0&width=2046&height=1536)

进去，获得flag

![做3.png](https://previewengine.zohopublic.com.cn/image/WD/u4whz5609c526f1ff473684587c3b96528e36?version=1.0&width=2046&height=1536)

## 读取源代码

### 知识

> php://filter/\[读|写|两者兼有的过滤器链]/resource=要处理的资源

### 题目

![zz1.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whz0b29d72f42c64f60a4dcf988c837d6bc?orig=true&version=1.0)

![zz2.png](https://previewengine.zohopublic.com.cn/image/WD/u4whz25cf6ef4617e47ce95cc5781d487ee80?version=1.0&width=2046&height=1536)

### 解题

告诉了我们flag的位置了，直接构造php://filter/resource=/flag，获取flag

![zz3.png](https://previewengine.zohopublic.com.cn/image/WD/u4whzad4272096479451a8b16c308161e6573?version=1.0&width=2046&height=1536)

## 远程包含

### 题目

![远程1.png](https://previewengine.zohopublic.com.cn/image/WD/u4whzfa522bc4a098433cbd055d812ace2f0f?version=1.0&width=2046&height=1536)

![远程2.png](https://previewengine.zohopublic.com.cn/image/WD/u4whz07120eeaa7984209bbf2db053ef4f30b?version=1.0&width=2046&height=1536)

### 解题

看一下phpinfo

![远程3.png](https://previewengine.zohopublic.com.cn/image/WD/u4whz77fdfe4f573c4f68a9924df80d92a101?version=1.0&width=2046&height=1536)

发现allow\_url....都是on,php://input是能用的，使用burp抓包，重放，构造，看一下上级目录

![yy1.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whzc2e7b133d2c1440fb8b7a7bdd1921944?orig=true&version=1.0)

发现flag，进去 ，获得flag

![yy2.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whz8806734a4dd64036a107196e579738b3?orig=true&version=1.0)

## 命令注入

### 题目

![ml1.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whz5b3435c7cf5e4b668090a4f1ff8b8d6c?orig=true&version=1.0)

![ml2.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whz5d9e798f2b30420096977df14794367d?orig=true&version=1.0)

### 解题

题目中说了无过滤直接url中输入命令，用;隔开，先看一下目录

![ml3.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whza761eef37a9d46749f6b136dba3dcdb4?orig=true&version=1.0)

有2个文件，都进去看一下

![ml4.png](https://previewengine.zohopublic.com.cn/image/WD/u4whz2176854672ee468d9b99d3af93db8543?version=1.0&width=2046&height=1536)

![ml5.png](https://files.zohopublic.com.cn/public/workdrive-public/previewdata/u4whzd24702f35207419da49544775da7cfea?orig=true&version=1.0)

最终在26433137587301.php的源代码中发现了flag

![flag.png](https://previewengine.zohopublic.com.cn/image/WD/u4whz26cdeba387de40acb65ceadc66f29810?version=1.0&width=2046&height=1536)

