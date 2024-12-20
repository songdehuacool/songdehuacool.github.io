# Authentication and Authorization for the Internet of Things


Kim H, Lee E A. Authentication and Authorization for the Internet of Things[J]. IT Professional, 2017, 19(5): 27-33.

核心：locally centralized, globally distributed的认证与授权

引入：由2016年DNS服务商Dyn受到的DDoS攻击说明物联网带来的安全挑战。由2015年乌克兰电网受到的攻击说明物联网遭受攻击的后果更具破坏性。这两者反映的是，物联网设备缺乏相应的访问控制机制，导致面对攻击不够健壮。

&lt;!--more--&gt;

## 认证和授权

**授权**是确定实体（设备或用户）是否可以访问资源（如，读取或写入数据、执行程序和控制执行器）的过程。还包括拒绝或撤销访问权限，尤其是针对恶意用户或行为。

**认证**是识别实体的过程，是授权的前提。认证本质上基于信任，比如身份证是基于对国家的信任。现在的网站使用HTTPS协议，这是建立在[SSL/TLS](&lt;https://www.techug.com/post/https-ssl-tls.html&gt;)上的HTTP。SSL/TLS使用公钥加密进行信道构建，所以，服务器公钥的真实性至关重要。

**证书**是用于认证的令牌，其中包含服务器公钥。证书由证书颁发机构（CA）办法并进行数字签名。最初的时候，CA为银行网站颁发证书，该证书被浏览器信任。浏览器使用CA的证书验证银行网站的证书，如果验证成功，就信任该网站。所以，公钥基础设施（PKI）就是用于颁发和管理这些证书的一组角色和策略。

有很多方法来实现计算机系统中用于认证的令牌。密码是验证人类用户最常见的方式，为了提高安全性，密码之外，还经常使用手机（what we have）或指纹(what we are)等辅助验证。而在机器到机器的通信中，加密是最有效的提供安全保证的手段。在加密系统中，加密密钥通常用作认证和授权的令牌，因此，很多情况下，认证和授权问题可以归结为生成和管理加密密钥的问题。

## 建立信任的方式

建立信任通常从信任根（root of trust）开始。信任根就是一个特殊的实体，是一定可被信任的，比如PKI中的根证书。然后，基于信任根，可以建立更进一步的信任关系。这种信任关系有两种类型，一种是集中式（如下图b），一种是分布式（如下图c）。

![](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/6294/8057714/8057722/8057722-fig-2-source-small.gif)

### A. 集中式

集中式方案中的证书颁发机构叫可信第三方，代表是基于SSL/TLS的PKI体系。无线传感器网络(WSNs)也使用这种方式，它们使用具有足够资源的基站和电池供电的传感器节点写作。有时，基站也作为传感器节点的信任根，尤其是作为密钥分发器。一个例子是Sensor Network Encryption Protocol(SNEP)，其中传感器节点和基站共享称为“主密钥”的密钥，所有其它密钥基于主密钥生成，换句话说，基于对基站的信任。

集中式的缺陷是证书颁发机构的错误可能导致整个系统的崩溃，一个例子是2016年中国的CA—WoSign的事故。

### B. 分布式

分布式方案中参与者自主协调建立进一步的信任，从而避免中心化的单点故障。电子邮件加密标准OpenPGps也使用证书，但证书由其它受信任用户签名而不是证书颁发机构。比特币系统同样是由网络中其它节点验证。

The Localized Encryption and Authentication Protocol (LEAP&#43;)是基于分布式安全的WSNs的安全协议，其中基站的作用只限于节点初始化等任务，密钥创建和管理由节点自身和相邻节点协作完成。

分布式的方案往往可扩展性更好，但恶意节点过多也更危险。并且，管理和跟踪整个系统也更困难。

## 本地集中，全局分布的架构

引入名为Auth的实体进行本地验证和授权，它可以部署在任意类型的边缘设备中，为本地注册的实体（IoT设备）提供授权服务，同时管理全局范围内与其它Auths的信任关系，称为本地集中，全局分布的架构，如下图。

![](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/6294/8057714/8057722/8057722-fig-3-source-small.gif)

### A. 本地集中

Auth会在本地保留已注册设备的凭据，因为我们希望本地的管理者可以更好地管理Auth和已注册地设备。这种本地的网络粒度根据网络性质而变化，如可以是PAN或车联网。

Auth将在本地注册的实体的凭据和访问策略存在数据库中，授权过程通过分发会话密钥实现，这种会话密钥只对特定访问操作有效。为了支持异构的物联网环境，Auth还可以支持多种底层通信协议，如Wi-Fi和BLE，并通过将相同的会话密钥分发给两个以上实体来支持安全的一对多通信。

### B. 全局分布

当前使用HTTPS在各Auths间通信，访问其它Auths中的注册实体，需要两个Auths合作授权。

## 问题和未来的工作

设备初始化注册过程是繁琐且昂贵的，应尽可能自动化或半自动化。另一个问题是移动设备的授权。


---

> Author:   
> URL: http://localhost:1313/2019/authentication-and-authorization-for-the-internet-of-things/  

