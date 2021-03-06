# 精通比特币
[书籍链接](http://book.8btc.com/books/1/master_bitcoin/_book/)

## 第一章 介绍

### 概念
贝壳的交换一步步构建了人类的物质社会，生活。BitCoin 该是互联网发展到千禧年代的特有产物，象征着人类人活对于网络世界的迁徙。  
比特币系统由网络构成，能够联网的物理设备也成为了虚拟货币世界的入口。  

> 比特币是由一系列概念和技术作为基础构建的数字货币生态系统。狭义的“比特币”代表系统中的货币单位，用于储存和传输价值。用户主要通过互联网使用比特币系统，当然其他网络也可以使用。比特币协议以各种开源软件的形式实现，这些软件可以在笔记本电脑、智能手机等多种设备上运行，让用户方便地接入比特币系统。

### 特性

| 安全(加密)   | 去中心化(网络 存储)  | 可信任(共识) |
|:------------:|:--------------------:|:------------:|
| 唯一数字密钥 | 分布式点对点网络系统 | 区块链       |

>比特币是一种协议、一种网络、一种分布式计算创新的代名词。比特币是这种创新的首次实际应用。作为一个开发者，我看比特币之于货币就像看到当年的互联网，一个通过分布式计算来传播价值和保障数字资产所有权的网络。比起初识比特币，这里将知无不言。

### 故事
| **软件 平台 交易** | **51%攻击**      | **合约**              |
|:------------------:|:----------------:|:---------------------:|
| 北美低价零售       | 北美高价零售     | 离岸合同服务          |
| **众筹**           | **实物商品收支** | **网络安全 特殊设备** |
| 慈善捐赠           | 进口 / 出口      | 比特币挖矿            |

## 第二章 比特币的原理

### 创建交易输出
比特币支付二维码包含(地址 金额 标签 信息)，常见的交易形式有(找零 兑整 分发)。
>与一个简单包含目的比特币地址的二维码不同，当前支付请求的是一个二维编码过的URL，它包含有一个目的地址，一笔支付金额，和一个像“Bob咖啡”这样的交易描述。这使比特币钱包应用在发送支付请求时，可以预先填好支付用的特定信息，给用户显示一种友好易懂的描述。你可以用比特币钱包应用扫描这个二维码来看Alice可能看到的信息

未消费交易输出, BitCoin 钱包由一个个地址构成，每次发送交易都会产生一个新的地址。
```lisp
;; 交易包含 一个或多个(输入 输出) 与 所有权证明
(defconstant `Atransaction 
    ((+ input[@]) (+ output[@]) (fowner towner)))

;; 输出小于输入时产生矿工费
(defun gas (i o)
    (if(> o i)
        (return (- o i))
    ))

