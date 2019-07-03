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

## 支付成功异步通知接口

#### 接口概要

  <table>
   <thead>
    <tr>
     <th>接口名称</th>
     <th>支付成功通知接口</th>
    </tr>
   </thead>
   <tbody>
    <tr>
     <td>接口URL</td>
     <td>管理后台-&gt;账户配置-&gt;支付成功回调URL</td>
    </tr>
    <tr>
     <td>请求方式</td>
     <td>POST</td>
    </tr>
    <tr>
     <td>返回格式</td>
     <td>html</td>
    </tr>
   </tbody>
  </table>

#### 请求参数表

  <table>
   <thead>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>必选</th>
     <th>描述</th>
    </tr>
   </thead>
   <tbody>
    <tr>
     <td>order_id</td>
     <td>integer</td>
     <td>是</td>
     <td>订单编号</td>
    </tr>
    <tr>
     <td>out_order_id</td>
     <td>string</td>
     <td>是</td>
     <td>外部订单编号</td>
    </tr>
    <tr>
     <td>price</td>
     <td>float</td>
     <td>是</td>
     <td>订单价格 （精确小数点后2位 示例：10.23）</td>
    </tr>
    <tr>
     <td>realprice</td>
     <td>float</td>
     <td>是</td>
     <td>真实价格 （精确小数点后2位 示例：10.23）</td>
    </tr>
    <tr>
     <td>type</td>
     <td>string</td>
     <td>是</td>
     <td>支付类型</td>
    </tr>
    <tr>
     <td>paytime</td>
     <td>integer</td>
     <td>是</td>
     <td>支付时间</td>
    </tr>
    <tr>
     <td>extend</td>
     <td>string</td>
     <td>是</td>
     <td>联系方式</td>
    </tr>
    <tr>
     <td>sign</td>
     <td>string</td>
     <td>是</td>
     <td>签名信息算法：sign = md5(md5(appkey + order_id + out_order_id + price + realprice + type + paytime + extend) + appsecret)</td>
    </tr>
   </tbody>
  </table>

#### 返回结果表

  <table>
   <thead>
    <tr>
     <th>数据</th>
     <th>说明</th>
    </tr>
   </thead>
   <tbody>
    <tr>
     <td>success</td>
     <td>回调成功</td>
    </tr>
    <tr>
     <td>fail</td>
     <td>回调失败</td>
    </tr>
   </tbody>
  </table>

## 支付成功同步通知接口

#### 接口概要

  <table>
   <thead>
    <tr>
     <th>接口名称</th>
     <th>支付成功通知接口</th>
    </tr>
   </thead>
   <tbody>
    <tr>
     <td>接口URL</td>
     <td>管理后台-&gt;账户配置-&gt;支付成功后前台跳转地址</td>
    </tr>
    <tr>
     <td>请求方式</td>
     <td>GET</td>
    </tr>
    <tr>
     <td>返回格式</td>
     <td>html</td>
    </tr>
   </tbody>
  </table>

#### 请求参数表

  <table>
   <thead>
    <tr>
     <th>名称</th>
     <th>类型</th>
     <th>必选</th>
     <th>描述</th>
    </tr>
   </thead>
   <tbody>
    <tr>
     <td>price</td>
     <td>float</td>
     <td>是</td>
     <td>订单价格 （精确小数点后2位 示例：10.23）</td>
    </tr>
    <tr>
     <td>type</td>
     <td>string</td>
     <td>是</td>
     <td>支付类型</td>
    </tr>
    <tr>
     <td>product_id</td>
     <td>string</td>
     <td>是</td>
     <td>产品ID</td>
    </tr>
    <tr>
     <td>order_id</td>
     <td>integer</td>
     <td>是</td>
     <td>订单编号</td>
    </tr>
    <tr>
     <td>out_order_id</td>
     <td>string</td>
     <td>是</td>
     <td>外部订单编号</td>
    </tr>
    <tr>
     <td>sign</td>
     <td>string</td>
     <td>是</td>
     <td>签名信息算法：sign = md5(md5(appkey + price + type + prodcut_id + order_id + out_order_id) + appsecret)</td>
    </tr>
   </tbody>
  </table>

#### 返回结果表

  <table>
    <tr>
     <th>数据</th>
     <th>说明</th>
    </tr>
    <tr>
     <td>html</td>
     <td>地址</td>
    </tr>
  </table>

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
