---
title: "PHP 抖音视频去水印"
date: 2020-10-12 10:35:39
lastmod: 2022-06-07T10:16:26+08:00
draft: false
description: "r抖音视频去水印的实现原理和 php 的实现方式，附各种视频去水印的 composer 扩展包"
tags: ["去水印"]
featured_image: "douyin.jpg"
categories: ["PHP"]
series: ["codding"]
resources:
- name: featured-image
  src: douyin.jpg
- name: featured-image-preview
  src: douyin.jpg
---

## 原理

### 播放地址
`https://aweme.snssdk.com/aweme/v1/playwm/?video_id=...`
### 无水印地址
`https://aweme.snssdk.com/aweme/v1/play/?video_id=...`
### 区别
参数 `paly` / `playwm`
wm: water mark 的缩写
### 注意
抖音对 PC 做了限制，现在只有模拟手机发送请求才可以实现无水印播放。

## 代码简单实现

```php
/**
 * 返回无水印播放地址 apiDAta
 * @desc 使用方法 域名url=视频的分享地址
 */
function getApiDAta()
{
    // 通过 url 获取到 解析后的地址
    $url = $_GET['url'];
    $res = curl_http_exec($url);
    preg_match('/href="(.*?)">Found/', $res, $matches);
    $url_share = $matches[1];
    // 根据解析后的地址获取到 item_ids
    preg_match('/video\/(.*?)\//', $url_share, $matches);
    $item_ids = $matches[1];
    // 获取视频API数据
    $apiDAta = json_decode(file_get_contents('https://www.iesdouyin.com/web/api/v2/aweme/iteminfo/?item_ids=' . $item_ids), true)['item_list'][0];
    // 获取播放地址
    $url_play = $apiDAta['video']['play_addr']['url_list'][0];
    // 根据播放地址 获取到无水印播放地址
    // 二次解析视频
    $url_play_remove_water_mark = str_replace('playwm', 'play', $url_play);
    preg_match('/href="(.*?)">Found/', curl_http_exec($url_play_remove_water_mark), $matches);
    $apiDAta['video']['play_addr']['url_list'][0] = $matches[1];

    return $apiDAta;
}

/**
 * 获取地址中的内容
 * @param $url
 * @return bool|string
 */
function curl_http_exec($url)
{
    // $Header = array("User-Agent:Mozilla/5.0 (iPhone; CPU iPhone OS 11_0 like Mac OS X) AppleWebKit/604.1.38 (KHTML, like Gecko) Version/11.0 Mobile/15A372 Safari/604.1");
    $Header = array("User-Agent:Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1");
    $con = curl_init((string)$url);
    curl_setopt($con, CURLOPT_HEADER, false); # 启用时会将头文件的信息作为数据流输出。
    curl_setopt($con, CURLOPT_SSL_VERIFYPEER, false); # 禁用后cURL将终止从服务端进行验证。
    curl_setopt($con, CURLOPT_RETURNTRANSFER, true); # 将curl_exec()获取的信息以文件流的形式返回，而不是直接输出。
    curl_setopt($con, CURLOPT_HTTPHEADER, $Header); # 用来设置HTTP头字段的数组
    curl_setopt($con, CURLOPT_TIMEOUT, 5000); # 设置cURL允许执行的最长秒数。
    $result = curl_exec($con); # 抓取URL并把它传递给浏览器
    curl_close($con); # //关闭cURL资源，并且释放系统资源
    return $result;
}
```

## 推荐 composer 扩展包

1. [smalls/video-tools](https://github.com/SMalls0098/video-tools)：短视频的拓展包，集成各大短视频的去水印功能