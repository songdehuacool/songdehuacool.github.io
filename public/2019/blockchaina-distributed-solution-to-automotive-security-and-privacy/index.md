# BlockChain：A Distributed Solution to Automotive Security and Privacy


### Abstract

智能车辆互联提供了一系列先进的服务，这有益于车主、运输当局、车辆制造商和其它服务提供者。但这也可能把智能汽车暴露在一系列安全和隐私威胁之下，如位置追踪或远程劫持车辆。论文谈论了区块链技术，这是解决上述问题的可能方案。论文提出了一个基于区块链的架构来保护用户隐私和增加车辆自治系统的安全性。无线远程软件更新和其他新兴服务（例如动态车辆保险费）用于说明所提出的安全架构的功效。最后还定性地论证了该架构对常见安全攻击的弹性。

### Introduction

智能汽车越来越多的联网或连到其它系统从而使它面临许多安全问题，不仅仅是对智能车辆本身还对路上行人有威胁。人们能通过无线接口远程控制智能车辆核心功能，关于隐私数据的存储和交换也使其面临新的隐私问题。

同时，旧的安全手段因为下面的问题不能用于该系统。

**中心化**

当前架构依赖于中心服务器，面临性能瓶颈和单点失效问题。

**隐私缺失**

当前通信架构基本不考虑用户隐私，不经用户运行获取所有车辆数据并提供广告这些不想要的东西。

**安全威胁**

自动车辆的自动化功能越来越多，由安全漏洞导致的故障就可能威胁驾驶者和行人

区块链因为它拥有它的安全性，数据不可变性和隐私性等特性成为解决智能车辆问题的一个可行方案。提到了以太坊平台和使用比特币作为底层支付手段保证隐私的电动车辆充电平台BlockCharge。也能通过以太坊区块链设计一个用于车辆属主和服务提供者之间安全和隐私的智能合约。作者之前还写了一篇文章介绍了一个用于物联网的优化的区块链实例叫轻量级可扩展区块链（LSB）

本文提出了一个基于区块链的安全和隐私架构，用于智能车辆自治系统。智能车辆、原始设备制造商和服务提供者一起形成一个彼此之间可以相互通信的覆盖网络。这一架构建立在LSB之上，覆盖网络中的节点是成簇的，只有簇首（CH）可以管理区块链和执行核心功能，被命名为overlay block managers(OBMs)。交易的广播和验证都由它完成，从而取代了中心服务器的作用。为了保护隐私，每个智能车辆还配备了车内存储用于存隐私敏感的数据，车辆属主可以定义哪些数据提供给第三方换取更方便的服务，哪些只能存在本地。

覆盖网络中的智能车辆是移动的，与OBM的距离增加会增加延迟，所以提出使用软切换的方式保证智能车辆始终连到离他最近的OBM。

覆盖网络中的通信使用非对称加密，从而保证安全性。

### LSB概述

传统区块链网络面临a)全网广播的高负载和高开销，b)因为要全网广播，节点增加，数据包也增加，不能无限扩展，c)吞吐量的限制三个问题，于是提出了LSB

LSB主要是用一个序列的块生成过程取代了计算密集的工作量难题，每个节点在特定时间间隔只被允许存一个块，并且对网络节点进行簇划分，只由簇首对区块链管理，从而解决扩展性问题，然后用distributed throughput management（DTM）动态调整吞吐量。使用一个分布式可信算法减少块验证时间。

列举了两类型交易，只有发送者的单签名和同时有发送者接收者的多签名。交易广播到覆盖网络里，被OBM验证有效后被打包的block里，多签名的会被OBM和它维护的整个簇的公钥列表做匹配，匹配到的话直接交付，没匹配给其它OBM。

### 基于区块链的架构

这部分描述这个用于智能车辆安全隐私的架构的细节。架构主体是覆盖网络，其中公链被节点管理，节点包括智能车辆、原始车辆制造商、汽车装配线、软件提供者、云存储提供者和用户的移动设备。整个架构如图4。

每个车辆有无线接口和车内存储，无线接口用来连到覆盖网络，车内存储用来存隐私数据。车辆以预定义的时间间隔生成单签名交易，其中包含车内存储的哈希值。这个交易发送到车辆关联的OBM并被存到链里。车内存储的哈希值用于以后验证存储未被改变，同时由于车内存储的容量限制，可以考虑把备份存在属主智能家庭里。备份数据周期性的发送智能家庭的存储里，备份数据的哈希指也被存到链里。

