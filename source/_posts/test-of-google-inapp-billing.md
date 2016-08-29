---
title: 关于google In-app Billing的测试注意点
date: 2016-08-29 11:52:28
tags:
  - google In-app Billing
categories: 技术
---

## 介绍
Google In-app Billing是Android app调用google play去进行充值支付的一个模块。具体的介绍请参看[官方文档](https://developer.android.com/google/play/billing/index.html)

## google In-app Billing的测试购买
点击[这里](https://developer.android.com/google/play/billing/billing_testing.html)查看官方文档（要看英文版，中文版坑爹，翻译错误）

需要注意的几点如下：
通常用于google测试需要将apk发布到alpha/beta渠道。一定要注意需要在发布状态下才能够进行测试，草稿状态下是测试不了的。

例如将引用是发布到BETA渠道，配置好①商品详情，②内容分级，③定价和分发范围，④应用内商品
最后，⑤上传apk（注意apk不能用debug签名，还需要用zipalign处理[注1]），上传完apk之后，可以选择“封闭式BETA版测试”，在里面添加测试人员账号列表。OK之后点击发布。

<!-- more -->

![上传apk](/images/uploadapk.png)

一般等待一段时间之后（时间有长有短，大概半个小时左右），查看是不是已经发布完成。如果成功发布，刚刚添加的测试人员账号，可以在手机的浏览器输入“测试的链接”（例如上面截图中的应用的测试链接就是：https://play.google.com/apps/testing/org.MyTest.game），
授权成为测试人员之后就可以开始测试了。（这一步很关键，不然在购买商品的时候老是会弹出“需要验证身份”的错误）

这里有个小技巧，就是我们可以上传一个空的apk上去，这个空的apk的包名，版本号，签名跟我们要测试的apk只要保持一致就行。这样，我们在自己手机上直接安装我们需要测试的apk就可以进行测试，而且如果有问题，我们可以直接修改代码再重新生成apk，并再次安装到手机上进行测试。

## 说明
注1：android-sdk里面的build tools就有zipalign.exe工具，指令是：zipalign -f 4 src_apk dest_apk
