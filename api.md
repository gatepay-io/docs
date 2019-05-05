---
title: 接口
type: docs
order: 3
---

## 任意金额支付接口
#### 接口概要
| 接口名称 | 任意金额支付接口 |
| ------- | --------------- |
| 接口URL | https://gatepay.io/api/anypay/create |
| 请求方式 | POST |
| 返回格式 | JSON |

#### 请求参数表
| 名称         | 类型        | 必选     |  描述                                               |
| ------------ | ---------- | -------- | -------------------------------------------------- |
| appkey       | string     | 是       | 秘钥                                                |
| price        | float      | 是       | 商品价格，任意金额都可以（精确小数点后2位 示例：10.23） |
| type         | string     | 是       | 支付方式：wechat（微信）、alipay（支付宝）            |
| out_order_id | string     | 是       | 外部订单编号                                        |
| custom       | string     | 是       | 自定义信息:可以是用户的属性之类如用户ID,邮箱           |
| sign         | string     | 是       | 签名信息算法：sign = md5（md5（appkey + price + type + out_order_id + custom）+appsecret）|

#### 返回结果表
| 数据 | 说明 |
| ---- | --- |
| code | 状态码 |
| msg  | 状态描述 |
| time | 响应时间戳 |
| data | 业务结果集 |
| data.pay_url | 创建的支付地址 |
| data.qrcode_url | 二维码地址 |
| data.qrcode_body | 二维码图像 |
| data.params | 请求的参数 |

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

#### 成功返回的结果例子
```
{
    "code": 100,
    "msg": "请求成功",
    "time": "1556614084",
    "data": {
        "pay_url": "https:\/\/gatepay.io\/pay\/api?id=5cc75a6a0b418&type=wechat",
        "api_url": "https:\/\/gatepay.io\/pay\/api?id=5cc75a6a0b418&type=wechat&format=json",
        "qrcode_url": "https:\/\/gatepay.io\/qrcode\/buildsize=130&text=https%3A%2F%2Fgatepay.io%2Fpay%2Fapi%3Fid%3D5cc75a6a0b418%26type%3Dwechat",
        "qrcode_body": "data:image\/jpeg;base64,iVBORw0KGgoAAAANSUhEUgAAAKAAAACgAQMAAACxAfVuAAAABlBMVEX\/\/\/8AAABVwtN+AAAACXBIWXMAAA7EAAAOxAGVKw4bAAABg0lEQVRIie2WMY7EIAxFHVH4Ukhciw46roXkS1Egeb8hkWa73eByXETK0yh4Pt8fiL71ui5VlUkxVCqV8VL\/BzsF6TF1HtxaJfaAoiI96eRRWmvanGAPPcjgQewHRXSmNiCIE4Qg6F1Ud+fsAW3jrJrV526+h6sCdg6dj1+Geg8vdK6msgJlKFI9YCSKFCOPnIl10DkkCAyFZ9I28rNxh\/CywdIZg\/WO7tUBkmnR0yTMa2k2tecQIttohZ6pQI39w0MIebEQnrnAto8fziCGCyiJYIU7W87hBJAZYQlY4R6Dv0N0GE3NiDZh+\/3NUxhmsviMGX9eR3GBtkqaMdnbY6VDeK2g6zEsiHKAlh+Qw84OeKncqx9CWEksRJDIYDtDTmHaUwR\/Wnr6wLAMGrrNJnaOPeDiOI0z1\/KZywdwnR3dDFbWYVw9oN0ZrFaA8Mc95ADus1hkWDBpLV5w5TIEHrmoE8QtZMayTNtcoN0ZwlxBN1h94Loz7KMYk3Bn8hn81sv6AcQJdFCohA5NAAAAAElFTkSuQmCC",
        "params": {
            "appkey": "098f6bcd4621d373cade4e832627b4f6",
            "price": "0.82",
            "type": "wechat",
            "out_order_id": "5cc75a6a0b418",
            "custom": "terry",
            "sign": "45f46863f10965c0f0671fb738efb13e",
        }
    }
}
```

## 组合商品支付接口
#### 接口概要
| 接口名称 | 组合商品支付接口 |
| ------- | --------------- |
| 接口URL | https://gatepay.io/api/grouppay/create |
| 请求方式 | POST |
| 返回格式 | JSON |

