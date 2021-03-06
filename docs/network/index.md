---
id: index
title: 网络
---

## IP 地址的分类

国际规定：把所有的 IP 地址划分为 A，B，C，D，E 五类，IP 地址由**网络号 + 主机号**构成。

### A 类地址

一个 A 类 IP 地址由 1 字节的网络地址和 3 字节主机地址组成，网络地址的最高位必须是 "0"（二进制表示），地址范围 `1.0.0.1-126.255.255.254`。可用的 A 类网络有 126 个，每个网络能容纳 1677214 个主机。

> 子网掩码：255.0.0.0

### B 类地址

一个 B 类 IP 地址由 2 个字节的网络地址和 2 个字节的主机地址组成，网络地址的最高位必须是 "10"，地址范围 `128.1.0.1-191.255.255.254`。可用的 B 类网络有 16384 个，每个网络能容纳 65534 主机 。

> 子网掩码：255.255.0.0

### C 类地址

一个 C 类 IP 地址由 3 字节的网络地址和 1 字节的主机地址组成，网络地址的最高位必须是 "110"。范围 192.0.1.1-223.255.255.254。C 类网络可达 2097152 个，每个网络能容纳 254 个主机。

> 子网掩码：255.255.255.0

### D 类地址

D 类 IP 地址第一个字节以 “1110” 开始，它是一个专门保留的地址。它并不指向特定的网络，目前这一类地址被用在多点广播（multicast）中。多点广播地址用来一次寻址一组计算机，它标识共享同一协议的一组计算机。

地址范围 224.0.0.1-239.255.255.254

### E 类地址

此类地址是保留地址，留作将来使用，前五位必须是 11110，网络地址的取值范围是 240~~254。

E 类 IP 范围：前五位为 11110；240.0.0.1~~254.255.255.254

### 特殊地址（不属于 IP 地址分类，只是一些特殊情况）

在这么多网络 IP 中，国际规定有一部分 IP 地址是用于我们的局域网使用，也就是属于私网 IP，不在公网中使用的，他们的范围是：

10.0.0.0 ～ 10.255.255.255

172.16.0.0 ～ 172.31.255.255

192.168.0.0 ～ 192.168.255.255

### 参考

