# Golang密码学算法


在 Go 中，加密是很重要的一部分，本文对此进行介绍。

&lt;!--more--&gt;

## 1. Hash

利用 Hash 算法可以将任意长度的二进制值（明文）映射为较短的固定长度的二进制值（Hash 值），是密码学的基础之一。

### 1.1 流行的Hash算法

目前常见的Hash算法包括Message Digest（MD）系列和Secure HashAlgorithm（SHA）系列算法。

MD算法主要包括MD4和MD5两个算法。MD4（RFC 1320）是MIT的Ronald L. Rivest在1990年设计的，其输出为128位。MD4已被证明不够安全。MD5（RFC 1321）是Rivest于1991年发布的MD4改进版本。它对输入仍以512位进行分组，其输出是128位。MD5比MD4更加安全，但过程更加复杂，计算速度要慢一点。MD5已于2004年被成功碰撞，其安全性已不足以应用于商业场景。

SHA算法由美国国家标准与技术研究院（National Institute ofStandards and Technology，NIST）征集制定。SHA-0算法于1993年问世，1998年即遭破解。随后的修订版本SHA-1算法在1995年面世，它的输出为长度160位的Hash值，安全性更好。SHA-1设计采用了MD4算法类似原理。SHA-1已于2005年被成功碰撞，意味着无法满足商用需求。为了提高安全性，NIST后来制定出更安全的SHA-224、SHA-256、SHA-384和SHA-512算法（统称为SHA-2算法）。新一代的SHA-3算法也正在研究中。

**目前MD5和SHA-1已经不够安全，推荐至少使用SHA-256算法**。比特币系统就是使用SHA-256算法。

SHA-3算法又名Keccak算法。Keccak的输出长度有：512位、384位、256位、224位。

SHA-3并不是要取代SHA-2，因为SHA-2目前并没有暴露明显的弱点。由于对MD5出现成功的破解，以及对SHA-1出现理论上破解的方法，NIST认为需要一个与之前算法不同的、可替换的加密杂凑算法，也就是现在的SHA-3。区块链中的以太坊系统就是使用Keccak256算法

### 1.2 SHA-256

SHA-256算法输入报文的最大长度是264 bit，产生的输出是一个256bit的报文摘要。SHA-256算法步骤如下。

1. 附加填充比特：对报文进行填充，使报文长度与448模512同余（长度=448 mod512），填充的比特数范围是1到512，填充比特串的最高位为1，其余位为0。就是先在报文后面加一个1，再加很多个0，直到长度满足mod512=448。为什么是448？因为448&#43;64=512。第二步会加上一个64bit的原始报文的长度信息。
2. 附加长度值：将用64bit表示的初始报文（填充前）的位长度附加在步骤1的结果后（低位字节优先）。
3. 初始化缓存：使用一个256bit的缓存来存放该Hash函数的中间及最终结果。该缓存表示为A=0x6A09E667，B=0xBB67AE85，C=0x3C6EF372，D=0xA54FF53A，E=0x510E527F，F=0x9B05688C，G=0x1F83D9AB，H=0x5BE0CD19。
4. 处理512bit（16个字）报文分组序列：该算法使用了6种基本逻辑函数，由64步迭代运算组成。每步都以256bit缓存值ABCDEFGH为输入，然后更新缓存内容。

每步使用一个32bit Kt（常数值）和一个32bit Wt（分组后的报文）。

### 1.3 示例代码

计算字符串的 SHA-256 使用如下函数原型

```go
func Sum256(data []byte) [Size]byte
```



## 2. 对称加密算法



---

> Author:   
> URL: http://localhost:1313/2020/golang-cryptographic-algorithm/  