#### 请求参数表
| 名称         | 类型        | 必选     |  描述                                               |
| ------------ | ---------- | -------- | -------------------------------------------------- |
| appkey       | string     | 是       | 秘钥                                                |
| fields       | string     | 是       | 支付模式信息（商品ID:购买件数 可用逗号隔开购买多种商品 示例：8:1,7:1 ） |
| type         | string     | 是       | 支付方式：wechat（微信）、alipay（支付宝）            |
| out_order_id | string     | 是       | 外部订单编号                                        |
| custom       | string     | 是       | 自定义信息:可以是用户的属性之类如用户ID,邮箱           |
| sign         | string     | 是       | 签名信息算法：sign = md5（md5（appkey + fields + type + out_order_id + custom）+appsecret）|

#### 返回结果表
| 数据 | 说明 |
| ---- | --- |
| code | 状态码 |
| msg  | 状态描述 |
| time | 响应时间戳 |
| data | 业务结果集 |
| data.pay_url | 创建的支付地址 |
| data.qrcode_url | 二维码地址 |
| data.qrcode_body | 二维码图像 |
| data.params | 请求的参数 |

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
| 201 | 无效的支付方式    |
| 202 | 当前支付方式已关闭  |
| 203 | 无可用支付方式    |
| 204 | 组合内无有效库存商品 |
| 205 | 分类创建错误     |
| 206 | 产品创建错误     |
| 207 | 库存创建错误     |
| 208 | 队列创建错误     |

#### 成功返回的结果例子
```
{
  "code": 100,
  "msg": "请求成功",
  "time": "1556777605",
  "data": {
    "pay_url": "https://gatepay.io/pay/api?id=af396965-c05a-48b2-8d03-81020dddcb7c&amp;type=wechat",
    "qrcode_url": "https://gatepay.io/qrcode/build?size=130&amp;text=https%3A%2F%2Fgatepay.io%2Fpay%2Fapi%3Fid%3Daf396965-c05a-48b2-8d03-81020dddcb7c%26type%3Dwechat",
    "qrcode_body": "data:image/jpeg;base64,iVBORw0KGgoAAAANSUhEUgAAAKAAAACgAQMAAACxAfVuAAAABlBMVEX///8AAABVwtN+AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAB+klEQVRIie2WMY7sIAyGf0RBN1wg2lwjxUhcKWW60KXMlZBSzDWIcgGmo0D4mc3saF+XDCnXDeKLRGz8Yxv4s49NEGX5oGyi2B6BiOw56HCDsW0CbRQ81BVwoZskS4m/qbDS9AF0PR+mk7HXQXQ6Q4mNPoAcZgO0bsjtf7HXQE5H0/XrMt14+ZWjY7CYfMyCInkVfgmiAori4GP2wJNo/joNiQSTLzPdeJffYdZASJtlhEgDZNTkxnOQsymSIj6Mtse8pt3POggTWezkjc2t0/6+//0wFAmhdf1KEQ10ltMlcMy842/ad5oWOg35zDHfVUkqqxUXwGWi8hNJvPRcdM5BmAnoei4sOnV6fWm+Et55Z2ZabJAO63IWsrokzd5MoTFBLLufdVA4lSVfnbRP4qS64RzkMPnVBMiJ/ezzj+qq4J6O/R05vEv6YZgU2ljEHkq02J2vg3xvbDOgnpsD68yegnx1QXLHSyM3htEbugDy09a+rEpT7H+K1WEo3FhUUJ4Mh8kP6AIIDHr7drDUK6JddScg0Jh5Xb4Fxnmw9bB0LqiZSzNKf385fxxy32z5zsz09OjFfvG1sPR3U8Yfjnuk9J5YjsMG3IQnLulo04BrIAx30aEMQ+2rJh+HZQaDXpf43CJXYeACWEYOZVuK7Ofo8c5RBfyzD+0f5HRQOvNTHzgAAAAASUVORK5CYII=",
    "params": {
      "fields": "8:2,7:3,10:1",
      "type": "wechat",
      "out_order_id": "2d5fdb06-ee8e-43ed-bdc7-f6818e68c042",
      "custom": "terry"
    }
  }
}
```


