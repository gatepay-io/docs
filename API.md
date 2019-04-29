---
title: 接口
type: docs
order: 4
---


## 支付接口 

| 接口名称   | 创建支付订单   |
| --------- | ----- |
| 接口URL    | https://gatepay.io/api/pay/create |
| 请求方式   | Post  |
| 返回格式   | JSON  |

###请求参数表

| 名称         | 类型        | 必选     |  描述                                     |
| ------------ | ---------- | -------- | ---------------------------------------- |
| appkey       | string     | 是       | 秘钥                                      |
| product_id   | integer    | 是       | 产品编号                                  |
| out_order_id | string     | 是       | 外部订单号                                |
| product_num  | integer    | 是       | 购买产品数量                              |
| pay_type     | string     | 是       | 支付类型 （wechat/alipay/onecode）        |
| custom       | string     | 是       | 自定义信息:可以是用户的属性之类如用户ID,邮箱 |
| sign         | string     | 是       | 签名信息算法：sign = md5（md5（appkey + product_id + product_num + pay_type + out_order_id + custom）+appsecret） |
