---
title: "页面设置"
date: 2021-09-14T13:27:08+08:00
draft: true
hiddenFromHomePage: true
---

{{< admonition >}}
**不是所有**的以下前置参数都必须在你的每篇文章中设置.
只有在文章的参数和你的 [网站设置](../theme-documentation-basics#site-configuration) 中的 `page` 部分不一致时才有必要这么做.
{{< /admonition >}}

这是一个前置参数例子:

```yaml
---
title: "我的第一篇文章"
subtitle: ""
date: 2020-03-04T15:58:26+08:00
lastmod: 2020-03-04T15:58:26+08:00
draft: true
authors: []
description: ""
license: ""
images: []

tags: []
categories: []
series: []
series_weight: 1
seriesNavigation: true
featuredImage: ""
featuredImagePreview: ""

hiddenFromHomePage: false
hiddenFromSearch: false
twemoji: false
lightgallery: true
ruby: true
fraction: true
fontawesome: true
linkToMarkdown: true
linkToSource: false
linkToEdit: false
linkToReport: false
rssFullText: false

toc:
  enable: true
  auto: true
code:
  copy: true
  # ...
table:
  sort: true
  # ...
math:
  enable: true
  # ...
mapbox:
  accessToken: ""
  # ...
share:
  enable: true
  # ...
comment:
  enable: true
  # ...
library:
  css:
    # someCSS = "some.css"
    # 位于 "assets/"
    # 或者
    # someCSS = "https://cdn.example.com/some.css"
  js:
    # someJS = "some.js"
    # 位于 "assets/"
    # 或者
    # someJS = "https://cdn.example.com/some.js"
seo:
  images: []
  # ...
outdatedArticleReminder:
  enable: false
  # ...
sponsor:
  enable: false
  # ...
---
```

* **title**: 文章标题.
* **subtitle**: {{< version 0.2.0 >}} 文章副标题.
* **date**: 这篇文章创建的日期时间. 它通常是从文章的前置参数中的 `date` 字段获取的, 但是也可以在 [网站配置](../theme-documentation-basics#site-configuration) 中设置.
* **lastmod**: 上次修改内容的日期时间.
* **draft**: 如果设为 `true`, 除非 `hugo` 命令使用了 `--buildDrafts`/`-D` 参数, 这篇文章不会被渲染.
* **authors**: {{< version 0.2.12 changed >}} 文章作者.
* **description**: 文章内容的描述.
* **license**: 这篇文章特殊的许可.
* **images**: 页面图片, 用于 Open Graph 和 Twitter Cards.

* **tags**: 文章的标签.
* **categories**: 文章所属的类别.
* **series**: {{< version 0.2.12 >}} 文章所属的系列.
* **series_weight**: {{< version 0.2.13 >}} 自定义文章在系列中的[位置](https://gohugo.io/content-management/taxonomies/#order-taxonomies).
* **seriesNavigation**: {{< version 0.2.13 >}} 是否使用系列导航.
* **featuredImage**: 文章的特色图片.
* **featuredImagePreview**: 用在主页预览的文章特色图片.

* **hiddenFromHomePage**: 如果设为 `true`, 这篇文章将不会显示在主页上.
* **hiddenFromSearch**: {{< version 0.2.0 >}} 如果设为 `true`, 这篇文章将不会显示在搜索结果中.
* **twemoji**: {{< version 0.2.0 >}} 如果设为 `true`, 这篇文章会使用 twemoji.
* **lightgallery**: 如果设为 `true`, 文章中的图片将可以按照画廊形式呈现.
* **ruby**: {{< version 0.2.0 >}} 如果设为 `true`, 这篇文章会使用 [上标注释扩展语法](#ruby).
* **fraction**: {{< version 0.2.0 >}} 如果设为 `true`, 这篇文章会使用 [分数扩展语法](#fraction).
* **fontawesome**: {{< version 0.2.0 >}} 如果设为 `true`, 这篇文章会使用 [Font Awesome 扩展语法](#fontawesome).
* **linkToMarkdown**: 如果设为 `true`, 内容的页脚将显示指向原始 Markdown 文件的链接.
* **linkToSource**: {{< version 0.2.14 >}} 如果设为 `false`, 则关闭页脚 **view source** 的链接. 你可以将其设置为一个指向文章原始文件的链接. 使用魔法变量 `{path}` 来获取文章的相对路径, 这篇文章的 `{path}` 是 `posts/theme-documentation-content/index.en.md`.
* **linkToEdit**:{{< version 0.2.13 >}} 如果设为 `false`, 则关闭页脚 **编辑此页** 的链接. 你可以将其设置为一个用于编辑这个页面的链接. 使用魔法变量 `{path}` 来获取这篇文章的相对路径, 这篇文章的 `{path}` 是 `posts/theme-documentation-content/index.zh-cn.md`.
* **linkToReport**: {{< version 0.2.14 >}} 如果设为 `false`, 则关闭页脚 **报告问题** 的链接. 你可以将其设置为一个用于报告此页面中错误的链接. 使用魔法变量 `{path}` 来获取文章的相对路径, 这篇文章的 `{path}` 是 `posts/theme-documentation-content/index.en.md`, 使用 `{title}` 来获取文章的标题, 这篇文章的 `{title}` 为 `Theme Documentation - Content`, 使用 `{url}` 来获取文章的链接, 这篇文章的 `{url}` 为 `https://hugodoit.pages.dev/theme-documentation-content/`.
* **rssFullText**: {{< version 0.2.4 >}} 如果设为 `true`, 在 RSS 中将会显示全文内容.
* **pageStyle**: {{< version 0.2.11 >}} 调整页面样式, 可选择"normal"或"wide".
* **license**: {{< version 0.2.14 >}} 许可协议信息 (支持 HTML 格式).

* **toc**: {{< version 0.2.9 changed >}} 和 [网站配置](../theme-documentation-basics#site-configuration) 中的 `params.page.toc` 部分相同.
* **code**: {{< version 0.2.0 >}} 和 [网站配置](../theme-documentation-basics#site-configuration) 中的 `params.page.code` 部分相同.
* **table**: {{< version 0.2.14 >}} 和 [网站配置](../theme-documentation-basics#site-configuration) 中的 `params.page.table` 部分相同.
* **math**: {{< version 0.2.0 changed >}} 和 [网站配置](../theme-documentation-basics#site-configuration) 中的 `params.page.math` 部分相同.
* **mapbox**: {{< version 0.2.0 >}} 和 [网站配置](../theme-documentation-basics#site-configuration) 中的 `params.page.mapbox` 部分相同.
* **share**: 和 [网站配置](../theme-documentation-basics#site-configuration) 中的 `params.page.share` 部分相同.
* **comment**: {{< version 0.2.0 changed >}} 和 [网站配置](../theme-documentation-basics#site-configuration) 中的 `params.page.comment` 部分相同.
* **library**: {{< version 0.2.7 >}} 和 [网站配置](../theme-documentation-basics#site-configuration) 中的 `params.page.library` 部分相同.
* **seo**: {{< version 0.2.10 >}} 和 [网站配置](../theme-documentation-basics#site-configuration) 中的 `params.page.seo` 部分相同.
* **outdatedArticleReminder**: {{< version 0.2.13 >}} 和 [网站配置](../theme-documentation-basics#site-configuration) 中的 `params.page.outdatedArticleReminder` 部分相同.
* **sponsor**: {{< version 0.2.13 >}} 和 [网站配置](../theme-documentation-basics#site-configuration) 中的 `params.sponsor` 部分相同.

{{< admonition tip >}}
{{< version 0.2.10 >}}

**featuredImage** 和 **featuredImagePreview** 支持[本地资源引用](#contents-organization)的完整用法.

如果带有在前置参数中设置了 `name: featured-image` 或 `name: featured-image-preview` 属性的页面资源,
没有必要在设置 `featuredImage` 或 `featuredImagePreview`:

```yaml
resources:
- name: featured-image
  src: featured-image.jpg
- name: featured-image-preview
  src: featured-image-preview.jpg
```
{{< /admonition >}}