## 固定商品支付接口
#### 接口概要
| 接口名称 | 固定商品支付接口 |
| ------- | --------------- |
| 接口URL | https://gatepay.io/api/stablepay/create |
| 请求方式 | POST |
| 返回格式 | JSON |

#### 请求参数表
| 名称         | 类型        | 必选     |  描述                                               |
| ------------ | ---------- | -------- | -------------------------------------------------- |
| appkey       | string     | 是       | 秘钥                                                |
| product_id   | string     | 是       | 产品编号                                            |
| type         | string     | 是       | 支付方式：wechat（微信）、alipay（支付宝）            |
| out_order_id | string     | 是       | 外部订单编号                                        |
| custom       | string     | 是       | 自定义信息:可以是用户的属性之类如用户ID,邮箱           |
| sign         | string     | 是       | 签名信息算法：sign = md5（md5（appkey + product_id + type + out_order_id + custom）+appsecret）|

#### 返回结果表
| 数据 | 说明 |
| ---- | --- |
| code | 状态码 |
| msg  | 状态描述 |
| time | 响应时间戳 |
| data | 业务结果集 |
| data.pay_url | 创建的支付地址 |
| data.qrcode_url | 二维码地址 |
| data.qrcode_body | 二维码图像 |
| data.params | 请求的参数 |

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
| 201 | 无效的支付方式    |
| 202 | 当前支付方式已关闭  |
| 203 | 无可用支付方式    |
| 204 | 队列创建错误     |
| 205 | 产品不可获得     |
| 206 | 当前产品无库存    |

#### 成功返回的结果例子
```
{
  "code": 100,
  "msg": "请求成功",
  "time": "1556779654",
  "data": {
    "pay_url": "https://gatepay.io/pay/api?id=aa9633ee-9b23-4d68-af03-5a0eaef434b2&amp;type=wechat",
    "qrcode_url": "https://gatepay.io/qrcode/build?size=130&amp;text=https%3A%2F%2Fgatepay.io%2Fpay%2Fapi%3Fid%3Daa9633ee-9b23-4d68-af03-5a0eaef434b2%26type%3Dwechat",
    "qrcode_body": "data:image/jpeg;base64,iVBORw0KGgoAAAANSUhEUgAAAKAAAACgAQMAAACxAfVuAAAABlBMVEX///8AAABVwtN+AAAACXBIWXMAAA7EAAAOxAGVKw4bAAAB9klEQVRIie2WMY6DMBBFx6JwF18AxdegiOQrUdLZHSVXskTBNUC5AHQUlme/WbKb7SC43CkS6SFhZv6fGRP9x8chmGNpZt0zP33NzO4c9HTTnmLRCsCRZA7Y863w9eQbxZ4mbs/Dsqo14xm7fJAqGg1TaT6ASJNITd4Ssn3L/QpMclT11Lfpc981OgRT6LUm04rxjyEuQNGvsAZydzOZeXxYdxK6ZawokoWalqihDJBdLKlGBQWe/Xj+MAx2CWTxavFcLT43B+xbBbNrbgkmm3aNjkN2YpTz3aRuZA4yA0SxYrHaCd7VayoknYJQc2HuqHCMHFF8lwPiBIY1ZNRQ07QnYZBLqOACuYwSr+UMEBG/PZ/Oi9+mPQEfaJnBQcVbOsFv/rwIRWjUKDvN60xk9S7xYYj8iExyVrJpOuE6FF7e4KzkefbqvrfhcRjwY7opNJjs9uX5a5DMyrxatLbiwWEOnoObP4eZHs2sB7SMzQE9ccCYKdK2UK9hdRii1niZu5ONmJ8cKAPEZGDogKGDP8v75joMU8Ds2kvFPKMpM8Btc0nWfRtpW2AnIfZmWcEFTo1mFt7mgOnKARm9xLawr9KdgpgMGFQQVb3dGa5CT3fjVID1/e9Bx+B2u8AdjNVz6Hgf6Rch5NgGIEPUbvq9h1yA//FhfAFhOkUegl9dwwAAAABJRU5ErkJggg==",
    "params": {
      "product_id": "8",
      "type": "wechat",
      "out_order_id": "6bfad15e-f96d-40b7-a497-6fb4b9387894",
      "custom": "terry"
    }
  }
}
```

