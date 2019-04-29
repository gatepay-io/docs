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

#### 请求参数表

| 名称         | 类型        | 必选     |  描述                                     |
| ------------ | ---------- | -------- | ---------------------------------------- |
| appkey       | string     | 是       | 秘钥                                      |
| product_id   | integer    | 是       | 产品编号                                  |
| out_order_id | string     | 是       | 外部订单号                                |
| product_num  | integer    | 是       | 购买产品数量                              |
| pay_type     | string     | 是       | 支付类型 （wechat/alipay/onecode）        |
| custom       | string     | 是       | 自定义信息:可以是用户的属性之类如用户ID,邮箱 |
| sign         | string     | 是       | 签名信息算法：sign = md5（md5（appkey + product_id + product_num + pay_type + out_order_id + custom）+appsecret） |

#### 返回结果表

| 数据 | 说明 |
| ---  | --- |
| code | 状态码 |
| msg | 状态描述 |
| time | 响应时间戳 |
| data | 业务结果集 |
| data.order_type | 订单类型 |
| data.order_price | 订单价格 |
| data.order_url | 支付链接 |
| data.order_qrcode | 支付二维码 |

#### 状态码表

| 状态码 | 说明 |
| ---- | ---- |
| 100 | 成功 |
| 101 | 参数不完整 |
| 102 | 无效的支付类型 |
| 103 | 微信支付只能单件购买 |
| 104 | 产品编号不合法 |
| 105 | 购买数量需要大于0 |
| 106 | 产品信息不存在 |
| 107 | 商铺信息不存在 |
| 108 | 无效的秘钥 |
| 109 | 签名失败 |
| 110 | 有效库存不足 |
| 111 | 商铺当日额度已用完 |
| 112 | 商铺授权已过期 |

#### 成功返回的结果例子
```
  {
  "code": 100,
  "msg": "请求成功",
  "time": "1555750250",
  "data": {
    "order_type": "wechat",
    "order_price": 1.5,
    "order_url": "https://gatepay.io/pay/index?id=5cbadd67774f8&type=wechat",
    "order_qrcode": "data:image/jpeg;base64,iVBORw0KGgoAAAANSUhEUgAAAKAAAACgAQMAAACxAfVuAAAABlBMVEX///8AAABVwtN+AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAB/klEQVRIie2WMY6sMBBEyyIggwsgfA0CJK5ESGZnE3IlSwRzDSMuAJkDRP8yM7N/QlgI1xE8JOjuKpcB/tavlxLZtMyj43XViog9Bx2yAkaJzRLXeqR3wEEyoC2ToCRglMd5WDR9WeNeCBifBBTNfB6yzcTlWxOyovru/QqkHLwbh0eEXxodg3GxwF2AdP4yxAWohiCTzJQjXxvra2NPQdRG+cpsDetEDnS4ASaSs2G1Glmr9lP5Yahcx+Za5VKwVJ/YOyDNrp0pqaaWfhzeGh2FfNMyPXuRsBVpL6u5AyJl07lHN2t6fgg4BdVgZ1TGcyNTTXHvXXwJsk7x1KHu8snlaF5lHoY05sI6EUf3tL75hNUlKHa3Rp0u0bRnIRrhXa/lgaKCdi9/XoM0GPeRaAkLra/Xd1wchoNdJmdGkYXTRw3cAHdnWT5TU2hLnIRUc44jrzvGFvMz3AFrmhZxZosEI8OeycehWsF39h7IPSP9tWWuQseYaWJwZkwGtb7VPAppBhaJEmaj4bc6tdch5cgSEcaMTE+eEgGnYFw65NqlNEOr3vO8BvdfDn6BJxdj9CcVD8P976Jludw5PKvMHTCe7zxFGelFZaJZTkO2KQ7KIx8/AXgZFqmUjeUU+vEVNicg20RFM3RInr0eboFRDof4hf2Y+K/R7+Hf+uX6B3+4Ja732AjXAAAAAElFTkSuQmCC"
  }
}
```




































