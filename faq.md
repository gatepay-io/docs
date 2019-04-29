---
title: 问题
type: docs
order: 2
---

如果你在使用GatePay收款中出现了问题可以在[https://github.com/gatepay-io/docs/issues](https://github.com/gatepay-io/docs/issues) 提交问题。

## 微信可以想支付宝一样，唤起APP完成支付吗？

不行，不过微信支付在微信浏览器里面可以长按二维码识别。

## 用「GatePay 个人收款」收款安全吗？

肯定的，用户支付的钱款不经过 GatePay 而是直接到你的微信和支付宝钱包，即时到账，绝对安全。

## 「GatePay 个人收款」稳定吗？会不会掉单？

GatePay 用了严密的支付检测技术和二维码调度算法且服务器在国内，稳定运行已久，无一漏单。

## 安装 GatePay App 的手机需要 root 吗？

不用。

## 为什么要安装App呢，如果手机没电或者没网会怎样？

「GatePay 个人收款」的原理就是获取微信、支付宝的二维码到账通知，通过在 Android 手机上面安装「GatePay 个人收款」App 可以获取到账通知，从而实现支付成功回调。如果手机没电或者没网络，那么手机就无法收到支付到账通知，用户扫码支付成功后就没办法回调你的服务接口了。

## 我用于收款的微信或支付宝账号会不会有什么风险？

没有风险，这个支付过程和平常扫码支付一样，合理合规合法。

## 可以自定义支付页面吗？

可以的。支付接口请求得到的支付链接 通过设置 format=json 参数可以返回 json 格式的支付数据，你可以自己渲染支付页面。

## 你们平台如何扣费呢？

每月的套餐费用需要提前升级或者续费，平台是零手续费，使用期间不收费。

## 订单未支付成功会扣除手续费吗？

平台是零手续费，除了套餐费用，使用期间不收费。

## 用户已经扫码付款，但是我没有收到回调是什么情况呢？

有多种可能。用户支付后到你的应用收到回调通知，大概有几秒的延迟，如果 GatePay 调用你的回调通知接口失败，GatePay 会连续通知三次，每次间隔一分钟。还有可能是订单已经过期后用户才付款，这也会导致不会收到回调通知。

## 支付二维码过期后用户转账付款，怎么办呢？

你可以在后台的订单管理页面，找到这个用户对应的订单，然后点击「我已收款」按钮，Gatepay.io 会调用你的回调接口通知这个订单已经收款。

## 支持支付宝官方收钱码吗，提现免费的那种？

支持的，GatePay 支持支付宝普通收款码和官方收钱码。

## 用 java 调用接口怎么会提示证书出错呢？

可能是 jdk 对 let's encrypt ssl 证书的支持问题，把 API 的 https 换成 http 即可。

## 微信收到款后在通知栏怎么没有金额呢，只有到账通知？

应该是没有开启 “微信收款语音播报” 在微信「我」-「钱包」-「收付款」- 「二维码收款」- 点击右上角三个点 开启收款到账语音提醒。

## GatePay 收款有限额吗？

没有。

## 上传收款二维码数量有限制吗？

没有数量限制。每天最多上传5w张，超过5w张可以发给客服批量导入。

## 支持企业微信买单二维码吗？

支持。

**#### 方法一： 修改 composer 的全局配置文件（推荐方式）**

打开命令行窗口并执行如下命令：

```
composer config -g repo.packagist composer https://packagist.laravel-china.org
```

**#### 方法二： 修改当前项目的 composer.json 配置文件：**

打开命令行窗口，进入你的项目的根目录（也就是 composer.json 文件所在目录），执行如下命令：

```
composer config repo.packagist composer https://packagist.laravel-china.org
```

感谢：https://packagist.laravel-china.org


## 如何修改或禁用左侧菜单栏的角标

FastAdmin后台左侧菜单栏有彩色的小角标，这一般用于通知和提醒操作，在后台开发时是非常方便的一个小功能，如何修改和禁用它呢？
找到`/application/admin/controller/Index.php`中的index方法，其中有一段

```php
$menulist = $this->auth->getSidebar([
	'dashboard'  => 'hot',
	'auth'       => ['new', 'red', 'badge'],
	'auth/admin' => 12,
	'auth/rule'  => 4,
	'general'    => ['18', 'purple'],
]);
```

数组的键名是对应的左侧菜单栏的相对链接
数组的键值是需要显示的文字或数字，可以传字符串或数组

1. 如果是字符串，则角标的颜色是按照`'red', 'green', 'yellow', 'blue', 'teal', 'orange', 'purple'`的方式进行循环的。
2. 如果是数组，这三个值分别表示：[显示的文字, 颜色，展现方式(badge或label)]

如果需要删除这个小角标，则可以直接到数组置为空即可

在这里仅仅是PHP端操作小角标的方式，在JS端同样可以进行相应的操作
在你的模块中可以调用

```js
top.window.Backend.api.sidebar({
	'auth/admin':44
});
```

具体使用方法同PHP端相同
如何动态的在JS中移除一个小角标呢，采用以下的方法即可

```js
top.window.Backend.api.sidebar({
	'auth/admin':0
});
```

## 后台上传文件时提示HTTP Error.(code:-200)错误

在后台上传文件时如果遇到-200错误，首先请开启调试模式，然后请使用谷歌浏览器的开发者工具，按F12，切换到`Network`，看具体的错误信息。

## 在Windows下如何压缩打包JS和CSS

在FastAdmin中压缩打包JS和CSS文件需要NodeJS的支持
在Windows下需要手动配置Node的可执行文件,请修改`application/admin/command/Min.php`中`$nodeExec`的值
如你的Node可执行文件是`C:/Program Files/nodejs/node.exe`，则请配置`$nodeExec = '"C:/Program Files/nodejs/node.exe"'`;



## 提示你所浏览的页面暂时无法访问

如果我们在FastAdmin开发过程中遇到此错误，说明我们`application/config.php`中的`app_debug`是关闭的，必须开启`app_debug`为`true`才可以显示出详细的错误信息。如果开启`app_debug`仍然显示不出详细错误，请确保`php.ini`中的`display_error`为开启状态。




## 提示未知的数据格式或网络错误

很多时候都有可能遇到提示未知的数据格式或网络错误这个提示，产生这个错误的原因一般来说都是服务端报错，导致返回的数据不是JSON格式或直接未返回，如下图

![](https://cdn.forum.fastadmin.net/uploads/201706/02/0f650de53f0ee93ddfd658f731027d43)

准备工作：首先确保你的FastAdmin开启了调试模式`application/config.php`中的`app_debug`置为`true`
两种定位错误的方法：

1. 使用Chrome浏览器，打开开发者工具，选中`Network(网络)`选项卡,刷新一下页面或重新请求一次，定位到我们请求的URL，点击然后在`Preview`即可看到错误信息
2. 直接查看`runtime/log`目录下的错误日志

修复错误后再重试即可

FastAdmin建议运行在PHP5.5及以上版本，因此如果提示网络错误请检查你的PHP是否低于该版本

## 安装时提示无法写入application/database.php

造成此问题的原因通常有几下两种情况

1. `application/database.php`文件没有写入权限，请先查看你的apache或nginx的运行用户，然后修改文件的所有者，再添加上写入的权限，通常情况下需要执行以下命令：

   ```
   cd /yourpath/fastadmin/
   chown www-data:www-data ./ -R
   chmod a+w ./application/database.php
   chmod a+w ./runtime/ -R
   ```

2. 其次就是可能你的目录绑定到public后，`open_basedir`限制了访问父目录，可以配置下`open_basedir`，添加上级目录即可，通常情况下Linux需要在配置文件中追加的代码是：

   ```
   fastcgi_param PHP_ADMIN_VALUE "open_basedir=/yourpath/fastadmin/:/tmp/:/proc/";
   ```

   如果使用的是lnmp一键安装包，可能需要修改`.user.ini`文件，在`.user.ini`文件中添加

   ```
   open_basedir=/yourpath/fastadmin/:/tmp/:/proc/
   ```

3. 如果使用的是`宝塔面板`，请直接在`网站`->`配置`->`网站目录`中修改`运行目录`为`public`目录
​

## 如何将静态资源采用CDN方式部署到第三方云存储

FastAdmin可以将静态的资源部署到又拍云、七牛云或阿里OSS，可大大的加快网站的访问。
默认FastAdmin的静态资源是不采用CDN部署的，如果需要启用，需要修改以下两个文件的配置

1. 修改`application/extra/site.php`中`cdnurl`的值为你CDN的地址
2. 修改`application/config.php`中`__CDN__`的值为你CDN的地址

请将你的静态资源`public/assets`文件夹上传至你的CDN空间中去。

如果采用了静态资源部署CDN，在后台`插件管理`中对插件执行安装、禁用、启用、卸载后都需要将`public/assets/addons/`目录和`public/assets/js/addons.js`文件再次同步更新到CDN。

如果你需要将上传的文件直传至又拍云、七牛云或阿里OSS，请在插件管理中下载对应第三方云存储的插件并配置好即可。
