## 1.配置回调

在集成支付到你的系统之前，第一步要做的事情就是配置回调地址。

回调地址分为三种，分别是`同步回调地址`，`异步回调地址`，`支付超时地址`

在后台的"账户配置"里分别填写，其中同步回调地址，异步回调地址是`必填`选项，支付超时地址是`选填`。

![](https://cloud.gatepay.io/assets/teaching/001.png)

他们的含义分别是：

1.异步回调地址:如果云端检测到订单已支付，云端的推送网络会往你填写的地址发送一次post请求，将订单信息推送过去。

2.同步回调地址:如果异步回调地址返回"success",则支付页面会执行网页跳转，跳转到你填写的这个地址。

3.支付超时地址:如果支付没有到账，或者用户没有支付，订单因为超时而关闭后跳转的地址。

### 完整接入流程图

![](https://cloud.gatepay.io/assets/teaching/002.png)

### 支付成功异步通知接口

#### 接口概要

| 接口名称  | 支付成功通知接口                |
|-------|-------------------------|
| 接口URL | 管理后台\->账户配置\->支付成功回调URL |
| 请求方式  | POST                    |
| 返回格式  | html                    |


#### 请求参数表

| 名称             | 类型      | 必选 | 描述                                                                                                                                |
|----------------|---------|----|-----------------------------------------------------------------------------------------------------------------------------------|
| order\_id      | integer | 是  | 订单编号                                                                                                                              |
| out\_order\_id | string  | 是  | 外部订单编号                                                                                                                            |
| price          | float   | 是  | 订单价格 （精确小数点后2位 示例：10\.23）                                                                                                         |
| realprice      | float   | 是  | 真实价格 （精确小数点后2位 示例：10\.23）                                                                                                         |
| type           | string  | 是  | 支付类型                                                                                                                              |
| paytime        | integer | 是  | 支付时间                                                                                                                              |
| extend         | string  | 是  | 联系方式                                                                                                                              |
| sign           | string  | 是  | 签名信息算法：sign = md5\(md5\(appkey \+ order\_id \+ out\_order\_id \+ price \+ realprice \+ type \+ paytime \+ extend\) \+ appsecret\) |


#### 返回结果表

| 数据      | 说明   |
|---------|------|
| success | 回调成功 |
| fail    | 回调失败 |


### 支付成功同步通知接口

#### 接口概要

| 接口名称  | 支付成功通知接口                  |
|-------|---------------------------|
| 接口URL | 管理后台\->账户配置\->支付成功后前台跳转地址 |
| 请求方式  | GET                       |
| 返回格式  | html                      |


#### 请求参数表

| 名称             | 类型      | 必选 | 描述                                                                                                             |
|----------------|---------|----|----------------------------------------------------------------------------------------------------------------|
| price          | float   | 是  | 订单价格 （精确小数点后2位 示例：10\.23）                                                                                      |
| type           | string  | 是  | 支付类型                                                                                                           |
| product\_id    | string  | 是  | 产品ID                                                                                                           |
| order\_id      | integer | 是  | 订单编号                                                                                                           |
| out\_order\_id | string  | 是  | 外部订单编号                                                                                                         |
| sign           | string  | 是  | 签名信息算法：sign = md5\(md5\(appkey \+ price \+ type \+ prodcut\_id \+ order\_id \+ out\_order\_id\) \+ appsecret\) |


#### 返回结果表

| 数据   | 说明 |
|------|----|
| html | 地址 |


## 2.扫码上线

这一步，我们可以在后台的`云端管理`里`云端扫码`功能来快速上线你手上的账户。

如下图所示，点击`+`开启扫码进程，需要注意的是，成功扫码上线将会扣除相应的`上码费`(积分)。

![](https://cloud.gatepay.io/assets/teaching/004.png)

`上码费`:按每次成功将一个支付宝或者微信上线到云端收费。

`积分`:积分是本系统内唯一流通的清算货币，100积分=1元(人民币)，请提前联系服务商充值足够的积分。

云端扫码进程开启后，请耐心等待出码过程

![](https://cloud.gatepay.io/assets/teaching/005.png)

生成的二维码是登录支付宝或者微信的官方授权码，请放心使用

![](https://cloud.gatepay.io/assets/teaching/006.png)

提示扫码成功后点击菜单栏的在线会话参看上线的账户

![](https://cloud.gatepay.io/assets/teaching/008.png)

如果想要重新上线旧的会话，可以切换到离线会话，点击"扫码上线” 实现会话复用。

![](https://cloud.gatepay.io/assets/teaching/007.png)

`什么是会话`:会话是一个在云端常驻的虚拟化进程，功能是监控支付宝或者微信账单变化。

如果你听过或者做过在网上挂QQ之类的业务，类比理解，一个会话等于是挂一个支付宝或者微信账户的在线软件进程。


<style type="text/css">
  html,body,div,span,applet,object,iframe,h1,h2,h3,h4,h5,h6,p,blockquote,pre,a,abbr,acronym,address,big,cite,code,del,dfn,em,img,ins,kbd,q,s,samp,small,strike,strong,sub,sup,tt,var,b,u,i,center,dl,dt,dd,ol,ul,li,fieldset,form,label,legend,table,caption,tbody,tfoot,thead,tr,th,td,article,aside,canvas,details,embed,figure,figcaption,footer,header,hgroup,menu,nav,output,ruby,section,summary,time,mark,audio,video{margin:0;padding:0;border:0}body{font-family:Helvetica,arial,freesans,clean,sans-serif;font-size:14px;line-height:1.6;color:#333;background-color:#fff;padding:20px;max-width:960px;margin:0 auto}body>*:first-child{margin-top:0 !important}body>*:last-child{margin-bottom:0 !important}p,blockquote,ul,ol,dl,table,pre{margin:15px 0}h1,h2,h3,h4,h5,h6{margin:20px 0 10px;padding:0;font-weight:bold;-webkit-font-smoothing:antialiased}h1 tt,h1 code,h2 tt,h2 code,h3 tt,h3 code,h4 tt,h4 code,h5 tt,h5 code,h6 tt,h6 code{font-size:inherit}h1{font-size:28px;color:#000}h2{font-size:24px;border-bottom:1px solid #ccc;color:#000}h3{font-size:18px}h4{font-size:16px}h5{font-size:14px}h6{color:#777;font-size:14px}body>h2:first-child,body>h1:first-child,body>h1:first-child+h2,body>h3:first-child,body>h4:first-child,body>h5:first-child,body>h6:first-child{margin-top:0;padding-top:0}a:first-child h1,a:first-child h2,a:first-child h3,a:first-child h4,a:first-child h5,a:first-child h6{margin-top:0;padding-top:0}h1+p,h2+p,h3+p,h4+p,h5+p,h6+p{margin-top:10px}a{color:#4183c4;text-decoration:none}a:hover{text-decoration:underline}ul,ol{padding-left:30px}ul li>:first-child,ol li>:first-child,ul li ul:first-of-type,ol li ol:first-of-type,ul li ol:first-of-type,ol li ul:first-of-type{margin-top:0}ul ul,ul ol,ol ol,ol ul{margin-bottom:0}dl{padding:0}dl dt{font-size:14px;font-weight:bold;font-style:italic;padding:0;margin:15px 0 5px}dl dt:first-child{padding:0}dl dt>:first-child{margin-top:0}dl dt>:last-child{margin-bottom:0}dl dd{margin:0 0 15px;padding:0 15px}dl dd>:first-child{margin-top:0}dl dd>:last-child{margin-bottom:0}pre,code,tt{font-size:12px;font-family:Consolas,"Liberation Mono",Courier,monospace}code,tt{margin:0;padding:0;white-space:nowrap;border:1px solid #eaeaea;background-color:#f8f8f8;border-radius:3px}pre>code{margin:0;padding:0;white-space:pre;border:0;background:transparent}pre{background-color:#f8f8f8;border:1px solid #ccc;font-size:13px;line-height:19px;overflow:auto;padding:6px 10px;border-radius:3px}pre code,pre tt{background-color:transparent;border:0}blockquote{border-left:4px solid #DDD;padding:0 15px;color:#777}blockquote>:first-child{margin-top:0}blockquote>:last-child{margin-bottom:0}hr{clear:both;margin:15px 0;height:0;overflow:hidden;border:0;background:transparent;border-bottom:4px solid #ddd;padding:0}table th{font-weight:bold}table th,table td{border:1px solid #ccc;padding:6px 13px}table tr{border-top:1px solid #ccc;background-color:#fff}table tr:nth-child(2n){background-color:#f8f8f8}img{max-width:100%}
  body{margin:0;}
</style>

## 3.收款规则

什么是`收款规则`?

收款规则就是通过限制收款时间、收款金额、付款方归属地来针对具体账户的限制展示支付二维码的一套规则。

a.如何创建收款规则？

后台->云端管理->收款规则，可以创建和管理收款规则。

b.如何设置`默认收款规则`？

后台->账户配置->默认收款规则,默认收款规则只针对`新上线`的会话有效。

c.如何针对具体的会话设置收款规则？

后台->云端管理->在线会话,点击`收款规则按钮`实现实施规则到具体的会话。

d.如何对账户进行轮询收款呢？

后台->账户配置->云端轮询策略

`智能随机`:如果上一笔完成的交易是A会话，则当前生成二维码时，会剔除A会话，然后从剩余的在线会话里随机一个会话。

`均匀收款`:所有在线可用的会话里，按当日收款金额从大到小排序，剔除收款金额最大的那个会话，然后随机一个会话。

`普通随机`:所有在线可用的会话里，随机一个会话。

## 4.测试支付

![](https://cloud.gatepay.io/assets/teaching/008.png)

在正式部署前，我们可用通过测试支付来判断收款规则、轮询策略、收款账户等能否正常收款。

## 发起支付

#### 接口概要

| 接口名称  | 支付接口                            |
|-------|---------------------------------|
| 接口URL | \{$domain\}/api/cloudpay/create |
| 请求方式  | POST                            |
| 返回格式  | JSON                            |


#### 请求参数表

| 名称             | 类型     | 必选 | 描述                                                                                         |
|----------------|--------|----|--------------------------------------------------------------------------------------------|
| appkey         | string | 是  | 后台\->账户设置\->appkey                                                                         |
| price          | float  | 是  | 商品价格，任意金额都可以（精确小数点后2位 示例：10\.23）                                                           |
| type           | string | 是  | 支付方式：alipay（支付宝）                                                                           |
| out\_order\_id | string | 是  | 外部订单编号                                                                                     |
| custom         | string | 是  | 自定义信息:可以是用户的属性之类如用户ID,邮箱                                                                   |
| sign           | string | 是  | 签名信息算法：sign = md5\(md5\(appkey \+ price \+ type \+ out\_order\_id \+ custom\)\+appsecret\) |

`appsecret:在后台->账户配置->appsecret`

`请不要公开泄露您的appsecret,修改登录密码会强制更新appsecret`

#### 返回结果表

| 数据                | 说明      |
|-------------------|---------|
| code              | 状态码     |
| msg               | 状态描述    |
| time              | 响应时间戳   |
| data              | 业务结果集   |
| data\.pay\_url    | 创建的支付地址 |
| data\.qrcode\_url | 二维码地址   |
| data\.params      | 请求的参数   |


#### 状态码表

| 状态码 | 描述         |
|-----|------------|
| 101 | 秘钥必须       |
| 102 | 无效的秘钥      |
| 103 | 秘钥已过期      |
| 103 | 签名必须       |
| 104 | 无效的签名      |
| 105 | 参数缺失       |
| 106 | 存在禁止传递的参数  |
| 107 | api已关闭     |
| 108 | 回调接口url未填写 |
| 109 | 通知接口url未填写 |
| 110 | 套餐已超额      |
| 199 | 未知错误       |
| 201 | 价格无效       |
| 202 | 无效的支付方式    |
| 203 | 当前支付方式已关闭  |
| 204 | 无可用支付方式    |
| 205 | 分类创建错误     |
| 206 | 产品创建错误     |
| 207 | 库存创建错误     |
| 208 | 队列创建错误     |
| 209 | 非代理用户      |


#### 成功返回的结果例子

```
{
    "code": 100,
    "msg": "请求成功",
    "time": "1556614084",
    "data": {
        "pay_url": "{$domain}\/pay\/api?id=5cc75a6a0b418&amp;type=alipay",
        "qrcode_url": "{$domain}/qrcode\/buildsize=130&amp;text={$domain}%2Fpay%2Fapi%3Fid%3D5cc75a6a0b418%26type%3Dalipay",
       	"params": {
            "appkey": "098f6bcd4621d373cade4e832627b4f6",
            "price": "0.82",
            "type": "alipay",
            "out_order_id": "5cc75a6a0b418",
            "custom": "test_user",
            "sign": "45f46863f10965c0f0671fb738efb13e",
        }
    }
}
```

提取json数据中`data.pay_url`后，在浏览器里执行跳转到这个支付页面即可，商户`无需自行设计`支付页面。

## 6.支付页面

在`5.发起支付`获取得到`data.pay_url`就是支付页面。

客户不需要再设计这个支付页面，因为我们已经在支付页面做了如下几个功能：

a.适配PC

![](https://cloud.gatepay.io/assets/teaching/009.png)

b.适配H5

![](https://cloud.gatepay.io/assets/teaching/010.png)

c.自带订单异步查询

d.如果支付超时，且配置了超时回调地址，网页会自动跳转到配置的地址

e.如果支付成功，且配置了同步回调地址，网页会自动跳转到配置的地址
