# 2018-2021 研究历史


本文总结2018年12月到2021年4月的研究工作历史，不包括论文阅读工作。

## 2018.12

- 区块链主流共识算法收集了解和分析
- IIoT 与区块链结合的场景收集和一些研究思路， [总结文档地址](https://songdehua.github.io/blockchain-for-iot/)
- 利用 Hyperledge Composer 完成供应链场景下的易腐食品运输示例

## 2019.01

- 实时与非实时数据的区别，区块链存储问题分析，[总结文档地址](https://songdehua.github.io/data-storage-in-blockchain/)
- 区块链平台比较和选择，[总结文档地址](https://songdehua.github.io/blockchain-platform-compare-and-select/)

## 2019.03

- Ethereum 原理、架构等基本知识学习
- 利用虚拟机搭建 Ethereum 私有链，熟悉转账、挖矿等相关命令和操作
- 了解智能合约编译、部署、调用全过程，了解智能合约开发与测试框架 Truffle
- 搭建 Swarm 分布式存储网络

## 2019.04

- Ethereum 区块生成时间数据集获取及分析 [过程记录](https://songdehua.github.io/extract-the-block-generation-time-of-ethereum/)
- 场景思考，初步的方案设计和实验设计，工业4.0背景了解。[未完成的智能工厂方案设计](https://songdehua.github.io/blockchain-for-smart-factory/)
- 智能合约编程语言 Solidity 语法学习及练习
- 基于已有知识的区块链综述文章撰写，[文档地址](https://songdehua.github.io/blockchain-for-iot/iiota-smart-factory-case-study/)

## 2019.05

- 继续撰写综述文章，智能工厂场景可行性分析及相关问题考虑
- 区块链安全与隐私问题总结分析，比如可能的攻击、相关解决方案等，相关方向论文阅读
- 注意力集中在两篇当时新出的区块链和智能工厂结合的论文，初步确认了应实现一个访问控制方案

## 2019.06

- 各论文使用的访问控制方案总结比较
- 各论文使用的存储方案总结
- 起草开题报告第一版，确认三个创新方向为：访问控制，存储，其它（如共识、通信方式、不相干区块过滤），并确认具体的细节

## 2019.07

- 开题报告内容继续完善
- 开始关注区块链平台性能分析工具，并将其作为一个可能的方向
- 确认要做的三件事：1. 在 Zhang 的方案上复现然后做改进；2. 区块链压缩；3. 移动性和通信链路不稳定性问题解决

## 2019.08

- 关注性能分析可能遇到的问题及其实验设计细节，寻找可能的方向
- 安排访问控制方案实现的时间表
- 熟悉 Quorum 区块链及其网络搭建
- 开题

## 2019.09

- 设计树莓派和PC的组网方案，Quorum 客户端编译部署到树莓派，最终将树莓派作为节点加入 Quorum网络
- Zhang 论文中的访问控制合约复现，部署及相关问题解决
- 开始关注异常检测方向，了解强化学习概念和信誉问题

## 2019.10

- 复现合约的功能测试，相关测试脚本的编写
- 异常检测方向的论文收集和阅读，相关思路提出，[总结文档地址](https://songdehua.github.io/blockchain-and-anomaly-detection/)
- 访问控制方案场景思考，可优化之处分析，[总结文档地址](https://songdehua.github.io/idea-design-and-optimization-of-smart-contract-based-access-control-scheme/)

## 2019.11

- 实验室已有设备梳理及实验方案设计
- 优化的访问控制方案设计及智能合约实现
- 区块链用于物联网访问控制的全部问题总结，[文档地址](https://songdehua.github.io/blockchain-based-access-control-for-iot/)

## 2019.12

- 区块链发展情况调查，包括论文发表情况，期刊、会议和基金信息，研究团队，著名研究者，征稿情况等
- 已实现的访问控制合约功能测试，使用Truffle 部署，Gas和时间消耗统计，合约安全性检查

## 2020.01

- 整理已完成访问控制工作，总结创新点，思考下一步研究方向（异常检测、区块链压缩，细化方案，性能测试工具）
- 通过阅读论文了解当时访问控制发展情况，区块链理论发展情况

## 2020.03

- 论文写作
- 分析存储方向研究思路的可行性
- 开始阅读 Edge-D2D-区块链 的论文

## 2020.04

- D2D与区块链结合背景情况调查，初步方案提出，[总结文档地址](https://songdehua.github.io/blockchain-for-d2d-cache-or-computing-offload/)
- 阅读已有论文分析现有访问控制工作的可扩展性

## 2020.05

- 设计具体的信誉函数，包括奖励和惩罚两部分
- 修改现有合约结构，加入信誉合约，在其中实现设计的信誉函数
- 搭建基于Docker的Quorum区块链环境，寻找合适的区块链浏览器
- 进行合约功能测试，解决浮点数运算产生的影响

## 2020.06

- 完成合约功能测试，使用Mythx 进行合约审计（失败），尝试不同的合约部署方式，确定待测量值及测试方式
- 设计具体的实验场景和设计的访问控制操作，阅读并对比 IBM Food Trust（一个基于区块链的供应链解决方案，
- 测试私有合约及交易，获取合约部署的Gas消耗，测试访问控制时间并和未添加信誉部分时的系统进行对比
- 复现wang的论文

## 2020.07

- 对复现的论文进行功能测试、获取Gas消耗、访问时间测试
- 确认访问时间与智能合约逻辑（代码逻辑、合约结构等）、和网络（发起访问的时机、CPU占用率）之间的关系
- 利用linux time命令测试访问控制进程实际执行的CPU时间

## 2020.08

阅读关于事件到达仿真的相关资料，模拟泊松过程，生成符合指数分布的事件到达间隔时间

## 2020.09

- 阅读论文，跟踪 iot-blockchain-access control 最新发展
- 查找 discrete event simulation 的相关资料，以及查找阅读 supply chain 事件产生符合的数学模型，目前没有进展

- 进一步明确要取得什么样的实验结果，明确攻击模型，对属性、策略等非法的增删改行为，可能造成系统出错的行为，寻找更多的风险行为。
- 寻找时间序列数据集，供应链相关的、过程控制相关的。

## 2020.10

- 完善信誉部分的实验，包括到达时间间隔的生成、恶意行为分类、公平性指标的制定
- 寻找其它待测量的性能指标
- 调整代码，添加策略冲突解决机制、修复源信誉算法的错误、尝试浮点数运算的实现，匹配最新的编译器，统一代码风格，整理实验文档
- 测试系统重构，重新进行实验测试

## 2020.11

- 代码整理打包到Github
- 调整检测算法和输入的相关参数，重新进行实验
- 整理文档，实验收尾
- 对众包、计算卸载、隐私保护方向研究的探讨

## 2020.12-2021.04

研究生毕业论文书写


---

> Author:   
> URL: http://localhost:1313/2021/2018-2020-research-history/  