```
>简单来说，交易告知全网：比特币的持有者已授权把比特币转帐给其他人。而新持有者能够再次授权，转移给该比特币所有权链中的其他人，产生另一笔交易来花掉这些比特币，后面的持有者在花费比特币也是用类似的方式。


### 将交易在全网确认
发一起笔交易，交易信息会被存入交易池(支付更高交易费率的优先存入)，矿工带着交易池中的交易信息进行挖矿，在发现新一个区块的时候，矿工通过比特币的 P2P 网络传输给网络中的某一节点，这一节点会继续再把交易信息传输给它自身连接的其他节点，当信息覆盖全网之后，所有的钱包客户端也就更新了交易的结果。

## 第三章 比特币核心

![Bitcore](/assets/bitcore.png)  


| Category  | Content                                             |
|:---------:|:---------------------------------------------------:|
| Consensus | Validation Engine                                   |
| Crypto    | Txs / Validation Engine / Wallet                    |
| P2P       | Connection Manager / Miner /Peer Discovery /  RPC   |
| Storage   | Blocks   / Mempool / Storage Engine / Txs /  Wallet |

> Bitcoin Core实现了比特币的所有方面，包括钱包，交易和区块验证引擎，以及P2P网络中的完整网络节点。

## 第四章 密钥和地址

### 简介
数字密钥完全独立于比特币协议。但发送交易时，输入比特币网络的交易信息应该是符合比特币协议标准的。密钥实现了比特币的去中心化信任和控制，所有权认证和基于密码学证明的安全模型。
+ 密钥成对出现，比特币交易需要一个有效的签名才能够存入区块链，用于支出资金的数字签名被称为见证(witness)。
+ 收件人的公钥地址被称为比特币地址，比特币地址由一个公钥生成并对应于这个公钥。并非所有比特币地址都是公钥，他们也可以表示其他支付对象，譬如脚本。

> 比特币的所有权是通过数字密钥、比特币地址和数字签名来确定的。数字密钥实际上并不存储在网络中，而是由用户生成之后，存储在一个叫做钱包的文件或简单的数据库中。存储在用户钱包中的数字密钥完全独立于比特币协议，可由用户的钱包软件生成并管理，而无需参照区块链或访问网络。密钥实现了比特币的许多有趣特性，包括去中心化信任和控制、所 有权认证和基于密码学证明的安全模型。

密钥对包括一个私钥，和由其衍生出的唯一公钥。公钥用于接收比特币，而私钥用于比特币支付时的交易签名。私钥可用于生产特定消息的签名，此签名可以在不泄露私钥的同时对公钥进行验证。
> 大多数比特币钱包工具为了方便会将私钥和公钥以密钥对的形式存储在一起。然而，公钥可以由私钥计算得到， 所以只存储私钥也是可以的。

### 比特币私钥与公钥
生成比特币私钥在本质上与 "在1到2^256之间选一个数字" 无异，只要结果不可预测或不可重复，那么选取数字的具体方法并不重要。  
公钥由私钥通过椭圆曲线乘法获得，椭圆曲线加密法是一种基于离散对数问题的非对称加密法，可以用对椭圆曲线上的点进行加法或乘法运算来表示。

![ECC](/assets/ecc.png)
> 大多数比特币程序使用OpenSSL加密库进行椭圆曲线计算。例如，调用EC_POINT_mul() 函数，可计算得到公钥。

### 比特币地址
比特币地址以数字 "1" 开头。可由公钥经过单向的加密哈希算法得到加密哈希函数在比特币中被广泛使用： 比特币地址、脚本地址以及在挖矿中的工作量证明算法。  
通常用户见到的比特币地址是经过 "Base58Check" 编码的，Base58Check 编码也被用于比特币的其他地方。  

> 为了更简洁方便地表示长串的数字，使用更少的符号，许多计算机系统会使用一种以数字和字母组成的大于十进制的表示法。

Base58Chek 由前缀、数据和校验和组成。我们为 Base58 数据添加叫做 "版本字节" 的前缀，并计算 "双哈希" 校验和，制作 Base58Check。

![base58check](/assets/base58check.png)

>为了更简洁方便地表示长串的数字，使用更少的符号，许多计算机系统会使用一种以数字和字母组成的大于十进制的表示法。Base64通常用于编码邮件中的附件。Base58 是一种基于文本的二进制编码格式，用在比特币和其它的加密货币中。这种编码格式不仅实现了数据压缩，保持了易读 性，还具有错误诊断功能。为了增加防止打印和转录错误的安全性，Base58Check是一种常用在比特币中的Base58编码格式，比特币有内置的检查错误的编码。

### 密钥的格式
公钥和私钥的都可以有多种格式。一个密钥被不同的格式编码后，虽然结果看起来可能不同，但是密钥所编码数字并没有改变。  
**压缩格式公钥**，引入压缩格式公钥是为了减少比特币交易的字节数，从而可以节省那些运行区块链数据库的节点磁盘空间。  
**压缩格式私钥**，私钥是非压缩的，也不能被压缩。  

私钥的格式如此：

| Type           | Prefix | Description                                                                 |
|:--------------:|:------:|:---------------------------------------------------------------------------:|
| Raw            | None   | 32 bytes                                                                    |
| Hex            | None   | 64 hexadecimal digits                                                       |
| WIF            | 5      | Base58Check encoding: Base58 with version prefix of 128- and 32-bitchecksum |
| WIF-compressed | K or L | As above, with added suffix 0x01 before encoding                            |

例如：

| Format         | Private                                                          |
|:--------------:|:----------------------------------------------------------------:|
| Hex            | 1e99423a4ed27608a15a2616a2b0e9e52ced330ac530edcc32c8ffc6a526aedd |
| WIF            | 5J3mBbAH58CpQ3Y5RNJpUKPE62SQ5tfcvU2JpbnkeyhfsYB1Jcn              |
| WIF-compressed | KxFC1jmwwCoACiCAWZ3eXa96mBM6tb3TYzGmf6YwgdGWZgawvrtJ             |

公钥格式：

| Key | Value                                                                                                                               |
|:---:|:------------------------------------------------------------------------------------------------------------------------------------|
| x   | F028892BAD7ED57D2FB57BF33081D5CFCF6F9ED3D3D7F159C2E2FFF579DC341A                                                                    |
| y   | 07CF33DA18BD734C600B96A72BBC4749D5141C90EC8AC328AE52DDFE2E505BDB                                                                    |
| K   | 04F028892BAD7ED57D2FB57BF33081D5CFCF6F9ED3D3D7F159C2E2FFF579DC341A07CF33DA18BD734C600B96A72BBC4749D5141C90EC8AC328AE 52DDFE2E505BDB |

> 实际上“压缩格式私钥”是一种名称上的误导，因为当一个私钥被使用WIF压缩格式导出时，不但没有压缩，而且比“非压缩格式”私钥长出一个字节。这个多出来的一个字节是私钥被加了后缀01，用以表明该私钥是来自于一个较新的钱包， 只能被用来生成压缩的公钥。

### 高级密钥和地址
BIP0038 加密后的密钥前缀为 "6P"，解开它需要一个长密码(由多个单词或一段复杂的数字字母字符串组成)作为口令，原比特币私钥通常使用 WIF 编码过。

> Base58Check编码的比特币地址是以1开头的，而Base58Check编码的私钥WIF是以5开头的。

| Private Key (WIF)                                    | Passphrase        |
|:----------------------------------------------------:|:-----------------:|
| 5J3mBbAH58CpQ3Y5RNJpUKPE62SQ5tfcvU2JpbnkeyhfsYB1JcnA | A String You Want |

以数字3开头的比特币地址是P2SH地址，有时被错误的称谓多重签名或多重签名地址。他们指定比特币交易中受益人为哈希的脚本，而不是公钥的所有者。他们指定比特币交易中受益人为哈希的脚本，而不是公钥的所有者。  
P2SH函数最常见的实现是多重签名地址脚本，设计比特币多重签名特性是需要从总共N个密钥中需要M个签名（也被称为“阈值”），被称为M-N多签名，其 中M是等于或小于N。

| Type | Prefix |
|:----:|:------:|
| Raw  | 1      |
| P2SH | 3      |
| WIF  | 5      |

### 第五章 钱包

比特币钱包分为非确定性钱包和确定性钱包，非确定性钱包中每个密钥都是从随机数独立生成的，确定性钱包所以密钥都是从主密钥派生而来的。  

> 钱包控制用户访问权限，管理密钥和地址，跟踪余额以及创建和签名交易。狭义上，即从程序员的角度来看，“钱包”是指用于存储和管理用户密钥的数据结构。比特币钱包只含密钥，是密钥链。

**非确定性钱包。**比特币核心客户端预先生成100个随机私钥，从最开始就生成足够多的私钥并且每个密钥只使用一次。

![randomWallt](/assets/randomWallet.png)

> 这种钱包现在正在被确定性钱包替换，因为它们难以管理、 备份以及导入。随机密钥的缺点就是如果你生成很多私钥，你必须保存它们所有的副本。这就意味着这个钱包必须被经常性 地备份。每一个密钥都必须备份，否则一旦钱包不可访问时，钱包所控制的资金就付之东流。

**确定性钱包。**确定性，或者“种子”钱包包含通过使用单项离散函数而可从公共的种子生成的私钥。种子是随机生成的数字。

![certainWallt](/assets/certainWallet.png)

> 在确定性钱包中，种子足够恢复所有的已经产生的私钥，所以只用在初始创建时的一个简单备份就足以搞定。并且种子也足够让钱包导入或者导出。这就很容易允许使用者的私钥在钱包之间轻松转移。

**分层确定性钱包。**确定性钱包被开发成更容易从单个“种子”中生成许多密钥。确定性钱包的最高级形式是通过BIP0032标准定义的HD钱包。HD钱包包含以树状结构衍生的密钥，使得父密钥可以衍生一系列子密钥，每个子密钥又可以衍生出一系列孙密钥，以此类推，无限衍生。

![hdWallet](/assets/hdWallet.png)

> 相比较随机（不确定性）密钥，HD钱包有两个主要的优势。  
> 第一，树状结构可以被用来表达额外的组织含义。  
> 第二，它可以允许让使用者去建立一个公共密钥的序列而不需要访问相对应的私钥。


## 疑问 🤔️

##### 钱包生成多个地址，发送一笔交易后返回的新的 UTXO 是否会以新的地址为形式再次存储到钱包里，密钥到底是针对钱包还是某个地址？

##### BTC 的私钥是否可重复，如果重复，会发生什么事情？

<style>img{ padding: 5rem 18rem }</style>
