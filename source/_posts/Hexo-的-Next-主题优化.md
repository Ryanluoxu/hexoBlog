---
title: Hexo 的 Next 主题优化
date: 2017-11-26 13:49:21
categories: 搭建博客
tags: [Hexo, Nexy, 博客, 主题优化]
---

**声明：本文为 ryanluoxu 原创文章，欢迎转载，请在明显位置注明出处。**

这篇博客用来记录和分享我对博客优化的过程，均为实际经历。欢迎纠正，与君共勉。

## 修改 Next 主题的 Scheme ##

Next 默认的风格是 Muse。现有的四个风格里，我最喜欢 Gemini。
因为此风格的博客首页里，每篇博客有明显的分割。菜单在左侧，方便访问时转到别的页面。  

**操作如下：**
1. 打开 D:\blog\themes\next\_config.yml
2. 找到 `Scheme Settings`
3. 去掉 `Gemini` 前面的 `#`。 
```
# Schemes
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini
```

## 添加访问统计 ##

开始时尝试用 LeanCloud，尝试数次无果，一直得不到访问数据。
改用 BuSuanZi，效果显著！

博客主页效果：

![博客主页下方访问量](/images/博客主页下方访问量.png)

<!--more-->

文章页面效果：

![文章页面访问量](/images/文章页面访问量.png)


**操作如下：**
1. 打开 D:\blog\themes\next\_config.yml
2. 找到 `busuanzi_count`
3. 如下修改： 
```
busuanzi_count:
  # count values only if the other configs are false
  enable: true	// 此处
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: <i class="fa fa-user"></i> Visitor // 此处
  site_uv_footer:
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: <i class="fa fa-eye"></i> Total Visit // 此处
  site_pv_footer:
  # custom pv span for one page only
  page_pv: true
  page_pv_header: <i class="fa fa-file-o"></i> View // 此处
  page_pv_footer:
```

## 添加头像 ##


**操作如下：**
1. 将头像照片 `头像1.jpg` 保存到 D:\blog\themes\next\source\images 路径下。
2. 打开 D:\blog\themes\next\_config.yml
3. 找到 `Sidebar Avatar`
4. 如下修改： 
```
# Sidebar Avatar
# in theme directory(source/images): /images/avatar.gif
# in site  directory(source/uploads): /uploads/avatar.gif
avatar: /images/avatar1.JPG
```

<a name="添加页面"></a>
## 添加 About 等页面 ##

前后效果对比：

![添加页面之前](/images/添加页面之前.png)

![添加页面之后](/images/添加页面之后.png)

**操作如下：**
1. 打开 Git Bash：
``` bash
cd /d/blog // 进入到 blog 所在文件夹
hexo new page "about" 
```
2. 打开 D:\blog\themes\next\_config.yml
3. 找到 `Menu Settings`
4. 如下修改： 
```
menu:
  home: / || home
  about: /about/ || user  // 此处
  #tags: /tags/ || tags
  #categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
```


## 侧边栏的分类和标签页面 ##

