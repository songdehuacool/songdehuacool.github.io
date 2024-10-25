# Hugo搭建个人博客4-主题美化


## 1. 基础知识

通过一个简单的主题开发流程，理解需要的基本知识，为自己进行主题修改和美化打基础，这里参考[create a new theme](https://github.com/digitalcraftsman/hugo-steam-theme/blob/master/exampleSite/content/post/creating-a-new-theme.md)一文。

### 开发准备

Ubuntu安装hugo

```bash
$ snap install hugo --channel=extended
hugo (extended/stable) 0.58.3 from Hugo Authors installed
```

该命令将安装`extended`Sass/SCSS版本(apt-get 安装的hugo版本较低)

建立博客文件

```bash
$ hugo new site newTheme
$ ls -l
total 28
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 15:52 archetypes
-rw-r--r-- 1 songdehua songdehua   82 Sep 25 15:52 config.toml
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 15:52 content
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 15:52 data
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 15:52 layouts
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 15:52 static
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 15:52 themes
```

创建主题

```bash
$ hugo new theme LeaveIt
$ find themes -type f | xargs ls -l
-rw-r--r-- 1 songdehua songdehua    8 Sep 25 16:09 themes/LeaveIt/archetypes/default.md
-rw-r--r-- 1 songdehua songdehua    0 Sep 25 16:09 themes/LeaveIt/layouts/404.html
-rw-r--r-- 1 songdehua songdehua    0 Sep 25 16:09 themes/LeaveIt/layouts/_default/list.html
-rw-r--r-- 1 songdehua songdehua    0 Sep 25 16:09 themes/LeaveIt/layouts/_default/single.html
-rw-r--r-- 1 songdehua songdehua    0 Sep 25 16:09 themes/LeaveIt/layouts/index.html
-rw-r--r-- 1 songdehua songdehua    0 Sep 25 16:09 themes/LeaveIt/layouts/partials/footer.html
-rw-r--r-- 1 songdehua songdehua    0 Sep 25 16:09 themes/LeaveIt/layouts/partials/header.html
-rw-r--r-- 1 songdehua songdehua 1081 Sep 25 16:09 themes/LeaveIt/LICENSE.md
-rw-r--r-- 1 songdehua songdehua  436 Sep 25 16:09 themes/LeaveIt/theme.toml
```

`find themes -type f`将themes目录及其子目录的所有一般文件列出

`xargs ls -l`在`find`命令基础上列出这些文件的基本信息

LeaveIt 包含 templates (以 .html为后缀的文件), license 文件, 主题描述 (theme.toml 文件), 和一个空的archetype.

license文件默认填充MIT协议

根据引号中的描述编辑theme.toml文件，声明主题基本信息，参照[hugoThemes](https://github.com/gohugoio/hugoThemes#themetoml )的说明

```bash
$ nano themes/LeaveIt/theme.toml
name = &#34;Theme Name&#34;
license = &#34;MIT&#34;
licenselink = &#34;Link to theme&#39;s license&#34;
description = &#34;Theme description&#34;
homepage = &#34;Website of your theme&#34;
tags = [&#34;blog&#34;, &#34;company&#34;]
features = [&#34;some&#34;, &#34;awesome&#34;, &#34;features&#34;]
min_version = &#34;0.57.0&#34;

[author]
    name = &#34;Your name&#34;
    homepage = &#34;Your website&#34;

# If porting an existing theme
[original]
    author = &#34;Name of original author&#34;
    homepage = &#34;His/Her website&#34;
    repo = &#34;Link to source code of original theme&#34;
```

编辑config.toml文件，在文件名添加theme字段，启用主题

```bash
$ nano config.toml
baseURL = &#34;http://example.org/&#34;
languageCode = &#34;en-us&#34;
title = &#34;My New Hugo Site&#34;
theme = &#34;LeaveIt&#34;
```

重新生成网站，public文件夹和themes/LeaveIt都将生成js和css文件夹用于控制格式

```bash
$ hugo --verbose
$ ls -l public
total 24
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 15:56 categories
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 16:09 css
-rw-r--r-- 1 songdehua songdehua  468 Sep 25 16:43 index.xml
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 16:09 js
-rw-r--r-- 1 songdehua songdehua  437 Sep 25 16:43 sitemap.xml
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 15:56 tags
$ find themes/LeaveIt -type d | xargs ls -ld
drwxr-xr-x 5 songdehua songdehua 4096 Sep 25 16:32 themes/LeaveIt
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 16:09 themes/LeaveIt/archetypes
drwxr-xr-x 4 songdehua songdehua 4096 Sep 25 16:09 themes/LeaveIt/layouts
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 16:09 themes/LeaveIt/layouts/_default
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 16:09 themes/LeaveIt/layouts/partials
drwxr-xr-x 4 songdehua songdehua 4096 Sep 25 16:09 themes/LeaveIt/static
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 16:09 themes/LeaveIt/static/css
drwxr-xr-x 2 songdehua songdehua 4096 Sep 25 16:09 themes/LeaveIt/static/js
```

### 开发流程

删除public文件夹，执行hugo server命令并添加--watch参数，打开浏览器查看网站，修改主题文件，浏览器页面将会实时更改

建议：不要直接在主题上开发，使用git，在开发分支开发，确认功能无误后合并到主分支

```bash
# 删除public文件夹
$ rm -rf public
# 以watch模式实时查看改动
$ hugo server --watch --verbose
```

更新Home Page 模板，位于layout/目录下：

- index.html
- _default/list.html
- _default/single.html

现在，模板文件是空的，添加以下内容到模板文件

```bash
$ nano themes/LeaveIt/layouts/index.html
&lt;html&gt; 
&lt;body&gt; 
  &lt;p&gt;hugo says hello!&lt;/p&gt; 
&lt;/body&gt; 
&lt;/html&gt;
```

浏览器将显示p标签中的语句

hugo中有三种类型的模板，home页面模板刚刚已修改，single类型的模板用于生成单个内容的文件，list类型的模板用于生成多个内容的文件，即single.html和list.html

还存在partial，content views和terms三种类型的模板，这里不做详细介绍。

更新index.html使之能显示主页

```html
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;body&gt;
  {{ range first 10 .Data.Pages }}
    &lt;h1&gt;{{ .Title }}&lt;/h1&gt;
  {{ end }}
&lt;/body&gt;
&lt;/html&gt;
```

hugo使用Go模板引擎，引擎将扫描模板文件中”{{“和”}}“中间的命令内容并执行，上面的index.html文件中包含三个命令

1. range
2. .Title
3. end

range是迭代器，用于遍历前十个page，hugo创建的每个html文件都属于page，所以遍历pages将查看创建的每个文件

.Title打印`title`变量的值，hugo从markdown文件前面的格式说明中获取该值

end结束range开启的迭代

hugo会在创建html文件前将所有内容加载到变量中，然后模板对其进行处理

因此，更新后的index.html文件将显示first.md和second.md两篇博文的标题

到此开发一个主题的所有知识就全部介绍完毕了，剩下的就是熟悉Go模板的命令及使用它。但这里还有一些内容可以令我们更容易地创建模板

修改single.html文件使之展示博文内容

```html
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;{{ .Title }}&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;h1&gt;{{ .Title }}&lt;/h1&gt;
  {{ .Content }}
&lt;/body&gt;
&lt;/html&gt;
```

修改index.html为博文标题标题添加链接

```html
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;body&gt;
  {{ range first 10 .Data.Pages }}
    &lt;h1&gt;&lt;a href=&#34;{{ .Permalink }}&#34;&gt;{{ .Title }}&lt;/a&gt;&lt;/h1&gt;
  {{ end }}
&lt;/body&gt;
&lt;/html&gt;
```

在content目录创建about.md文件，作为主页面顶级菜单

```markdown
&#43;&#43;&#43;
title = &#34;about&#34;
description = &#34;about this site&#34;
date = &#34;2014-09-27&#34;
slug = &#34;about time&#34;
&#43;&#43;&#43;

## about us

i&#39;m speechless
```

浏览器主页面将显示about菜单，单击即可跳转查看其内容，但它和博文标题放在一起，因此修改index.html文件

```html
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;body&gt;
  &lt;h1&gt;posts&lt;/h1&gt;
  {{ range first 10 .Data.Pages }}
    {{ if eq .Type &#34;post&#34;}}
      &lt;h2&gt;&lt;a href=&#34;{{ .Permalink }}&#34;&gt;{{ .Title }}&lt;/a&gt;&lt;/h2&gt;
    {{ end }}
  {{ end }}

  &lt;h1&gt;pages&lt;/h1&gt;
  {{ range .Data.Pages }}
    {{ if eq .Type &#34;page&#34; }}
      &lt;h2&gt;&lt;a href=&#34;{{ .Permalink }}&#34;&gt;{{ .Title }}&lt;/a&gt;&lt;/h2&gt;
    {{ end }}
  {{ end }}
&lt;/body&gt;
&lt;/html&gt;
```

主页面将分两部分显示：博文和页面。并链接到不同的页面。

改变配置文件中的permalinks，设置页面名

```toml
[permalinks]
	page = &#34;/:title/&#34;
	about = &#34;/:filename/&#34;
```

如果模板文件存在重叠，可以把重叠部分以共享模板的形式放在themes/LeaveIt/layouts/partials/目录。通常，模板文件引用都会有一个指定的路径，但是partials没有，hugo会沿着TODO定义的搜索路径去使用，因此可以编辑这里的内容来覆盖主题的表达。

```bash
$ vi themes/LeaveIt/layouts/partials/header.html
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
	&lt;title&gt;{{ .Title }}&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

$ vi themes/LeaveIt/layouts/partials/footer.html
&lt;/body&gt;
&lt;/html&gt;
```

partials和普通模板调用的不同是没有路径，比如

```html
{{ template &#34;theme/partials/header.html&#34; . }}
vs
{{ partial &#34;header.html&#34; . }}
```

更新index.html文件内容

```html
{{ partial &#34;header.html&#34; . }}

  &lt;h1&gt;posts&lt;/h1&gt;
  {{ range first 10 .Data.Pages }}
    {{ if eq .Type &#34;post&#34;}}
      &lt;h2&gt;&lt;a href=&#34;{{ .Permalink }}&#34;&gt;{{ .Title }}&lt;/a&gt;&lt;/h2&gt;
    {{ end }}
  {{ end }}

  &lt;h1&gt;pages&lt;/h1&gt;
  {{ range .Data.Pages }}
    {{ if or (eq .Type &#34;page&#34;) (eq .Type &#34;about&#34;) }}
      &lt;h2&gt;&lt;a href=&#34;{{ .Permalink }}&#34;&gt;{{ .Type }} - {{ .Title }} - {{ .RelPermalink }}&lt;/a&gt;&lt;/h2&gt;
    {{ end }}
  {{ end }}

{{ partial &#34;footer.html&#34; . }}
```

更新single.html文件

```html
{{ partial &#34;header.html&#34; . }}

  &lt;h1&gt;{{ .Title }}&lt;/h1&gt;
  {{ .Content }}

{{ partial &#34;footer.html&#34; . }}
```

此时浏览器中主页面about菜单将额外展示类型和标题

更新single.html文件，添加对博文日期的渲染

```html
{{ partial &#34;header.html&#34; . }}

  &lt;h1&gt;{{ .Title }}&lt;/h1&gt;
  &lt;h2&gt;{{ .Date.Format &#34;Mon, Jan 2, 2006&#34; }}&lt;/h2&gt;
  {{ .Content }}

{{ partial &#34;footer.html&#34; . }}
```

此时浏览器博文页面将展示创建日期

有多种方式使日期只展示在博文页面中，一种是在index.html中添加if条件语间，另一种是为博文创建单独的模板。当主题比较复杂时，创建针对博文的单独模板

```bash
$ mkdir themes/LeaveIt/layouts/post
$ nano themes/LeaveIt/layouts/_default/single.html
{{ partial &#34;header.html&#34; . }}

  &lt;h1&gt;{{ .Title }}&lt;/h1&gt;
  {{ .Content }}

{{ partial &#34;footer.html&#34; . }}
$ nano themes/LeaveIt/layouts/post/single.html
{{ partial &#34;header.html&#34; . }}

  &lt;h1&gt;{{ .Title }}&lt;/h1&gt;
  &lt;h2&gt;{{ .Date.Format &#34;Mon, Jan 2, 2006&#34; }}&lt;/h2&gt;
  {{ .Content }}

{{ partial &#34;footer.html&#34; . }}
```

移除了默认的single模板中对日期的指定，而在post的single模板添加

至此对主题的基本结构有了了解，接下来应该进一步学习Hugo中Go模板的语法，参见[Introduction to Go Templates](https://github.com/digitalcraftsman/hugo-steam-theme/blob/master/exampleSite/content/post/goisforlovers.md)

注意，以下的调整都是对原主题样式的调整，需要修改主题源码，因此最好clone主题仓库进行开发。

## 2. 调整引用样式

主题原有的引用样式如下

&gt; 引用样式示例

修改`assets/css/_common/_core/base.scss`文件如下调整引用样式

```diff
  }

  blockquote {
-    font-size: 1rem;
-    display: block;
-    border-width: 1px 0;
-    border-style: solid;
-    border-color: $light-border-color;
-    padding: 1.5em 1.2em 0.5em 1.2em;
-    margin: 0 0 2em 0;
-    position: relative;
-
-    &amp;:before {
-      content: &#39;\201C&#39;;
-      position: absolute;
-      top: 0em;
-      left: 50%;
-      transform: translate(-50%, -50%);
-      width: 3rem;
-      height: 2rem;
-      font: 6em/1.08em &#39;PT Sans&#39;, sans-serif;
-      color: $light-post-link-color;
-      text-align: center;
-
-       .dark-theme &amp;{
-         color: $dark-post-link-color;
-       }
-    }
-    &amp;:after {
-      content: &#34;#blockquote&#34; attr(cite);
-      display: block;
-      text-align: right;
-      font-size: 0.875em;
-      color: $light-post-link-color;
-
-       .dark-theme &amp;{
-         color: $dark-post-link-color;
-       }
-    }
&#43;    font: 14px/22px normal helvetica, sans-serif;
&#43;    margin-top: 10px;
&#43;    margin-bottom: 10px;
&#43;    margin-left: 2%;
&#43;    margin-right: 0%;
&#43;    padding-left: 15px;
&#43;    padding-top: 10px;
&#43;    padding-right: 10px;
&#43;    padding-bottom: 10px;
&#43;    border-left: 3px solid #ccc;
&#43;    background-color:#f1f1f1;  

    .dark-theme &amp; {
-      border-color: $dark-border-color;
&#43;      background-color:#252529;
    }
  } 
```

## 3. 添加阅读进度条

首先在`layouts/partials/header.html`文件中如下所示插入代码

```diff
&lt;nav class=&#34;navbar&#34;&gt;
&#43;    {{ if (and .IsPage (not .Params.notsb)) }}
&#43;        &lt;div class=&#34;top-scroll-bar&#34;&gt;&lt;/div&gt;
&#43;    {{ end }}
    &lt;div class=&#34;container&#34;&gt;
        &lt;div class=&#34;navbar-header header-logo&#34;&gt;
        	&lt;a href=&#34;{{ .Site.BaseURL }}&#34;&gt;{{ .Site.Title }}&lt;/a&gt;
@@ -13,7 &#43;16,10 @@
    &lt;/div&gt;
&lt;/nav&gt;
&lt;nav class=&#34;navbar-mobile&#34; id=&#34;nav-mobile&#34; style=&#34;display: none&#34;&gt;
&#43;    {{ if (and .IsPage (not .Params.notsb)) }}
&#43;        &lt;div class=&#34;top-scroll-bar&#34;&gt;&lt;/div&gt;
&#43;    {{ end }}
    &lt;div class=&#34;container&#34;&gt;
        &lt;div class=&#34;navbar-header&#34;&gt;
            &lt;div&gt;  &lt;a href=&#34;javascript:void(0);&#34; class=&#34;theme-switch&#34;&gt;&lt;i class=&#34;iconfont icon-sun&#34;&gt;&lt;/i&gt;&lt;/a&gt;&amp;nbsp;&lt;a href=&#34;{{.Site.BaseURL}}&#34;&gt;{{ .Site.Title }}&lt;/a&gt;&lt;/div&gt;
            &lt;div class=&#34;menu-toggle&#34;&gt;

```

然后在`assets/css/_cusstom.scss`文件中添加进度条样式

```scss
// 顶部阅读进度条
.top-scroll-bar {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 9999;
    display: none;
    width: 0;
    height: 3px;
    background: #ef3982;
  } 
```

之后新建一个 js 脚本文件 `assets/js/_custom.js` ，来控制进度条

```js
// 顶部阅读进度条
$(document).ready(function () {
    $(window).scroll(function(){
      $(&#34;.top-scroll-bar&#34;).attr(&#34;style&#34;, &#34;width: &#34; &#43; ($(this).scrollTop() / ($(document).height() - $(this).height()) * 100) &#43; &#34;%; display: block;&#34;);
    });
  }); 
```

最后， js 脚本引入到博客中，使其生效。

在 `/layouts/partials/js.html` 文件中添加以下内容，然后将 `$custom` 加入到变量 `$vendorscript` 中

```html
{{ $custom := resources.Get &#34;/js/_custom.js&#34; }}
```

重新编译后预览博客就可以看到阅读进度条了。

## 4. 添加侧边栏目录

原本LeaveIt主题不支持文章目录导航，可以按如下方法添加，但样式不是很合适

首先在`/assets/css/_custom.scss`添加侧边栏目录(toc)样式

```scss
// 添加toc栏
  .post-toc {
    position: absolute;
    width: 200px;
    margin-left: 800px;
    padding: 10px;
    word-wrap: break-word;
    box-sizing: border-box;

    .post-toc-title {
        margin: 0;
        font-weight: 400;
        text-transform: uppercase;
    }

    .post-toc-content {
        &amp;.always-active ul {
            display: block;
        }

        &gt;nav&gt;ul {
            margin: 10px 0;
        }

        ul {
            padding-left: 0;
            list-style: none;

            ul {
            padding-left: 15px;
            display: none;
            }

            .has-active &gt; ul {
                display: block;
            }
        }
    }

    a:hover {
        color: #c05b4d;
        -webkit-transform: scale(1.1);
        -ms-transform: scale(1.1);
        transform: scale(1.1);
    }

    a {
        display: block;
        line-height: 30px;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        -webkit-transition-duration: .2s;
        transition-duration: .2s;
        -webkit-transition-property: -webkit-transform;
        transition-property: -webkit-transform;
        transition-property: transform;
        transition-property: transform,-webkit-transform;
        -webkit-transition-timing-function: ease-out;
        transition-timing-function: ease-out;
    }
}
@media only screen and (max-width: 1224px) {
    .post-toc {
        display: none;
    }
} 
```

然后在 `layouts/partials/` 下新建 `toc.html` 文件，内容如下

```html
&lt;div class=&#34;post-toc&#34; id=&#34;post-toc&#34;&gt;
  &lt;h2 class=&#34;post-toc-title&#34;&gt;{{ T &#34;toc&#34; }}&lt;/h2&gt;
  {{ $globalAutoCollapseToc := .Site.Params.autoCollapseToc | default false }}
  &lt;div class=&#34;post-toc-content{{ if not (or .Params.autoCollapseToc (and $globalAutoCollapseToc (ne .Params.autoCollapseToc false))) }} always-active{{ end }}&#34;&gt;
    {{.TableOfContents}}
  &lt;/div&gt;
&lt;/div&gt;

&lt;script type=&#34;text/javascript&#34;&gt;
  window.onload = function () {
    var fix = $(&#39;.post-toc&#39;);
    var end = $(&#39;.post-comment&#39;);
    var fixTop = fix.offset().top, fixHeight = fix.height();
    var endTop, miss;
    var offsetTop = fix[0].offsetTop;
    $(window).scroll(function () {
      var docTop = Math.max(document.body.scrollTop, document.documentElement.scrollTop);
      if (end.length &gt; 0) {
        endTop = end.offset().top;
        miss = endTop - docTop - fixHeight;
      }
      if (fixTop &lt; docTop) {
        fix.css({ &#39;position&#39;: &#39;fixed&#39; });
        if ((end.length &gt; 0) &amp;&amp; (endTop &lt; (docTop &#43; fixHeight))) {
          fix.css({ top: miss });
        } else {
          fix.css({ top: 0 });
        }
      } else {
        fix.css({ &#39;position&#39;: &#39;absolute&#39; });
        fix.css({ top: offsetTop });
      }
    })
  }
&lt;/script&gt;  
```

在文章页的模板 `layouts/_default/single.html` 中`&lt;/header&gt;`标签后引入toc模板

```html
 {{ if ( .Site.Params.toc | default true ) }}
     {{ partial &#34;toc.html&#34; . }}
 {{ end }}
```

添加后重新使用hugo生成静态页面，只要文章有多级标题，就能在侧边栏看到导航目录

最后在站点配置文件`config.toml`中添加如下配置

```toml
toc = true                # 是否开启目录
autoCollapseToc = true   # Auto expand and collapse toc
```

## 5. 图片添加阴影

在 `assets/css/style.scss`中添加以下代码

```scss
// 图片阴影
.post-content {
	img {
        box-shadow: 0 0 15px 5px rgba(0, 0, 0, .28);
        max-width: 1080px;
	}
}
```



---

> Author:   
> URL: http://localhost:1313/2019/hugo-blog-theme-beautify/  

