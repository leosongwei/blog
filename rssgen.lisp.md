rssgen.lisp
-----------

把`rssgen.lisp`移到了一个单独的[repo](https://github.com/leosongwei/rssgen.lisp)里面。现在它已经不仅仅是一个生成rss xml的东西了，变得有点像JekyII那样的博客生成器，可以生成首页、标签云等东西。

写`rssgen.lisp`的主要原因就是因为JekyII那样的东西看起来太麻烦了，所以并不想安装它们。而且，Github的markdown支持显得相当不错，就让我有了直接用Github来做博客的想法。

本来我的需求就很简单：用markdown写博客。然而那些静态网站生成工具看起来太复杂了，配置文件长而吓人，所以我就自己造了一个轮子，看起来还不错。你看，rssgen.lisp不到500行，远远小于那些静态网站生成工具以及它们创建的垃圾文件。然而说起来其实并不轻量级，因为用了QuickLisp里面的库。
