# 以太坊开发5-以太坊节点连接到网络的几种方式


文章翻译自：[Connecting to the network](https://github.com/ethereum/go-ethereum/wiki/Connecting-to-the-network)

## 如何寻找对等节点

在初始化时，geth会使用一组记录在源码中的bootstrap节点来连接。要指定这些节点，只需使用`--bootnodes`选项，并使用逗号分隔参数，举例如下：

```bash
geth --bootnodes enode://pubkey1@ip1:port1,enode://pubkey2@ip2:port2,enode://pubkey3@ip3:port3
```

使用情况为：第一个节点已启动，并使用`admin.nodeInfo.enode`获得其地址，在启动第二个节点时，直接加入`--bootnodes`选项和第一个节点的地址作为参数，可以直接连接两个节点

## 常见问题

无法连接的时候，常见的一些原因如下：

- 本地时钟错误。以太坊连接需要一个准确的时钟，因此，需要检查操作系统的时间并和网络进行同步，不然，即使相差12秒也会造成连接失败。一个时间同步的命令例如：

  ```c
  sudo ntpdate -s time.nist.gov
  ```

- 防火墙配置错误导致阻止了UDP连接。此时可以使用静态节点进行连接或使用`admin.addPeer()`手动配置连接

若想使网络不被发现，可以在geth启动时使用`--nodiscover`选项

## 检查连接

为了检查有多少个节点已连接，`net`模块提供了两个命令来查询已连接节点数量和是否处于监听状态

```javascript
&gt; net.listening
true
&gt; net.peerCount
4
```

若想获取更多关于已连接节点的信息，诸如IP地址和端口号、支持的协议等，可以使用`admin.peers`命令，会返回最近连接的节点列表。

```javascript
&gt; admin.peers
[{
  ID: &#39;a4de274d3a159e10c2c9a68c326511236381b84c9ec52e72ad732eb0b2b1a2277938f78593cdbe734e6002bf23114d434a085d260514ab336d4acdc312db671b&#39;,
  Name: &#39;Geth/v0.9.14/linux/go1.4.2&#39;,
  Caps: &#39;eth/60&#39;,
  RemoteAddress: &#39;5.9.150.40:30301&#39;,
  LocalAddress: &#39;192.168.0.28:39219&#39;
}, {
  ID: &#39;a979fb575495b8d6db44f750317d0f4622bf4c2aa3365d6af7c284339968eef29b69ad0dce72a4d8db5ebb4968de0e3bec910127f134779fbcb0cb6d3331163c&#39;,
  Name: &#39;Geth/v0.9.15/linux/go1.4.2&#39;,
  Caps: &#39;eth/60&#39;,
  RemoteAddress: &#39;52.16.188.185:30303&#39;,
  LocalAddress: &#39;192.168.0.28:50995&#39;
}, {
  ID: &#39;f6ba1f1d9241d48138136ccf5baa6c2c8b008435a1c2bd009ca52fb8edbbc991eba36376beaee9d45f16d5dcbf2ed0bc23006c505d57ffcf70921bd94aa7a172&#39;,
  Name: &#39;pyethapp_dd52/v0.9.13/linux2/py2.7.9&#39;,
  Caps: &#39;eth/60, p2p/3&#39;,
  RemoteAddress: &#39;144.76.62.101:30303&#39;,
  LocalAddress: &#39;192.168.0.28:40454&#39;
}, {
  ID: &#39;f4642fa65af50cfdea8fa7414a5def7bb7991478b768e296f5e4a54e8b995de102e0ceae2e826f293c481b5325f89be6d207b003382e18a8ecba66fbaf6416c0&#39;,
  Name: &#39;&#43;&#43;eth/Zeppelin/Rascal/v0.9.14/Release/Darwin/clang/int&#39;,
  Caps: &#39;eth/60, shh/2&#39;,
  RemoteAddress: &#39;129.16.191.64:30303&#39;,
  LocalAddress: &#39;192.168.0.28:39705&#39;
} ]
```

要检查geth使用的端口和允许节点的enode URL，如下：

```javascript
&gt; admin.nodeInfo
{
  Name: &#39;Geth/v0.9.14/darwin/go1.4.2&#39;,
  NodeUrl: &#39;enode://3414c01c19aa75a34f2dbd2f8d0898dc79d6b219ad77f8155abf1a287ce2ba60f14998a3a98c0cf14915eabfdacf914a92b27a01769de18fa2d049dbf4c17694@[::]:30303&#39;,
  NodeID: &#39;3414c01c19aa75a34f2dbd2f8d0898dc79d6b219ad77f8155abf1a287ce2ba60f14998a3a98c0cf14915eabfdacf914a92b27a01769de18fa2d049dbf4c17694&#39;,
  IP: &#39;::&#39;,
  DiscPort: 30303,
  TCPPort: 30303,
  Td: &#39;2044952618444&#39;,
  ListenAddr: &#39;[::]:30303&#39;
}
```

## 静态节点

Geth还支持一种名为静态节点的特性，如果你有一组确定的节点需要连接，你可以使用静态节点，静态节点在断开连接时会尝试重连。通过配置如下路径的文件来使用。

```bash
&lt;datadir&gt;/geth/static-nodes.json
```

```bash
[
  &#34;enode://f4642fa65af50cfdea8fa7414a5def7bb7991478b768e296f5e4a54e8b995de102e0ceae2e826f293c481b5325f89be6d207b003382e18a8ecba66fbaf6416c0@33.4.2.1:30303&#34;,
  &#34;enode://pubkey@ip:port&#34;
]
```

也可以在Js命令行的运行环境添加静态节点，也就是我们之前所说的手动配置：

```bash
admin.addPeer(&#34;enode://f4642fa65af50cfdea8fa7414a5def7bb7991478b768e296f5e4a54e8b995de102e0ceae2e826f293c481b5325f89be6d207b003382e18a8ecba66fbaf6416c0@33.4.2.1:30303&#34;)
```

目前控制台不支持移除节点、增加节点数量以及增加非静态节点（断开连接时不重连的节点）


---

> Author:   
> URL: http://localhost:1313/2019/the-way-to-connect-to-the-network-about-ethereum-node/  

