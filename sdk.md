---
title: SDK
type: docs
order: 4
---
GatePay在基于[Hprose](https://github.com/hprose) 提供的RPC协议 定制了多种编程语言SDK。

Hprose 序列化格式是一个轻量级、自描述、半文本、格式紧凑、动态类型、语言无关、平台无关的序列化格式协议。



### PHP SDK

### JavaScript SDK
首先在你的html里加载gatepay的js脚本：

```html

<script type="text/javascript" src="gatepay.io.js"></script>

```

现在进入正题，gatepay提供三种接口，分别是anypay，stablepay，grouppay，不论哪种接口，我们都需要使用gatepay后台提供我们的appkey和appsecret。

```JavaScript
var appkey = 'your appkey from gatepay';
var appsecret = 'your appsecret from gatepay';
```

1. 任意金额支付 anypay,

这个主要的特点是：金额是任意的，无需后台提前上传二维码，填写商品啥的。比如你的应用是不固定价格的服务，比如充值会员的服务，想充多少充多少。那这个比较合适搞。

调用也很简单：

```Javascript
//注意，测试时，必须在真实网站环境测试，本地文件浏览模式不可以。
var params = {};//定义请求参数
params.price = 0.99;//任意金额都可以，商品价格。
params.type ='wechat';//支付方式，如果是支付宝则填写alipay
params.out_order_id = gatepay.uuid();//外部订单号，也就是你的系统产生的订单号，演示这里是用随机函数生成的编号
params.custom = 'terry';//这个是携带的客户信息， 可以是任何字符串，比如你的网站是充值会员，这个可以是会员用户名，邮箱 或者电话之类的。
//如果担心appsecret泄露，可以在服务端生成。这里直接用js的sdk执行了签名
var sign = gatepay.sign(appkey,params,appsecret);//执行签名，获取携带签名的参数信息，
//发起rpc请求
gatepay.any(sign,function(response){
	if(response.code == 100){
		//代表请求成功
    		gatepay.go(response.data.pay_url); //这个GO方法将会执行页面跳转，直接跳转到支付页面
    	}
    	else{
    		alert(response.msg);//输出错误信息，自己处理咯。
    	}
});
```

2.固定商品支付 stablepay,

这个主要的特点是，先要去管理后台->产品卡密->产品管理里创建一个产品，然后上传支付宝微信二维码。

然后在管理后台->产品卡密->卡密管理 里导入这个产品的卡密。

感觉是很麻烦，但是这个stablepay 可以帮我们做到销售卡密的过程，比如你要卖什么xxx影视会员点卡之类，对接这个api就可以。

直接上代码：

```Javascript
//注意，测试时，必须在真实网站环境测试，本地文件浏览模式不可以。
var params = {};//定义请求参数
params.product_id = '8';//产品ID为8,
params.type ='wechat';//支付方式，如果是支付宝则填写alipay
params.out_order_id = gatepay.uuid();//外部订单号，也就是你的系统产生的订单号，演示这里是用随机函数生成的编号
params.custom = 'terry';//这个是携带的客户信息， 可以是任何字符串，比如你的网站是充值会员，这个可以是会员用户名，邮箱 或者电话之类的。
//如果担心appsecret泄露，可以在服务端生成。这里直接用js的sdk执行了签名
var sign = gatepay.sign(appkey,params,appsecret);//执行签名，获取携带签名的参数信息，
//发起rpc请求
gatepay.stable(sign,function(response){
	if(response.code == 100){
		//代表请求成功
    		gatepay.go(response.data.pay_url); //这个GO方法将会执行页面跳转，直接跳转到支付页面
    	}
    	else{
    		alert(response.msg);//输出错误信息，自己处理咯。
    	}
});
```
3. 组合商品支付  grouppay,

可以实现对多个固定商品 组合后进行支付， 如果你想实现 一些组合出售的需求，可以使用这个接口。

直接上代码
```Javascript
//注意，测试时，必须在真实网站环境测试，本地文件浏览模式不可以。
var params = {};//定义请求参数
params.fields = '8:2,7:3,10:1';//产品ID为8的购买2件，产品ID为7的购买3件，产品ID为10的购买1件。
params.type ='wechat';//支付方式，如果是支付宝则填写alipay
params.out_order_id = gatepay.uuid();//外部订单号，也就是你的系统产生的订单号，演示这里是用随机函数生成的编号
params.custom = 'terry';//这个是携带的客户信息， 可以是任何字符串，比如你的网站是充值会员，这个可以是会员用户名，邮箱 或者电话之类的。
//如果担心appsecret泄露，可以在服务端生成。这里直接用js的sdk执行了签名
var sign = gatepay.sign(appkey,params,appsecret);//执行签名，获取携带签名的参数信息，
//发起rpc请求
gatepay.group(sign,function(response){
	if(response.code == 100){
		//代表请求成功
    		gatepay.go(response.data.pay_url); //这个GO方法将会执行页面跳转，直接跳转到支付页面
    	}
    	else{
    		alert(response.msg);//输出错误信息，自己处理咯。
    	}
});
```

### Go SDK

### Python SDK

### Ruby SDK

### Java SDK

### Node.js SDK

### ASP SDK

### C# SDK

### Objective-C SDK


