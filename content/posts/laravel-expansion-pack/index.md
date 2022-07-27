---
title: "(2020/9/11 更新) 常用 Laravel 开发扩展包"
date: 2020-09-08 17:20:17
lastmod: 2022-06-07T10:16:26+08:00
draft: false
description: "日常使用的扩展我经常容易忘记，所以写这篇文章来记录常用的包，看扩展的流行程度和替代方案，会删除或添加扩展，会保持更新。"
tags: [Larave, Laradock]
featured_image: "composer.jpg"
categories: [PHP, Laravel]
comment : true
disableToC: false
---

# 前言
日常使用的扩展我经常容易忘记，所以写这篇文章来记录常用的包，看扩展的流行程度和替代方案，会删除或添加扩展，会保持更新。

# 扩展列表

## 开发者工具

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |
| 1     | [barryvdh/laravel-ide-helper](https://github.com/barryvdh/laravel-ide-helper) | 代码提示及补全工具 |[Laravel 超好用代码提示工具 Laravel IDE Helper](https://learnku.com/articles/10172/laravel-super-good-code-prompt-tool-laravel-ide-helper)|
| 2     | [beyondcode/laravel-dump-server](https://github.com/beyondcode/laravel-dump-server) | 将Symfony Var-Dump 服务器带到 Laravel |[官方文档](https://beyondco.de/docs/laravel-dump-server/installation)|
| 3     | [overtrue/laravel-query-logger](https://github.com/overtrue/laravel-query-logger) |  用于记录Laravel应用程序的所有查询 |[官方文档](https://github.com/overtrue/laravel-query-logger)|

## 测试 & 调试

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |
| 1     | [overtrue/phplint](https://github.com/overtrue/phplint) |  PHP 语法错误检测工具 |[官方文档](https://github.com/overtrue/phplint)|



## 授权 & 认证

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |
| 1     | [laravel/passport](https://github.com/laravel/passport) |  简单易用的OAuth2服务器和API身份验证 |[官方文档](https://learnku.com/docs/laravel/8.x/passport/9420) <br> [学院君的 Passport 系列](https://xueyuanjun.com/post/9745.html)|
| 2     | [laravel/sanctum](https://github.com/laravel/sanctum) | 为 SPA 、移动应用程序和简单的、基于令牌的 API 提供轻量级身份验证系统 |[官方文档](https://learnku.com/docs/laravel/8.x/sanctum/9421) <br> [使用 Laravel Sanctum 作为 API 认证来构建 Vue.js 应用](https://learnku.com/laravel/t/43077)|
| 3     | [laravel/socialite](https://github.com/laravel/socialite) | Socialite 社会化登录 |[官方文档](https://learnku.com/docs/laravel/8.x/socialite/9423) <br> [安装配置 Laravel Socialite 并实现基于 Github 的用户认证](https://xueyuanjun.com/post/9499)|
| 4     | [overtrue/socialite](https://github.com/overtrue/socialite) | OAuth2 认证工具 |[官方文档](https://github.com/overtrue/socialite)|
| 5     | [socialiteproviders/xxx](https://github.com/SocialiteProviders/Providers) | 提供各种身份验证 |[官方文档](https://socialiteproviders.com/)|

## 其它有用的利器

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |
| 1     | [gregwar/captcha](https://github.com/Gregwar/Captcha) |  验证码 |[官方文档](https://github.com/Gregwar/Captcha)|
| 2     | [elasticsearch/elasticsearch](https://github.com/elastic/elasticsearch-php) |  Elasticsearch |[中文文档](https://learnku.com/docs/elasticsearch-php/6.0)|


## 媒体 & 文档管理

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |


## 集成 JavaScript

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |


## 数据库/ORM/迁移/填充

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |


## 搜索

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |
| 1     | [vanry/laravel-scout-tntsearch](https://github.com/vanry/laravel-scout-tntsearch) |  TNTSearch |[laravel下TNTSearch+jieba-php实现中文全文搜索](https://baijunyao.com/article/154)|
| 2     | [baijunyao/laravel-scout-elasticsearch](https://github.com/baijunyao/laravel-scout-elasticsearch/tree/v3.0.1) |  TNTSearch |[laravel下elasticsearch+analysis-ik实现中文全文搜索](https://baijunyao.com/article/156)|

## API

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |
| 1     | [tymon/jwt-auth](https://github.com/tymondesigns/jwt-auth) | 常用于实现API用户认证 |[JWT 超详细分析](https://learnku.com/articles/17883) <br>[官方文档](https://jwt-auth.readthedocs.io/en/develop/) <br>[Laravel JWT 多表多用户登录](https://learnku.com/articles/30342) <br> [Laravel jwt 多表（多用户端）验证隔离](https://learnku.com/articles/28881)|


## 后台模板

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |
| 1     | [encore/laravel-admin](https://github.com/z-song/laravel-admin) |  在十分钟内构建一个功能齐全的管理后台 |[官方文档](https://laravel-admin.org/)|
| 2     | [dcat/laravel-admin](https://github.com/jqhph/dcat-admin) |  基于laravel-admin二次开发而成的后台系统构建工具 |[官方文档](http://www.dcatadmin.com/)|


## 任务/命令/调度

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |


## 电子商务

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |


## 支付

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |
| 1     | [yansongda/laravel-pay](https://github.com/yansongda/laravel-pay) |  最优雅的 Alipay 和 WeChat 的支付 SDK 扩展包 |[官方文档](https://pay.yanda.net.cn/docs/2.x/)|

## 队列 & 消息

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |


## 性能优化

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |


## 本地化

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |
| 1     | [overtrue/laravel-lang](https://github.com/overtrue/laravel-lang) | 多语言包 |[laravel 项目语言包汉化](https://blog.csdn.net/smm1123kkk/article/details/93061976)|
| 2     | [overtrue/laravel-pinyin](https://github.com/overtrue/laravel-pinyin) | 中文转拼音工具 |[官方文档](https://github.com/overtrue/pinyin)|


## 第三方服务集成

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |
| 1     | [overtrue/laravel-wechat](https://github.com/overtrue/laravel-wechat) | 微信 SDK |[官方文档](https://www.easywechat.com/docs)|
| 2     | [overtrue/easy-sms](https://github.com/overtrue/easy-sms) | 一款满足你的多种发送需求的短信发送组件 |[Laravel 短信发送组件 - easy-sms](https://learnku.com/articles/24063)|



## 本地开发

| 序号   | 名称                        | 描述             | 用例链接   |
| ----  | ---------                   | ----             | ----      |
| 1     | [LaraDock](https://github.com/LaraDock/laradock) | Laradock 是为 Docker 提供的完整 PHP 本地开发环境 |[官方文档](http://laradock.io/documentation/) <br> [在 Mac/Windows 系统中使用 Laradock 搭建基于 Docker 的 Laravel 开发环境](https://xueyuanjun.com/post/9608)|