侧边栏有三个数字，分别对应文章，分类和标签。其中点击文章，可以到文章列表页面。但是分类和标签无法点击。
这里很有必要激活这个功能。 在此之前需要已经存在这两个页面。 参考[添加页面](#添加页面)进行添加。
```
hexo new page "categories"
hexo new page "tags"
```

**操作如下：**
1. 打开 D:\blog\themes\next\layout\_macro/sidebar.swig
2. 找到下面代码：
```
{% if site.categories.length > 0 %}
  {% set categoriesPageQuery = site.pages.find({type: 'categories'}, {lean: true}) %}
  {% set hasCategoriesPage = categoriesPageQuery.length > 0 %}
  <div class="site-state-item site-state-categories">
    {% if hasCategoriesPage %}<a href="{{ url_for(categoriesPageQuery[0].path) }}">{% endif %}
      <span class="site-state-item-count">{{ site.categories.length }}</span>
      <span class="site-state-item-name">{{ __('state.categories') }}</span>
    {% if hasCategoriesPage %}</a>{% endif %}
  </div>
{% endif %}

{% if site.tags.length > 0 %}
  {% set tagsPageQuery = site.pages.find({type: 'tags'}, {lean: true}) %}
  {% set hasTagsPage = tagsPageQuery.length > 0 %}
  <div class="site-state-item site-state-tags">
    {% if hasTagsPage %}<a href="{{ url_for(tagsPageQuery[0].path) }}">{% endif %}
      <span class="site-state-item-count">{{ site.tags.length }}</span>
      <span class="site-state-item-name">{{ __('state.tags') }}</span>
    {% if hasTagsPage %}</a>{% endif %}
  </div>
{% endif %}
```
3. 替换成下面代码：
```
{% if site.categories.length > 0 %}
  {% set categoriesPageQuery = site.pages.find({type: 'categories'}, {lean: true}) %}
  {% set hasCategoriesPage = categoriesPageQuery.length > 0 %}
  <div class="site-state-item site-state-categories">
    {% if hasCategoriesPage %}
	  <a href="{{ url_for(categoriesPageQuery[0].path) }}">
	{% else %}
      <a href="{{ url_for(theme.menu.categories).split('||')[0] | trim }}">
	{% endif %}
      <span class="site-state-item-count">{{ site.categories.length }}</span>
      <span class="site-state-item-name">{{ __('state.categories') }}</span>
    </a>
  </div>
{% endif %}

{% if site.tags.length > 0 %}
  {% set tagsPageQuery = site.pages.find({type: 'tags'}, {lean: true}) %}
  {% set hasTagsPage = tagsPageQuery.length > 0 %}
  <div class="site-state-item site-state-tags">
    {% if hasTagsPage %}
	  <a href="{{ url_for(tagsPageQuery[0].path) }}">
	{% else %}
      <a href="{{ url_for(theme.menu.tags).split('||')[0] | trim }}">  
	{% endif %}
      <span class="site-state-item-count">{{ site.tags.length }}</span>
      <span class="site-state-item-name">{{ __('state.tags') }}</span>
    </a>
  </div>
{% endif %}
```

没有深入研究，但应该是 `hasTagsPage` 没有实现，所以总是没有链接效果。所以给它加了一个 `else`   条件。就可以了。 


## 分类和标签页面的自动生成 categories & tags ##

一开始我自己手动添加了这两个页面的内容，后来无意看到了正确的打开方式：[主题配置](http://theme-next.iissnan.com/theme-settings.html)
很简单，分别加上 type 就可以了。

**分类页面：**
1. 打开 D:\blog\source\categories\index.md
2. 内容如下：
```
---
title: categories
date: 2017-11-26 18:38:13
type: "categories"
---
```

**标签页面：**
1. 打开 D:\blog\source\tags\index.md
2. 内容如下：
```
---
title: tags
date: 2017-11-26 18:38:13
type: "tags"
---
```

标签页面的效果特别好，对应文章数量多的标签会比较大。效果: [tags页面](https://ryanluoxu.github.io/tags/)


## 设置侧边栏社交链接 ##

官方文档：[设置侧边栏社交链接](https://github.com/iissnan/hexo-theme-next/wiki/%E8%AE%BE%E7%BD%AE%E4%BE%A7%E8%BE%B9%E6%A0%8F%E7%A4%BE%E4%BA%A4%E9%93%BE%E6%8E%A5)

但是内容好像没有更新。配置文件已经有，不需要新增。

**操作如下：**

1. 打开 D:\blog\themes\next\_config.yml
2. 找到 `Social Links.`
3. 修改如下：
```
social:
  GitHub: https://github.com/Ryanluoxu || github
  Linkedin: https://www.linkedin.com/in/luo-xu-ryan-675a8041/ ||  linkedin
  ZhiHu: https://www.zhihu.com/people/luojiuri/activities || 
  #StackOverflow: https://stackoverflow.com/users/7640451/ryan-l || stack-overflow
  E-Mail: mailto:luoxu2011@gmail.com || envelope
  #右键复制: mailto:luoxu2011@gmail.com || envelope
  #Google: https://plus.google.com/yourname || google
  #Twitter: https://twitter.com/yourname || twitter
  #FB Page: https://www.facebook.com/yourname || facebook
  #VK Group: https://vk.com/yourname || vk
  #YouTube: https://youtube.com/yourname || youtube
  #Instagram: https://instagram.com/yourname || instagram
  #Skype: skype:yourname?call|chat || skype

social_icons:
  enable: true
  icons_only: false
  transition: false
  GitHub: github
  Linkedin: linkedin 
```

## 设置侧边栏社交链接 ##

参考 [Hexo+Next主题优化](https://zhuanlan.zhihu.com/p/30836436) 的 10. 自定义文章底部版权声明

## 参考 ##

[NexT主题个性化修改与调试方案](http://blog.junyu.io/posts/0009-hexo-next-theme-modify.html)

