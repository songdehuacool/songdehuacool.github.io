# Blockchain for IoT Security and Privacy:The Case Study of a Smart Home


Dorri, Ali &amp; Kanhere, Salil &amp; Jurdak, Raja &amp; Gauravaram, Praveen. (2017). Blockchain for IoT Security and Privacy: The Case Study of a Smart Home. 10.1109/PERCOMW.2017.7917634.

### Abstract

由于物联网网络大规模和分布式的特性，物联网（IoT）安全和隐私仍然是一个主要的挑战。基于区块链的方法可以提供分布式的安全性和隐私性，但会带来显著的能量、延迟和计算开销，不适合大多数资源受限的IoT设备。在我们之前的工作中，我们通过去除PoW（Proof of Work, 工作量证明）和货币（coins）的概念，提出了一个适用于物联网的BC（Blockchain, 区块链）的轻量级实例。我们的方法在智能家居环境中进行了验证，主要包括三层：云存储，overlay和智能家居。在本文中，我们深入研究并概述了智能家居层的各种核心组件和功能。每个智能家居都配备了一个永远在线的高资源设备，称为“miner”，负责处理家庭内外的所有通信。该miner还维护一个私有BC，用于控制和审计通信。我们通过彻底分析其在机密性，完整性和可用性的基本安全目标，表明我们提出的基于BC的智能家居框架是安全的。最后，我们利用仿真结果证明我们的方法引入的开销（在流量，处理时间和能耗方面）相对于其安全性和隐私性增益而言是微不足道的。

&lt;!--more--&gt;

### I. Introduction

物联网设备生成，处理和交换大量与安全相关的关键数据以及隐私敏感信息，因此很容易遭受各种网络攻击。许多构成物联网的新型可联网设备能耗低，重量轻。但这些设备必须将大部分可用的能量和计算资源用于执行核心应用程序，从而使得经济地处理安全和隐私问题变得困难。在能耗和处理开销方面，传统安全方法对于物联网而言往往是高花费的。此外，许多最先进的安全框架都是高度集中式的，并且由于其规模的巨大，多对一流量，单点故障等问题，不一定适合物联网。为了保护用户隐私，现有方法通常会显示噪声数据或不完整数据，这可能会阻碍某些IoT应用程序提供个性化服务。因此，物联网需要轻量级，可扩展且分布式的安全性和隐私保护方法。BC技术有可能解决上述问题。

在之前的工作中，我们认为在物联网环境中无法直接使用BC，需要解决几个问题，例如：求解PoW难题的高资源需求，由广播交易和区块到整个网络造成的交易确认的高延迟以及低可扩展性。我们通过去除PoW的概念和对货币的需求，提出了一个框架。该框架依赖于层次结构和分布式信任来维护BC安全性和隐私性，同时使其更适合IoT的特定要求。我们以智能家居场景为例说明了整个框架，但框架是与场景无关的，可以用于其他物联网场景中。该设计包括三个核心层：智能家居，云存储和overlay。智能设备位于智能家居层内，由miner集中管理。智能家居与服务提供商（SP）、云存储、用户的智能手机或个人计算机一起构成overlay，如图1所示。overlay类似于比特币中的对等网络，将分布式特性引入我们的架构。为了减少网络开销和延迟，overlay中的节点被分组为簇，每个簇选举一个CH（簇头，Cluster Head）。overlay中的众多CH和两个密钥列表一起维护公共BC。这两个密钥列表是：

- requester(请求者)密钥列表，它是被允许访问连接到该簇的智能家居的数据的overlay用户的公钥列表;
- requestee(被请求者)密钥列表，它是连接到此簇的允许访问的智能家居的公钥列表。

智能家居设备使用云存储来存储和共享数据。我们在之前的工作中讨论了overlay和云存储的细节。

