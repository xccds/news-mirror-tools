---
name: people-daily-history
description: |
  获取人民网（www.people.com.cn）和人民日报图文数据库（1946-2026）的历史新闻标题与正文。
  提供：人民网首页/频道滚动新闻列表、人民日报每日20版版面文章索引、文章完整正文、PDF原文下载链接。
  适用：查询人民网某一天的历史新闻标题、获取人民日报往期版面文章列表、抓取某篇新闻的完整正文、批量采集某时间段内的新闻内容。
  不适用：实时新闻推送、视频新闻、央视新闻联播文字稿、非人民日报系媒体内容。
---

# 人民网历史信息获取

## 当天新闻

| 用途 | URL |
|------|-----|
| 首页 | `http://www.people.com.cn` |
| 今日头条一览 | `http://www.people.com.cn/GB/59476/index.html` |

首页底部有"人民网首页往日回顾"入口。

## 频道滚动新闻（可翻页回溯）

每个频道按页码回溯历史：

```
经济·科技: http://finance.people.com.cn/GB/70846/index.html → index2.html → index{n}.html
时政:      http://politics.people.com.cn
社会:      http://society.people.com.cn
国际:      http://world.people.com.cn
军事:      http://military.people.com.cn
教育:      http://edu.people.com.cn
健康:      http://health.people.com.cn
文旅:      http://ent.people.com.cn
```

每条新闻附带日期（如 `2026-05-14`）。

## 人民日报图文数据库（1946-2026）

入口：`http://paper.people.com.cn/rmrb/pc/layout/index.html`

### 版面URL
```
http://paper.people.com.cn/rmrb/pc/layout/{YYYYMM}/{DD}/node_{版号}.html
```
每期约20版。每个版面的 `.news-list` 包含该版所有文章标题和链接。

### 文章正文
```
http://paper.people.com.cn/rmrb/pc/content/{YYYYMM}/{DD}/content_{id}.html
```

### 日期导航
支持日历选择器（2006-2050年），直接改URL中的日期即可跳转。

## 获取方法

### 渠道A：人民网文章
URL：`http://{频道}.people.com.cn/n1/{YYYYMMDD}/c{分类号}-{文章ID}.html`
webfetch 抓取即可获取完整正文（标题、来源、日期、正文、责编）。

### 渠道B：人民日报数据库
1. 访问 `node_XX.html` 获取该版文章列表
2. 从列表提取 `content_{id}.html` 链接
3. 访问正文URL获取全文

## 注意事项
- 获取正文用 text 格式，获取链接用 html 格式
- 无需登录，反爬限制较低
