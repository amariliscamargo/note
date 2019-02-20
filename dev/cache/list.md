---
categories: [dev, project]
date: '2019-02-14 15:57:52'
tags: [dev, project]
title: 部分项目列表
titleen: Partial list of items
updated: '2019-02-19 12:35:38'
...
---
# 部分项目列表
<!-- MarkdownTOC -->

- [网站](#%E7%BD%91%E7%AB%99)
- [公众号,小程序,Hybrid App,和内网应用](#%E5%85%AC%E4%BC%97%E5%8F%B7%E5%B0%8F%E7%A8%8B%E5%BA%8Fhybrid-app%E5%92%8C%E5%86%85%E7%BD%91%E5%BA%94%E7%94%A8)

<!-- /MarkdownTOC -->

<a id="%E7%BD%91%E7%AB%99"></a>
## 网站

-   [八达岭奥特莱斯官网](http://www.badaling-outlets.com/)
-   [蓝光迅媒科技有限公司](http://www.blovemedia.com/)
-   [河南文艺出版社名人传记](http://mrzj.hnwycbs.com/)
-   [DPS5 视频发布工具](http://shuhuashiyu.hnmscbs.com)
-   [dps5 产品官网](http://dps5.cn/)

<a id="%E5%85%AC%E4%BC%97%E5%8F%B7%E5%B0%8F%E7%A8%8B%E5%BA%8Fhybrid-app%E5%92%8C%E5%86%85%E7%BD%91%E5%BA%94%E7%94%A8"></a>
## 公众号,小程序,Hybrid App,和内网应用

-   陕西省图书馆 (图书借阅查询) (微信)
-   河南大学微信图书馆 (SirsiDynix API) (微信)
-   我是导游 (旅游教育出版社 试卷书籍阅读) (微信, 混合应用)
-   比特出版 (公司内部开发的简化项目开发应用)
-   三更青年 (菜鸟在线网,视频培训) (小程序)
-   教材核检工具 (上海中文在线, 筛选统计数据,展示并导出为 excel world) (内网使用)
-   书籍荐购工具 南投市立图书馆/国立台南艺术大学图书馆 (北京大学图书馆 Demo) (内网使用)
-   天行美购 (电视购物) (微信)

Laravel 5.5 中文文档
Elasticsearch
微信支付
mozilla pdf.js


项目地址: http://mrzj.hnwycbs.com
名人传记数据库,将河南文艺出版社的电子书刊资源,以机构会员付费的方式进行在线检索和浏览;
总结: 
  此项目的工期比较紧凑, 适合使用"敏捷开发"的方式进行软件开发;
  在后台 PHP 框架上, 选用 Laravel 5.5 框架进行开发, 因为它支持 Composer 依赖管理工具,并且在高级开发者中比较流行,拥有很多第三方类库,在之后网站的"支付","分享"等环节可以很快速的使用第三方开源类库快速开发,减少后期测试和修改bug的时间;
  在前台 javaScript 框架上, 选用 jQuery 1.8 进行开发, 因为团队成员都对 jQuery 最熟悉.1.8版本当前使用最为广泛,接口比较稳定.并且网站的前台页面比较少,业务逻辑比较简单不需要更复杂的框架;
  在数据库的选用上用户行为记录使用 MySQL 数据库; 书籍资源数据库(SQL Server 2012)和全文检索(Elasticsearch)模块由开发 Java 的同事负责, 我们之间使用 "Webservice" 技术进行数据的相互交换和集成;
  网站功能方面: PDF文件阅读器,集成的 "mozilla pdf.js", 交互方式等根据客户需求进行修改; 微信支付方面,使用开源且稳定的"easywechat"类库进行快速开发;因为是PC网站场景,所以选用的是在网站中展示二维码，用户扫描二维码后在微信中完成支付;分享功能使用开源的第三方集成类库进行qq,微博,微信等分享;
在此项目中,我根据不同的业务需求和特点,选择不同的开发方式,将业务拆分为多个独立的小模块,不重复造轮子,分工合作,快速且有质量的交付;