![图1 overlay](https://picped-1301226557.cos.ap-beijing.myqcloud.com/YJS_20191114_overlay)

本文的贡献是全面描述了我们的设计中智能家居层的细节。首先概述如何初始化IoT设备，然后解释如何处理交易。使用部署在本地的私有BC用来为IoT设备及其数据提供安全的访问控制。此外，BC生成一个不可变的按时间排序的交易历史记录，该历史记录可链接到其他层以提供特定服务。设计安全性来自多种特性，包括

1. 间接可访问的设备
2. 智能家居和overlay中的不同交易结构

为了实现轻量级安全性，智能家居设备采用对称加密。我们提供定性论证来证明智能家居层实现了机密性，完整性和可用性，并讨论如何阻止诸如linking攻击和DDOS等安全攻击。最后，我们使用仿真提供了一个定量结果，证明我们的框架引起的开销相对较小。本文后面的部分按以下顺序介绍

Section II：设计的主要组件

Section III：深入讨论基于BC的智能家居

Section IV：仿真结果和安全分析

Section V：总结相关工作

Section VI：结论

&lt;br/&gt;

### II. Core Components

介绍图2中智能家居层的主要组成部分。

![图2 overlay of smart home](https://picped-1301226557.cos.ap-beijing.myqcloud.com/YJS_20191114_overlay-of-smart-home)

#### A. Transactions

本地设备或overlay节点间的通信称为transactions。方案里设计了几种不同的交易用于特定的功能。Store交易由设备发起，用于存数据。access交易由SP或房主发起用于访问云存储。monitor交易由SP或房主发起用于周期性的监测设备信息。genesis交易用于添加新设备到智能家居层，remove交易则用于删掉一个设备。所有以上交易使用一个共享密钥用于安全通信。一个轻量级哈希用于检测交易内容的改变。所有的交易（不管是smart home发出的还是接收的）都存在一个本地的私有BC中。

#### B. Local BC

在每个智能家居中，都有一个本地私有BC，它跟踪交易并具有一个策略头来强制执行用户对传入和传出交易的策略。从genesis交易开始，每个设备的交易被链接在一起作为BC中的不可变分类帐。本地BC中的每个区块包含两个头：区块头和策略头，如图2顶部所示。区块头包含前一个区块的哈希值以保持BC不可变。策略头用于对设备授权并在其家中强制执行所有者的控制策略。如图2右上角所示，策略头有四个参数。“请求者”参数指的是接收到的overlay交易中的请求者公钥。对于本地设备，此字段等于“设备ID”，比如图2中示例策略头的第四行。策略头中的第二列表示交易中请求的操作，可以是store（在本地存储数据），store cloud(在云存储上存储数据)，access(访问存储的设备数据)，monitor(访问特定设备的实时数据)。策略头中的第三列是智能家居中设备的ID，最后一列说明是否应该通过对第二列的请求。

除了区块头和策略头之外，每个区块都包含许多交易。本地BC的每个交易都会存储五个参数，如图2的左上角所示。前两个参数用于将同一个设备的交易链接在一起并且在BC中唯一地标识每个交易。交易的相应设备ID写入第三个参数列。“交易类型”是指可以是genesis,access,store 或monitor。如果交易来自overlay，则交易存储在第五个参数列，否则，该参数列为空。本地BC由本地miner维持和管理

#### C. Home Miner

智能家居miner是一种集中处理来往智能家居的传入和传出交易的设备。miner可以与家里的外网网关或独立设备集成。与现有的中心化的安全设备类似，miner对交易进行身份验证，授权和审核。此外，miner还完成以下附加功能：生成创世交易，分发和更新密钥，更改交易结构，以及形成和管理簇。miner将所有交易收集到一个区块中，并将完整区块附加到BC。为了提供额外的容量，miner管理本地存储

#### D. Local Storage

本地存储是一种存储设备，例如在本地用来备份数据的硬盘。本地存储可以与miner集成为一个设备，也可以是单独的设备。存储使用FIFO方法，并将每个设备的数据存储为一条链，所以这里是一个设备一条链，不是所有的设备共用一条链。

### III. The BC-Based Smart Home

讨论Initialization，Transaction Handing，shared overlay

#### A. Initialization

描述添加设备和策略头到本地BC的过程。首先，miner通过生成genesis交易与设备共享密钥。该共享密钥存在genesis交易里。然后定义策略头，房主根据之前所述的图2中的策略结构生成自己的策略，并把策略头添加到第一个区块中。miner在最新的区块中使用该策略头，因此，要更新策略，房主应更新最新的区块中的策略头。

#### B. Transactions Handling

智能设备可能会彼此直接通信或者与智能家居外部的实体通信。家里的每个设备可以请求另一个家里设备的数据以提供某些服务，例如，当有人进入家中时，灯泡从运动传感器请求数据以自动打开灯。为了实现用户对智能家庭交易的控制，miner应该将共享密钥分配给需要彼此直接通信的设备。要分配密钥，miner检查策略头或向所有者请求许可，然后在设备之间分配共享密钥。收到密钥后，只要密钥有效，设备就会直接通信。要拒绝授予权限，miner通过向设备发送控制消息将分布式密钥标记为无效。这种方法的好处是双重的：一方面，miner（以及所有者）有一个共享数据的设备列表，另一方面，设备之间的通信用共享密钥保护

在本地存储上存储数据是家中可能出现的另一种交易形式。要在本地存储数据，需要使用共享密钥对存储进行身份验证。要授予密钥，设备需要发送对miner的请求，如果它具有存储权限，则miner生成共享密钥并为设备和存储发送密钥。通过接收密钥，本地存储器生成包含共享密钥的起始点。使用共享密钥，设备可以将数据直接存储在本地存储中。

设备可能要求将数据存储在云存储上。在云中存储数据是一个匿名过程，在[6]中讨论过。要存储数据，请求者需要一个起始点，该起始点包含用于匿名身份验证的区块号和哈希值。云存储可以由SP拥有和管理（例如Nest恒温器），或者由房主（例如Dropbox）支付和管理。在前一种情况下，miner通过使用设备密钥生成签名交易来请求起始点。在后一种情况下，付款是通过比特币完成的。在任一存储类型中，在收到请求后，存储会创建一个起始点并将其发送给miner。当设备需要在云存储上存储数据时，它会将数据和请求发送给miner。通过接收请求，miner授权设备在云存储上存储数据。如果设备已被授权，则miner从本地BC中提取最后的区块编号和散列，并创建store交易并将其与数据一起发送到存储器。在存储数据之后，云存储将新的区块号返回给用于进一步存储交易的miner。

其他可能的交易是访问和监视交易。这些交易主要由房主在外面监控房屋时产生，或由SP来处理设备的个人服务数据。通过从overlay中的节点接收access交易，miner检查所请求的数据是在本地还是云存储上。如果数据存储在本地存储中，则miner从本地存储请求数据并将其发送给请求者。另一方面，如果数据存储在云中，则miner要么从云存储请求数据并将其发送给请求者，要么将最后的区块号和散列发送给请求者。后一种情况使请求者能够读取设备在云存储中存储的整个数据，并且当存储的数据用于唯一设备时是合适的。否则，用户的隐私可能会受到链接攻击的威胁，这将在后面的第IV节中讨论。

通过接收monitor交易，miner将请求的设备的当前数据发送给请求者。如果允许请求者在一段时间内接收数据，则miner定期发送数据，直到请求者向miner发送关闭请求并废除交易。monitor交易使房主能够观看发送定期数据的摄像机或其他设备。为了避免开销或可能的攻击，所有者应该以分钟为单位定义周期性数据的阈值。如果miner为请求者发送数据的时间达到阈值，则miner终止连接。

#### C. Shared Overlay

当一个人有多套房子，他需要为每套房子都部署miner和存储。为了降低这种情况下的花费和管理开销。定义了一个shared overlay。shared overlay由至少两个智能家庭组成，但由一个共同的miner管理，逻辑上可以视作一个家庭。但有些地方和一个家庭的情况还是有区别的，比如即使是shared overlay的情况，其中每个家庭也都有一个自己的创世交易，所有设备的创世交易都链到它们家庭的创世交易上。又比如设备间通信，同一个家庭内的设备间通信自然没有什么区别，但不同的家庭间设备的通信则通过VPN完成，数据包从一个家庭的miner路由到另一个家庭的miner。

### IV. Evaluation and Anlysis

讨论安全性、隐私和方案性能

#### A. 安全分析

任一设计都应保证三个安全需求：机密性、完整性和可用性。机密性确保只有授权用户才能阅读该消息。完整性确保目标接收到未经修改的消息，可用性意味着用户需要时每个服务或数据都是可用的。前两个需求的实现第III部分以及说清楚了。为了增加智能家居可用性，使设备可以免受恶意请求的影响，可以通过将接受的交易限制为每个设备已与其建立共享密钥的那些实体来实现的。从overlay接收的交易在将它们转发到设备之前由miner授权。此外，我们方案还带来了一些处理上的延迟，但这些延迟并不会影响可用性。表一总结了我们的方案如何实现上述需求

表1.

| 需求     | 保证方法                            |
| -------- | ----------------------------------- |
| 机密性   | 通过对称加密实现                    |
| 完整性   | 通过哈希实现                        |
| 可用性   | 通过限制设备和miner可接受的交易实现 |
| 用户控制 | 通过在本地BC中记录交易实现          |
| 身份鉴别 | 通过使用策略头和共享密钥实现        |

接下来分析该方案应对DDoS攻击和Linking攻击的有效性

1. DDoS Attack

   首先，攻击者不可能直接在智能家居设备上安装恶意软件，因为所有的交易都由miner检查，所有的设备都无法直接访问。

   其次，假设设备被感染，称为恶意节点，由于所有传入传出的请求都由miner通过检查策略头授权，构成DDoS攻击流量的请求是不会被授权的。

2. Linking Attack

   为了防止这种攻击，每个设备的数据由唯一密钥共享和存储。miner使用不同的公钥为每个设备在云存储中创建唯一的数据分类帐。从overlay的角度来看，miner应该为每个交易使用唯一的密钥。

#### B. 性能分析

本文架构为了提供改进的安全性和隐私性，引入了额外的计算和分组开销。通过使用Cooja仿真器仿真智能家居场景，和没有使用加密，哈希和区块链的场景做对比，结果如下：

1. Packet 开销：显著增大
2. 时间开销：由于额外的加密和哈希操作，需要更多的时间，但引入的额外时间最多不超过20ms，可以接收。
3. 能量开销：能耗几乎增加了一倍。

作者认为相比于该方案带来的安全性和隐私性，额外引入的这些开销是可以接受的。

### V. Related Works

首先是两篇论文说明了现有的智能家居场景确认有效的安全防御手段

14. S. Notra M. Siddiqi H. H. Gharakheili V. Sivaraman R. Boreli &#34;An experimental study of security and privacy risks with emerging household appliances&#34; Communications and Network Security (CNS) 2014 IEEE Conference on pp. 79-84 2014.
15. V. Sivaraman D. Chan D. Earl R. Boreli &#34;Smart-phones attacking smart-homes&#34; Proceedings of the 9th ACM Conference on Security &amp;amp; Privacy in Wireless and Mobile Networks pp. 195-200 2016.

以及一个现有的处理智能家居场景安全和隐私的方案，通过使用两个数据集保证真实用户对数据的访问权，但对服务提供商无法提供有效的隐私保证。

3. A. Chakravorty T. Wlodarczyk C. Rong &#34;Privacy preserving data analytics for smart homes&#34; Security and Privacy Workshops (SPW) 2013 IEEE pp. 23-27 2013.

&lt;br/&gt;

### VI. Conclusion

如今，物联网安全正受到学术界和工业界的广泛关注。由于高能耗和处理开销，现有的安全解决方案不适合物联网。我们提出的方法通过利用BC来解决这些挑战。使用智能家居场景为例研究讨论了这个想法。在本文中，我们概述了智能家居层的各核心组件，并讨论了与之相关的各种交易和程序。我们还提供了有关其安全性和隐私的全面分析。我们的仿真结果表明，对于低资源IoT设备，我们的方法产生的开销很低且易于管理。我们认为，鉴于提供的安全性和隐私优势，引入的开销是值得的。


---

> Author:   
> URL: http://localhost:1313/2019/blockchain-for-iot-security-and-privacythe-case-study-of-a-smart-home/  