## 付款结果查询接口
#### 接口概要
| 接口名称 | 付款结果查询接口 |
| ------- | ----------- |
| 接口URL | https://gatepay.io/api/find/findOrder |
| 请求方式 | GET |
| 返回格式 | JSON |

#### 请求参数表
| 名称 | 类型 | 必选 | 描述 |
| ---- | --- | ---- | --- |
| appkey | string | 是 | 秘钥 |
| out_order_id | string | 是 | 外部订单编号 |
| sign | string | 是 | 签名信息算法：sign = md5(md5(appkey + out_order_id) + appsecret) |

#### 返回结果表
| 数据 | 说明 |
| ---- | --- |
| code | 状态码 |
| msg  | 状态描述 |
| time | 响应时间戳 |
| data | 业务结果集 |
| data.order_id | 订单编号 |
| data.order_title | 订单标题 |
| data.order_price | 订单金额 |
| data.order_type | 支付类型 |
| data.order_status | 交易状态 |

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
| 201 | 订单不存在    |

#### 成功返回的结果例子
```
{
  "code": 100,
  "msg": "请求成功",
  "time": "1557056209",
  "data": {
    "order_id": 522,
    "order_title": "任意金额支付:1.88元",
    "order_price": "1.88",
    "order_type": "alipay",
    "order_status": "expired"
  }
}

```




## 支付成功通知接口
#### 接口概要
| 接口名称 | 支付成功通知接口 |
| ------- | ----------- |
| 接口URL | 管理后台->账户配置->支付成功回调URL |
| 请求方式 | GET |
| 返回格式 | html |

#### 请求参数表
| 名称 | 类型 | 必选 | 描述 |
| ---- | --- | ---- | --- |
| appkey | string | 是 | 秘钥 |
| order_id | integer | 是 | 订单编号 |
| out_order_id | string | 是 | 外部订单编号 |
| price | float | 是 | 订单价格 （精确小数点后2位 示例：10.23） |
| realprice | float | 是 | 真实价格 （精确小数点后2位 示例：10.23） |
| type | string | 是 | 支付类型 |
| paytime | integer | 是 | 支付时间 |
| extend | string | 是 | 联系方式 |
| sign | string | 是 | 签名信息算法：sign = md5(md5(appkey + order_id + out_order_id + price + realprice + type + paytime + extend) + appsecret) |

#### 返回结果表
| 数据 | 说明 |
| ---- | --- |
| success | 回调成功 |
| fail | 回调失败 |


## 快捷收款集成接口
#### 接口概要
| 接口名称 | 快捷收款集成接口 |
| ------- | ------------|
| 接口URL | https://gatepay.io/pay/any |
| 请求方式 | GET |
| 返回格式 | html |

#### 请求参数表
| 名称 | 类型 | 必选 | 描述 |
| ---- | --- | ---- | --- |
| appkey | string | 是 | 秘钥 |
| token | string | 是 | 快捷收款令牌 |
| custom | string | 否 | 联系方式（用户名，邮箱，手机号之类的都可以） |
| price | string | 否 | 金额 |
| skin | int | 否 | 0：默认模板，1：模板1 |
| stable | int | 否 | 是否自定义 默认开启，1关闭 |

#### 返回结果表
| 数据 | 说明 |
| --- | ---- |
|| 快捷收款页面 |

#### 生成您的快捷付款页
```
http://gatepay.io/pay/any?appkey=后台自动生成的Appkey秘钥&price=收款金额&custom=联系方式&skin=模板选择&token=您后台设置的token
```
具体参数及描述，可以参看上方请求参数表

#### 示例1 两个必要参数
https://gatepay.io/pay/any?appkey=e3d704f3542b44a621ebed70dc0efe13&token=qflknfokn

#### 示例2 给定价格为1.88，不能更改
https://gatepay.io/pay/any?appkey=e3d704f3542b44a621ebed70dc0efe13&token=qflknfokn&price=1.88&stable=1

#### 示例3 给定联系方式，不能更改,用第二套模板
https://gatepay.io/pay/any?appkey=e3d704f3542b44a621ebed70dc0efe13&token=qflknfokn&custom=terry&stable=1&skin=1

![skin1](https://gatepay.io/assets/img/pay_any1.png)
![skin2](https://gatepay.io/assets/img/pay_any2.png)












