## 名词定义

* **Third-party application**：第三方应用程序，本文中又称"客户端"（client），即上一节例子中的"云冲印"。
* **HTTP service**：HTTP服务提供商，本文中简称"服务提供商"，即上一节例子中的Google。
* **Resource Owner**：资源所有者，本文中又称"用户"（user）。
* **User Agent**：用户代理，本文中就是指浏览器。
* **Authorization server**：认证服务器，即服务提供商专门用来处理认证的服务器。
* **Resource server**：资源服务器，即服务提供商存放用户生成的资源的服务器。它与认证服务器，可以是同一台服务器，也可以是不同的服务器。

## 客户端的授权模式
客户端必须得到用户的授权（authorization grant），才能获得令牌（access token）。OAuth 2.0定义了四种授权方式。

* 授权码模式（authorization code）
* 简化模式（implicit）
* 密码模式（resource owner password credentials）
* 客户端模式（client credentials）

## 授权码模式

![](https://www.ruanyifeng.com/blogimg/asset/2014/bg2014051204.png)

### 执行步骤
1. 用户访问客户端，后者将前者导向认证服务器。
2. 用户选择是否给予客户端授权。
3. 假设用户给予授权，认证服务器将用户导向客户端事先指定的"重定向URI"（redirection URI），同时附上一个授权码。
4. 客户端收到授权码，附上早先的"重定向URI"，向认证服务器申请令牌。这一步是在客户端的后台的服务器上完成的，对用户不可见。
5. 认证服务器核对了授权码和重定向URI，确认无误后，向客户端发送访问令牌（access token）和更新令牌（refresh token）。

## 参考链接

https://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html