- [IP 地址分类](http://blog.51cto.com/gtssoul/1725462)

## 如何寻找到相应的 DNS 服务器并获取 IP 地址？（以 "buluo.qq.com" 为例）

- 客户端访问最近的一台 DNS 服务器，但其中没有域名对应的信息。
- 后者向根域 DNS 服务器发请求询问，但根域中也没有；判定这个域名是属于 “com” 域的，就返回其管理的 “com” 域的 DNS 服务器的 IP 地址。
- 最近的那个 DNS 服务器又向 “com” 域的 DNS 服务器发请求，也不知道，返回 “qq.com” 域的 DNS 服务器 IP。
- 这台最近的 DNS 服务器又向 “qq.com” 域 DNS 服务器发请求，仍然没有；
- 向 "buluo.qq.com" 这个域下的 DNS 服务器发请求才拿到 IP 地址。
- 最近的 DNS 服务器将获得的 "buluo.qq.com" 的 IP 地址返回给客户端；
- 客户端再拿着这个 IP 地址去请求资源。

![image.png](http://upload-images.jianshu.io/upload_images/3185709-4b650d75f6c5c016.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

为了优化性能，DNS 服务器会对中间的查询结果做个缓存，为保证缓存的实时性，每隔一段时间就会将缓存设为过期。

## Ajax

### 请尽可能详尽的解释 Ajax 的工作原理。

Ajax 的工作原理相当于在用户和服务器之间加了—个中间层 (AJAX 引擎), 使用户操作与服务器响应异步化。并不是所有的用户请求都提交给服务器, 像—些数据验证和数据处理等都交给 Ajax 引擎自己来做, 只有确定需要从服务器读取新数据时再由 Ajax 引擎代为向服务器提交请求。

Ajax 其核心有 JavaScript、XMLHTTPRequest、DOM 对象组成，通过 XmlHttpRequest 对象来向服务器发异步请求，然后 xhr 对象提供了一系列属性，可以监听响应的情况，然后从服务器获得数据，再用 JavaScript 来操作 DOM 而更新页面。

### Ajax 是什么? 如何创建一个 Ajax

全称：Asynchronous JavaScript And XML。（异步传输 JS & xml）所谓异步，在这里简单地解释就是：向服务器发送请求的时候，我们不必等待结果，而是可以同时做其他的事情，等到有了结果它自己会根据设定进行后续操作，与此同时，页面是不会发生整页刷新的，提高了用户体验。

(1) 创建 XMLHttpRequest 对象, 也就是创建一个异步调用对象
xmlhttp = new XMLHttpRequest();
(2) 创建一个新的 HTTP 请求，并指定该 HTTP 请求的方法、URL 及验证信息
(3) 设置响应 HTTP 请求状态变化的函数

```JavaScript
xmlhttp.onreadystatechange = function() {
    if (xmlhttp.readyState==4 && xmlhttp.status==200) {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
}
```

readyState 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。

- 0 请求未初始化（在调用 open() 之前）
- 1 请求已提出（调用 send() 之前）
- 2 请求已发送（这里通常可以从响应得到内容头部）
- 3 请求处理中（响应中通常有部分数据可用，但服务器还没有完成响应）
- 4 请求已完成（可以访问服务器响应并使用它）

(4) 发送 HTTP 请求

```JavaScript
xmlhttp.open("GET", "url", true);
xmlhttp.send();

// 或者
xmlhttp.open("POST", url", true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded"); xmlhttp.send("data");
```

(5) 获取异步调用返回的数据
(6) 使用 JavaScript 和 DOM 实现局部刷新

### 使用 Ajax 都有哪些优劣

#### 优势

无刷新在页面与服务器通信，更新页面，用户体验好。

异步与服务器通信，不需要打断用户的操作，具有更加迅速的响应能力。

前端和后端负载平衡。可以把以前一些服务器负担的工作转嫁到客户端，利用客户端闲置的能力来处理，减轻服务器和带宽的负担，节约空间和宽带租用成本。并且减轻服务器的负担，ajax 的原则是 “按需取数据”，可以最大程度的减少冗余请求，和响应对服务器造成的负担。

界面与应用分离

Ajax 使 WEB 中的界面与应用分离（也可以说是数据与呈现分离），有利于分工合作、减少非技术人员对页面的修改造成的 WEB 应用程序错误、提高效率、也更加适用于现在的发布系统。

基于标准化的并被广泛支持的技术，不需要下载插件或者小程序。

#### 缺点

AJAX 干掉了 Back 和 History 功能，即对浏览器机制的破坏。

AJAX 的安全问题

Ajax 技术就如同对企业数据建立了一个直接通道，这使得开发者在不经意间会暴露比以前更多的数据和服务器逻辑。Ajax 也难以避免一些已知的安全弱点，诸如跨站点脚步攻击、SQL 注入攻击和基于 Credentials 的安全漏洞等等对搜索引擎支持较弱。客户端过肥，太多客户端代码造成开发上的成本。违背 URL 和资源定位的初衷, 采用了 Ajax 技术，也许你在该 URL 地址下面看到的和我在这个 URL 地址下看到的内容是不同的。

## 从浏览器输入一个 URL 到页面渲染，涉及的内容

## OSI 七层模型

- 物理层：底层数据传输，如网线；网卡标准。
- 数据链路层：定义数据的基本格式，如何传输，如何标识；如网卡 MAC 地址。
- 网络层：定义 IP 编址，定义路由功能；如不同设备的数据转发。
- 传输层：端到端传输数据的基本功能；如 TCP、UDP。
- 会话层：控制应用程序之间会话能力；如不同软件数据分发给不同软件。
- 表示层：数据格式标识，基本压缩加密功能。
- 应用层：各种应用软件，包括 Web 应用。

[深入浅出－网络七层模型&&网络数据包](https://www.jianshu.com/p/4b9d43c0571a)

### 网络层

网络层位于传输层和数据链路层之间, 用于把数据从源主机经过若干个中间节点传送到目标主机, 并向传输层提供最基础的数据传输服务, 它要提供路由和选址的工作。

### 传输层

传输层是面向连接的、可靠的的进程到进程通信的协议。TCP 提供全双工服务，即数据可在同一时间双向传播。TCP 将若干个字节构成一个分组，此分组称为报文段 (Segment)。提供了一种端到端的连接。

传输层的协议主要有 TCP 和 UDP，TCP(Transmission Control Protocol) 是一种可靠的、面向连接的协议，传输效率低。UDP(User Datagram Protocol) 是一种不可靠的、无连接的服务，传输效率高。下面重点介绍一下 TCP 的三次握手和四次挥手。

TCP 主要是将数据进行分段打包传输，对每个数据包编号控制顺序，运输中丢失、重发和丢弃处理。

## TCP

TCP（Transmission Control Protocol，传输控制协议）是面向连接的协议，也就是说，在收发数据前，必须和对方建立可靠的连接。

1. TCP 是面向连接的，且传递是顺序的。
2. TCP 是面向字节的。TCP 对字符以及编码没有严格的约束，TCP 数据允许以 ASCII（每个字符一个字节）和 Unicode（每个字符四个字节）进行传输。
3. 可靠性。TCP 的目的是提供可靠的数据传输，基于确认和超时实现一系列的机制来达到可靠性的要求。
4. 流控制。TCP 通过流控制来保证传输数据的平衡。

## UDP

UDP（User Datagram Protocol 用户数据报协议）是 OSI（Open System Interconnection，开放式系统互联）参考模型中一种无连接的传输层协议，提供面向事务的简单`不可靠`信息传送服务。

1. UDP 是一个非连接的协议，传输数据之前源端和终端不建立连接，当它想传送时就简单地去抓取来自应用程序的数据，并尽可能快地把它扔到网络上。 在发送端，UDP 传送数据的速度仅仅是受应用程序生成数据的速度、计算机的能力和传输带宽的限制。在接收端，UDP 把每个消息段放在队列中，应用程序每次从队列中读一个消息段。

2. 由于传输数据不建立连接，因此也就不需要维护连接状态，包括收发状态等，因此一台服务机可同时向多个客户机传输相同的消息。

3. UDP 信息包的标题很短，只有 8 个字节，相对于 TCP 的 20 个字节信息包的额外开销很小。

4. 吞吐量不受拥挤控制算法的调节，只受应用软件生成数据的速率、传输带宽、 源端和终端主机性能的限制。

5. UDP 使用尽最大努力交付，即不保证可靠交付，因此主机不需要维持复杂的链接状态表（这里面有许多参数）。

6. UDP 是面向报文的。发送方的 UDP 对应用程序交下来的报文，在添加首部后就向下交付给 IP 层。既不拆分，也不合并，而是保留这些报文的边界， 因此，应用程序需要选择合适的报文大小。

## WebSocket

WebSocket 协议在 2008 年诞生，2011 年成为国际标准。所有浏览器都已经支持了。

它的最大特点就是，服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息，是真正的双向平等对话，属于服务器推送技术的一种。

其他特点包括：

1. 建立在 TCP 协议之上，服务器端的实现比较容易。
2. 与 HTTP 协议有着良好的兼容性。默认端口也是 80 和 443，并且握手阶段采用 HTTP 协议，因此握手时不容易屏蔽，能通过各种 HTTP 代理服务器。
3. 数据格式比较轻量，性能开销小，通信高效。
4. 可以发送文本，也可以发送二进制数据。
5. 没有同源限制，客户端可以与任意服务器通信。
6. 协议标识符是 ws（如果加密，则为 wss），服务器网址就是 URL。

```js
var ws = new WebSocket("wss://echo.websocket.org");

ws.onopen = function (evt) {
  console.log("Connection open ...");
  ws.send("Hello WebSockets!");
};

ws.onmessage = function (evt) {
  console.log("Received Message: " + evt.data);
  ws.close();
};

ws.onclose = function (evt) {
  console.log("Connection closed.");
};
```

## RESTful

RESTful 是指符合 REST 原则的架构风格，REST 是 Representational State Transfer （表现层状态转移）的缩写。

REST 的名称 "表现层状态转化" 中，省略了主语。"表现层" 其实指的是 "资源"（Resources）的 "表现层"。所谓 "资源"，就是网络上的一个实体，或者说是网络上的一个具体信息。

访问一个网站，就代表了客户端和服务器的一个互动过程。在这个过程中，势必涉及到数据和状态的变化。

互联网通信协议 HTTP 协议，是一个无状态协议。这意味着，所有的状态都保存在服务器端。因此，如果客户端想要操作服务器，必须通过某种手段，让服务器端发生 "状态转化"（State Transfer）。而这种转化是建立在表现层之上的，所以就是 "表现层状态转化"。

客户端用到的手段，只能是 HTTP 协议。具体来说，就是 HTTP 协议里面，四个表示操作方式的动词：GET、POST、PUT、DELETE。它们分别对应四种基本操作：

- GET 用来获取资源
- POST 用来新建资源（也可以用于更新资源）
- PUT 用来更新资源
- DELETE 用来删除资源

### 什么是 RESTful 架构

- 每一个 URI 代表一种资源
- 客户端和服务器之间，传递这种资源的某种表现形式
- 客户端通过四个 HTTP 动词，对服务器端资源进行操作，实现 "表现层状态转移"

### 参考

- [理解 RESTful 架构](http://www.ruanyifeng.com/blog/2011/09/restful.html)
- [RESTful API 设计指南](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)
- [从浏览器输入一个 url 到页面渲染，涉及的知识点及优化点](https://github.com/sunyongjian/blog/issues/34)
- [WebSocket 教程 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2017/05/websocket.html)
