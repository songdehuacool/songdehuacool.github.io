# Hugo搭建个人博客6-CDN加速


个人博客用的是 Github Pages 服务，国内访问实在是太慢了，于是想用 CDN 做加速。

## CDN介绍

CDN 全称为 Content Delivery Network，中文名为内容分发网络，以下介绍来自[^1]

[^1]:[内容分发网络 CDN 产品概述-产品简介-文档中心-腾讯云 (tencent.com)](https://cloud.tencent.com/document/product/228/2939)

### 加速原理

假设您的业务源站域名为 `www.test.com`，域名接入 CDN 开始使用加速服务后，当您的用户发起 HTTP 请求时，实际的处理流程如下图所示：

![CDN加速原理](https://qcloudimg.tencent-cloud.cn/image/document/9a8c5981e10ba9f5fa35378ecd00f22b.png)

详细说明如下：

1. 用户向 `www.test.com` 下的某图片资源（如：1.jpg）发起请求，会先向 Local DNS 发起域名解析请求。

2. 当 Local DNS 解析 `www.test.com` 时，会发现已经配置了 CNAME `www.test.com.cdn.dnsv1.com`，解析请求会发送至 Tencent DNS（GSLB），GSLB 为腾讯云自主研发的调度体系，会为请求分配最佳节点 IP。

3. Local DNS 获取 Tencent DNS 返回的解析 IP。

4. 用户获取解析 IP。

5. 用户向获取的 IP 发起对资源 1.jpg 的访问请求。

6. 若该 IP 对应的节点缓存有 1.jpg，则会将数据直接返回给用户（10），此时请求结束。若该节点未缓存 1.jpg，则节点会向业务源站发起对 1.jpg 的请求（6、7、8），获取资源后，结合用户自定义配置的缓存策略，将资源缓存至节点（9），并返回给用户（10），此时请求结束。

### 加速原理类比说明

CDN 的原理类似增加了仓储模式的网购过程（商家 = 源站；买家 = 用户；仓库 = CDN 节点）： 早期网购的方式是商家直接给全国各地的买家发送商品，送货时间受商家和买家的物理距离影响，距离长的自然送货时间就长；为解决该问题，网购平台在全国各省建设好仓库，商家将商品提前放到各省的仓库中，之后买家购买的商品就可以选择就近的仓库发货，有效减少了送货时间。

类比过程如下：

1. 用户获取最佳 CDN 节点 IP 的过程（加速原理详细说明1、2、3、4）： 买家要购买某个商品时，先在网购平台查询商品，网购平台将告知距离买家最近的仓库是哪个。

2. 用户请求 CDN 节点的资源响应的过程（加速原理详细说明5、6）： 买家向最近的仓库发送购买商品的消息，若仓库有该商品的库存，则直接将商品发送给买家；若仓库没有该商品的库存，则仓库将反馈商家，由商家将商品先发往仓库，再从仓库发送给买家。

3. CDN 节点缓存过期判断的过程（加速原理详细说明6）： 商家可以设置商品在仓库的存放过期时长，如30天。当买家购买的商品存放时间在30天内，仓库将直接发送给买家；而超过30天的商品将视为过期，仓库会清理过期商品的库存，买家购买时需要重新由商家发送新的商品至仓库。

4. 源站资源变更后 CDN 缓存更新的过程（加速原理详细说明7）： 当商品有更新时，为了保证买家获取到最新的商品，商家需要主动告知仓库清理该商品未过期的库存，否则仓库仍会将旧商品发送给买家。

腾讯云提供了 CDN 和 ECDN 两类服务，其中 CDN 针对静态资源，例如：html、css 和 js 文件、图片、视频、软件安装包、apk 文件、压缩包文件等，在用户多次访问某一资源时返回相同的内容，推荐的场景包括网站静态资源加速、大文件下载场景加速、音视频点播网站加速等；ECDN 针对动态资源，例如：API 接口、.jsp、.asp、.php、.perl 和 .cgi 文件等。

我们本次加速的是个人博客网站，加速内容为静态资源，所以选择 CDN 服务。开通CDN的准备工作

## 域名管理

开通腾讯云 CDN 要求必须拥有一个自有域名和可访问的站点，目前可访问的站点已经有了，我们还需要从腾讯云买个域名，之前我买过三年的 top 域名，只是后来过期了，这一次再买三年，费用小于100，可以接受。购买完成后开始进行域名配置。

### 第一步：添加域名

1. 登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)；

2. 单击左侧菜单内的**域名管理**，进入域名管理列表；

3. 单击**添加域名**，添加一个新域名；





---

> Author:   
> URL: http://localhost:1313/2023/using-hugo-to-build-personal-blog-6-cdn/  