交易被OBM验证和广播，不仅验证当前块的有效，还验证前一个块是否还在链里。每次交易都改变公钥提供了高隐私性，但有些时候却需要确认公钥的属主是不是某个实体，比如设备制造商提供服务时需要确认提供者是制造商。然后这里又引入了第三方证书机构。。。

智能车辆在覆盖网络中的行为通过OBM完成，当它移动时造成的延迟通过软切换完成（好巧，刚在新一代网络这门课里学了软切换）。车辆到新位置时通过测量和相邻的所有OBM的延迟，选一个延迟最小的OBM，然后更新新OBM的公钥列表以便别的节点能找到它，之后断开和旧OBM的连接，并清除在旧OBM公钥列表里的它自己。如果车辆找不到新OBM，因为可能各簇间太分散了，这时维持旧OBM。

### Application

讨论这个架构的一些应用

**远程软件更新**

车辆控制系统的软件更新或bug修复通过一种叫wireless remote software update (WRSU)的机制完成。这一机制在车辆开发、组装、车辆服务中心、自己家都有执行，这一机制的安全性是个大问题，因为它需要对车辆的完全控制。当前的安全架构是中心化的，就比如特斯拉用一个VPN完成远程软件更新，但车辆数多时，这一个架构的扩展性是个问题，并且前面提到的隐私问题这一架构也没办法解决。

但本文的架构能解决这个问题。OEM（原始设备制造商）把软件更新放在云里，然后为每个车辆在云里建一个账户，分配公私钥对，用于车辆进行软件更新的授权和验证。

服务提供者把新版本存在云里，然后建一个多签名交易，自己的公钥和新版本软件的哈希值都存在交易里，车辆可以通过验证哈希值确认软件未被篡改，把OEM公钥放进去然后发给OBM。OBM广播并按流程交付OEM，OEM收到后验证，验证无误广播给所有OBM，所有OBM通知各自管理的簇成员有新更新了。智能车辆通过验证相应OEM的公钥字段做验证，然后通过公私钥对从云下载更新，最后通过哈希值判断新版本软件的完整性。

**保险**

现在的车险很灵活，他们会收集数据评估驾驶行为。本文架构可以用在这个。保险公司在云端建一个存储库，给用户开个账户然后分配公私钥对，用户将相关数据存在保险公司的云里，保险公司凭这个评估用户驾驶行为。用户凭借自己对车内存储的隐私数据的控制决定哪些给保险公司看，同时，保险公司也可以通过公链中车内存储的哈希值判断用户没擅自改数据。

用户可能不再用保险公司的服务或卖车了，这时保险公司把用户账户和数据从云移除。

**电动汽车和智能充电服务**

和保险类似，电动汽车多了，充电桩跟不上，通过收集用户数据可以调整充电时间使之最适合用户。本文架构用于只开放需要的隐私数据给服务提供者换取想要的服务。这些服务提供者可以作为节点加入覆盖网络。

**共享汽车**

这一领域中车辆位置、车解锁使用、支付这些过程通过新架构给一个安全保证。

### 安全和隐私分析

是新架构可能遇到的一些安全和隐私问题

**隐私**

通过把地址和用户行为相关联可能推断出用户身份。可以通过每次交易变化密钥避免这一问题。

**安全**

数据哈希值的使用保证了数据完整性。

加密手段的使用保证了保密性。

OBM管理簇成员避免了流量攻击。

数字签名确认了数据来源可靠。

### 未来研究方向

密钥管理：因为架构里涉及很多密钥对

数据缓存：车辆从云下载数据造成开销与延迟，OBM缓存可以解决这一问题，和Decentralized Caching for Content Delivery Based on Blockchain这篇结合食用更佳

应用：这一架构适合更多的应用

移动：软切换其实并不是最好方式，可以想想其它办法。

### 结论

提出一个基于区块链的架构，用于智能车辆安全与隐私。并分析了其在一些场景中的应用。


---

> Author:   
> URL: http://localhost:1313/2019/blockchaina-distributed-solution-to-automotive-security-and-privacy/  
