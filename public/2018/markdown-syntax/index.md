# Markdown语法


Markdown由Aaron Swartz和John Gruber共同设计

- Aaron Swartz的博客：[http://www.aaronsw.com/](http://www.aaronsw.com/)
- John Gruber的博客： [https://daringfireball.net/ ](https://daringfireball.net/ )

作者中的Aaron Swartz是天才程序员，著名社交网站[Reddit](http://www.reddit.com/)的联合创始人，14岁参与RSS 1.0规格标准的制订，致力于网络信息开放。在2011年7月19日，因被指控从MIT和JSTOR下载480万篇学术论文并以免费形式上传于网络被捕，2013年1月自杀身亡，年仅26岁。    

![Aaron Swartz](https://tse3-mm.cn.bing.net/th?id=OIP.3gYYIbdHi-ZmoY65LaErfgHaF7&amp;pid=Api&amp;rs=1)

Markdown的优点很多，下面稍微列举一下

&#43; 易读（看起开舒服）、易写（语法简单）、易更改(纯文本)，处处体现着极简主义的影子。
&#43; 兼容HTML，可以转换为HTML格式发布。
&#43; 跨平台使用。
&#43; 越来越多的网站支持Markdown。

具体的Markdown语法主要分为如下几部分：标题，段落，引用，代码块，列表，加粗与斜体，分割线与删除线，链接，图片。

## 1. 基础语法

### 标题

标题的定义有两种形式

1. 使用`=`和`-`标记一级和二级标题。

    一级标题使用   `========= `  
    二级标题使用   `---------`

2. 使用`#`，可表示1-6级标题。

    \# 一级标题   
   \## 二级标题   
   \### 三级标题   
   \#### 四级标题   
   \##### 五级标题   
   \###### 六级标题    

**注**：一般习惯从二级标题开始使用，因为一级标题对于多数文章来说，字体都显得有点过大

### 段落

段落的前后要有空行，所谓的空行是指没有文字内容。若想在段内强制换行的方式是使用两个以上空格加上回车（引用中换行省略回车）。

### 引用

在段落的每行或者只在第一行使用符号`&gt;`，如

```markdown
&gt; 区块引用   
```

效果：

&gt; 区块引用  

### 代码块

在每行起始添加4个空格或者一个制表符，注意要和普通段落间存在空行。最常用围墙式代码块，即使用 3 个连续的反单引号把一段文字包围起来表示代码块，这样可以避免每行代码开头都添加 4 个空格，写法如下

```markdown
​```
let i = 100;
let j = 200;
console.log(i &#43; j);
​```
```

使用围墙式代码块还有有个额外的功能：可以指定编程语言类别，让其中的代码实现语法高亮，方法是在第一行反单引号后面写上语言种类的名称，写法如下

```markdown
​```javascript
let i = 100;
let j = 200;
console.log(i &#43; j);
​```
```

效果如下：

```javascript
let i = 100;
let j = 200;
console.log(i &#43; j);
```

行内也可以对较短的字符标记代码，方法是使用两个反单引号，比如  

```
行中`短代码`高亮
```

效果为：  
行中`短代码`高亮

### 列表

使用`·`、`&#43;`、或`-`标记无序列表，符号后需添加一个空格才能继续书写文字

 - 第一项

 &#43; 第二项

使用数字并辅以`.`标记有序列表，

  1. 第一项
  2. 第二项
  3. 第三项

### 加粗与斜体

在强调内容两侧分别加上`*`或者`_`，一个符号为斜体，两个为粗体，如：

```markdown
*斜体*，_斜体_    
**粗体**，__粗体__
```

效果：

 _斜体_    
 **粗体**，__粗体__

### 分割线和删除线

分割线最常使用就是三个或以上`-`，还可以使用`*`和`_`。删除线则是句子前后加两个波浪号`~~`

### 链接

链接可以由两种形式生成：**行内式**和**参考式**。    
行内式语法为：

```markdown
[书葬的github](https://github.com/songdehua)
```

效果：  

 [书葬的github](https://github.com/songdehua)

参考式语法为：

```markdown
[书葬的github][1]    
[书葬的github][2]    
[1]:https://github.com/songdehua   
[2]:https://github.com/songdehua   
```

效果：  

 [书葬的github][1]    
 [书葬的github][2]

[1]: https://github.com/songdehua
[2]: https://github.com/songdehua

### 图片

添加图片的形式和链接相似，只需在链接的基础上前方加一个`!`。如文章开头Azron Swartz图片使用如下语句

```markdown
![Aaron Swartz](https://laregledujeu.org/files/2013/01/Aaron_Swartz.jpg)
```



## 2. 扩展语法

除以上基本语法外，还有一些常用扩展语法，主要是因为在一些特定场景下某些需求无法满足，其中有一些如待办事项和表格等使用非常频繁，因此在这里介绍，其它少用的扩展语法在其它文章里介绍。

### 待办事项

使用`- [ ]`和`- [x]`，效果如下

- [ ] 未选
- [x] 已选

### 反斜杠`\`

相当于**反转义**作用，使Markdown语法符号成为普通符号。

### 表格

用`|`表示表格纵向边界，表头和表内容用`-`隔开，并可用`:`进行对齐设置，两边都有`:`则表示居中，若不加`:`则默认左对齐。

```markdown
| 姓名 | 角色 |
| ---- | ---- |
| 书藏 | 作者 |
```

以上语句效果如下

| 姓名 | 角色 |
| ---- | ---- |
| 书藏 | 作者 |

### 缩进

修改代码块的缩进，方法是选择多行代码，然后按 `Tab` 键增加缩进，按 `Shift &#43; Tab` 键减少缩进。

文字的缩进有两种办法

1. 使用表示空格的特殊字符`&amp;nbsp;`或`&amp;#160;`
2. 输入法半角改全角，然后连续键入两个空格（半角改全角的快捷键为`Shift&#43;Space`）

### Emoji

Emoji是否支持要看主题，github是肯定支持的。关于emoji符号查找表可以查看[emoji cheat sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet/)

### 数学公式

公式的语法规则基本和Latex相同，可参见[常用数学符号的 LaTeX 表示方法](http://www.mohu.org/info/symbols/symbols.htm)

主要也分为行内和区块两种，行内公式使用单个美元符`$`包围，区块使用两个美元符，比如

```markdown
$2^2$

$$
\frac{2}{3}
$$
```

效果如下（当然还要看渲染引擎是否支持，本博客支持显示数学公式）

$2^2$

$$
\frac{2}{3}
$$

### 特殊字符

不论是对公式的编辑，还是平时的使用，经常会遇到一些数学符号、希腊字母等特殊的字符，这些字符可以直接键入其命名实体或十进制代码而无需转义符`\`包含就能显示，对照表见[文末](#jump)，一个简单的例子如下。

```markdown
字符：希腊字母阿尔法
命名实体表示：&amp;Phi;
十进制编码表示：&amp;#934;
```

效果为&amp;Phi;

注1：命名实体和十进制编码后的分号是整体的一部分，不是分隔符

注2：有需要参考更多的 [Markdown基础语法](https://www.markdownguide.org/basic-syntax) 和 [Markdown扩展语法](https://www.markdownguide.org/extended-syntax)

## 3. HTML语法辅助

由于书写的文本最终还是要转换成HTML页面，所以实际上可以使用一些HTML的语法来辅助书写

### 插入空行

使用`&lt;/br&gt;`可以替代作为空行插入

### 文字居中

写法如下

```markdown
&lt;center&gt;这一行需要居中&lt;/center&gt;
```

效果如下

&lt;center&gt;这一行需要居中&lt;/center&gt;
### 上下标

写法如下

```markdown
H&lt;sub&gt;2&lt;/sub&gt;O
爆米&lt;sup&gt;TM&lt;/sup&gt;
```

效果如下

H&lt;sub&gt;2&lt;/sub&gt;O 

爆米&lt;sup&gt;TM&lt;/sup&gt;

### 字体颜色与字号

写法如下

```markdown
&lt;font color=&#34;#FF0000&#34;&gt; 红色 &lt;/font&gt; 
&lt;font size=6&gt; size=6 &lt;/font&gt; 
&lt;font size=5 color=&#34;#FF0000&#34;&gt; size=5的红色&lt;/font&gt;
```

效果如下

&lt;font color=&#34;#FF0000&#34;&gt; 红色 &lt;/font&gt; 
&lt;font size=6&gt; size=6 &lt;/font&gt; 
&lt;font size=5 color=&#34;#FF0000&#34;&gt; size=5的红色&lt;/font&gt;

### 图片

原始图片规格不一，展示出来的效果往往很不好，使用HTML的语法可以定制图片的某些属性。以上面的创始人Aaron Swartz的图片为例，我们控制其大小

```markdown
&lt;img src=&#34;https://laregledujeu.org/files/2013/01/Aaron_Swartz.jpg&#34; width=&#34;512&#34; height=&#34;384&#34; /&gt;
```

通过将多张图片放在一个一行多列的表格中，线宽设置为0， 可以让这些图片并排显示，代码如下

```html
&lt;table&gt;&lt;tr&gt;
&lt;td&gt;&lt;img src=&#34;http://bimgs.plmeizi.com/images/bing/2019/OHR.BeaujolaisRegion_ZH-CN1585928268_1920x1080.jpg&#34; alt=&#34;风景1&#34; style=&#34;zoom: 67%;&#34; /&gt;&lt;/td&gt;
&lt;td&gt;&lt;img src=&#34;http://bimgs.plmeizi.com/images/bing/2020/OHR.MalhamStars_ZH-CN4163177154_1920x1080.jpg&#34; alt=&#34;风景2&#34; style=&#34;zoom: 67%;&#34; /&gt;&lt;/td&gt;
&lt;/tr&gt;&lt;/table&gt;
```

效果如下

&lt;table&gt;&lt;tr&gt;
&lt;td&gt;&lt;img src=&#34;http://bimgs.plmeizi.com/images/bing/2019/OHR.BeaujolaisRegion_ZH-CN1585928268_1920x1080.jpg&#34; alt=&#34;风景1&#34; style=&#34;zoom: 67%;&#34; /&gt;&lt;/td&gt;
&lt;td&gt;&lt;img src=&#34;http://bimgs.plmeizi.com/images/bing/2020/OHR.MalhamStars_ZH-CN4163177154_1920x1080.jpg&#34; alt=&#34;风景2&#34; style=&#34;zoom: 67%;&#34; /&gt;&lt;/td&gt;
&lt;/tr&gt;&lt;/table&gt;


### 页内跳转

先定义一个锚

```markdown
&lt;span id=&#34;jump&#34;&gt;Hello World&lt;/span&gt;
```

然后使用markdown语法即可跳转到锚所在之处

```markdown
[XXXX](#jump)
```

比如数学公式部分点击[文末](#jump)可以跳转到附录

## 附录：特殊字符对照表

&lt;span id = &#34;jump&#34;&gt;普通字符&lt;/span&gt;

| 特殊符号 | 命名实体  | 十进制编码 |
| :------: | :-------: | :--------: |
|   空格   | `&amp;nbsp;`  |  `&amp;#160;`  |
| 全角空格 | `&amp;emsp;`  | `&amp;#12288;` |
|    ’     | `&amp;apos;`  |  `&amp;#39;`   |
|    &#34;     | `&amp;quot;`  |  `&amp;#34;`   |
|    (     |     —     |  `&amp;#40;`   |
|    )     |     —     |  `&amp;#41;`   |
|    &lt;     |  `&amp;lt;`   |  `&amp;#60;`   |
|    &gt;     |  `&amp;gt;`   |  `&amp;#62;`   |
|    [     |     —     |  `&amp;#91;`   |
|    ]     |     —     |  `&amp;#93;`   |
|    {     |     —     |  `&amp;#123;`  |
|    }     |     —     |  `&amp;#125;`  |
|    ´     | `&amp;acute;` |  `&amp;#180;`  |
|    °     |  `&amp;deg;`  |  `&amp;#176;`  |
|    ®     |  `&amp;reg;`  |  `&amp;#174;`  |
|    ©     | `&amp;copy;`  |  `&amp;#169;`  |

数学符号

| 特殊符号 |  命名实体  | 十进制编码 |
| :------: | :--------: | :--------: |
|    ≤     |   `&amp;le;`   | `&amp;#8804;`  |
|    ≥     |   `&amp;ge;`   | `&amp;#8805;`  |
|    ≈     | `&amp;asymp;`  | `&amp;#8773;`  |
|    ≠     |   `&amp;ne;`   | `&amp;#8800;`  |
|    ∩     |  `&amp;cap;`   | `&amp;#8745;`  |
|    ∪     |  `&amp;cup;`   | `&amp;#8746;`  |
|    ∠     |  `&amp;ang;`   | `&amp;#8736;`  |
|    ∞     | `&amp;infin;`  | `&amp;#8734;`  |
|    ±     | `&amp;plusmn;` |  `&amp;#177;`  |
|    √     | `&amp;radic;`  | `&amp;#8730;`  |
|    ∑     |  `&amp;sum;`   | `&amp;#8722;`  |
|    ∫     |  `&amp;int;`   | `&amp;#8747;`  |
|    Δ     | `&amp;Delta;`  |  `&amp;#916;`  |

希腊字母

| 特殊符号 |  命名实体   | 十进制编码 |
| :------: | :---------: | :--------: |
|    Φ     |   `&amp;Phi;`   |  `&amp;#934;`  |
|    Ω     |  `&amp;Omega;`  |  `&amp;#937;`  |
|    α     |  `&amp;alpha;`  |  `&amp;#945;`  |
|    β     |  `&amp;beta;`   |  `&amp;#946;`  |
|    γ     |  `&amp;gamma;`  |  `&amp;#947;`  |
|    δ     |  `&amp;delta;`  |  `&amp;#948;`  |
|    ε     | `&amp;epsilon;` |  `&amp;#949;`  |
|    ζ     |  `&amp;zeta;`   |  `&amp;#950;`  |
|    η     |   `&amp;eta;`   |  `&amp;#951;`  |
|    θ     |  `&amp;theta;`  |  `&amp;#952;`  |
|    λ     | `&amp;lambda;`  |  `&amp;#955;`  |
|    μ     |   `&amp;mu;`    |  `&amp;#956;`  |
|    ξ     |   `&amp;xi;`    |  `&amp;#958;`  |
|    π     |   `&amp;pi;`    |  `&amp;#960;`  |
|    ρ     |   `&amp;rho;`   |  `&amp;#961;`  |
|    σ     |  `&amp;sigma;`  |  `&amp;#963;`  |
|    φ     |   `&amp;phi;`   |  `&amp;#966;`  |
|    ψ     |   `&amp;psi;`   |  `&amp;#968;`  |
|    ω     |  `&amp;omega;`  |  `&amp;#969;`  |
|    ∂     |  `&amp;part;`   | `&amp;#8706;`  |
|    ∅     |  `&amp;empty;`  | `&amp;#8709;`  |

## 参考与扩展

[1]  [Github-Markdown](https://github.com/younghz/Markdown)

[2]  [Set table column width via Markdown](&lt;https://stackoverflow.com/questions/36121672/set-table-column-width-via-markdown&gt;)

[3]  [Markdown资源列表](https://github.com/nicejade/nice-front-end-tutorial/blob/master/tutorial/markdown-tutorial.md)



---

> Author:   
> URL: http://localhost:1313/2018/markdown-syntax/  

