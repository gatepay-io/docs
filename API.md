---
title: 接口
type: docs
order: 3
---


## 支付接口 
#### 请求接口
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

## 产品接口
#### 请求接口
| 接口名称 | 获取产品信息 |
| ------- | ----------- |
| 接口URL | https://gatepay.io/api/product/show |
| 请求方式 | Post |
| 返回格式 | JSON |

#### 请求参数表
| 名称 | 类型 | 必选 | 描述 |
| --- | ---- | ---- | --- |
| appkey | string | 是 | 秘钥 |
| sign | string | 是 | 签名信息算法：sign = md5（md5（appkey）+appsecret） |

#### 返回结果表
| 数据 | 说明 |
| ---  | --- |
| code | 状态码 |
| msg | 状态描述 |
| time | 响应时间戳 |
| data | 业务结果集 |
| data.category | 产品类型 |
| data.category.id | 产品类型编号 |
| data.category.name | 产品类型名称 |
| data.category.product | 产品信息 |
| data.category.product.id | 产品编号 |
| data.category.product.admin_id | 产品所属用户编号 |
| data.category.product.category_id | 产品所属类型编号 |
| data.category.product.name | 产品名称 |
| data.category.product.description | 产品描述 |
| data.category.product.image | 产品图片 |
| data.category.product.price | 产品价格 |
| data.category.product.stock | 产品库存 |

#### 状态码表
| 状态码 | 说明 |
| ---- | ---- |
| 100 | 成功 |
| 101 | 参数不完整 |
| 102 | 无效的秘钥 |
| 103 | 签名失败 |

#### 成功返回的结果例子
```
  {
  "code": 100,
  "msg": "请求成功",
  "time": "1555773183",
  "data": {
    "category": [
      {
        "id": 39,
        "name": "爱奇艺会员",
        "product": [
          {
            "id": 4,
            "admin_id": 6,
            "category_id": 39,
            "name": "爱奇艺牛逼号",
            "description": "爱奇艺牛逼账号出售",
            "image": "https://gatepay.gatecdn.com/uploads/20190414/51bf070aef0b51ea6c0597569a2a3f32.jpeg",
            "price": "1.00",
            "stock": 4
          }
        ]
      },
      {
        "id": 40,
        "name": "腾讯会员",
        "product": [
          {
            "id": 5,
            "admin_id": 6,
            "category_id": 40,
            "name": "腾讯视频稳定号",
            "description": "腾讯视频稳定号",
            "image": "https://gatepay.gatecdn.com/uploads/20190414/98095a716fe1de7ca364fac50408a260.jpg",
            "price": "1.90",
            "stock": 1
          },
          {
            "id": 8,
            "admin_id": 6,
            "category_id": 40,
            "name": "腾讯视频SVIP账号",
            "description": "超强，什么都能看",
            "image": "https://gatepay.gatecdn.com/uploads/20190415/2d169ca784ebfef2bc97f204b18ad80f.png",
            "price": "0.99",
            "stock": 89
          }
        ]
      }
    ]
  }
}
```

## 卡密接口
#### 请求接口
| 接口名称 | 获取产品卡密 |
| ------- | ----------- |
| 接口URL | https://gatepay.io/api/ka/show |
| 请求方式 | Post |
| 返回格式 | JSON |

#### 请求参数表
| 名称 | 类型 | 必选 | 描述 |
| ---- | --- | ---- | --- |
| appkey | string | 是 | 秘钥 |
| product_id | integer | 是 | 产品编号 |
| page | integer | 是 | 第几页 |
| sign | string | 是 | 签名信息算法：sign = md5（md5（appkey + product_id）+appsecret) |

#### 返回结果表
| 数据 | 说明 |
| ---  | --- |
| code | 状态码 |
| msg | 状态描述 |
| time | 响应时间戳 |
| data | 业务结果集 |
| data.ka | 产品卡密列表 |
| data.ka.total | 产品卡密总数 |
| data.ka.per_page | 每页显示卡密数量 |
| data.ka.current_page | 当前页数 |
| data.ka.last_page | 总页数 |
| data.ka.data | 卡密详情 |
| data.ka.data.id | 卡密编号 |
| data.ka.data.admin_id | 商品编号 |
| data.ka.data.pay_product_id | 商品编号 |
| data.ka.data.pay_order_id | 订单编号 |
| data.ka.data.content | 卡密内容 |
| data.ka.data.create_at | 创建时间 |
| data.ka.data.update_at | 更新时间 |
| data.ka.data.status | 卡密状态 |

#### 状态码表
| 状态码 | 说明 |
| ---- | ---- |
| 100 | 成功 |
| 101 | 参数不完整 |
| 102 | 产品编号不合法 |
| 103 | 产品不存在 |
| 104 | 商铺不存在 |
| 105 | 秘钥错误 |
| 106 | 签名失败 |
| 107 | 接口已关闭 |
| 108 | 页数不合法 |

#### 成功返回的结果例子
```
  {
  "code": 100,
  "msg": "请求成功",
  "time": "1556251812",
  "data": {
    "ka": {
      "total": 70,
      "per_page": 50,
      "current_page": 2,
      "last_page": 2,
      "data": [
        {
          "id": 1272,
          "admin_id": 3,
          "pay_product_id": 3,
          "pay_order_id": 0,
          "content": "asdfsafasdfsadf",
          "createtime": 1556251520,
          "updatetime": 1556251520,
          "status": "soldin"
        },
        {
          "id": 1273,
          "admin_id": 3,
          "pay_product_id": 3,
          "pay_order_id": 0,
          "content": "asdf",
          "createtime": 1556251520,
          "updatetime": 1556251520,
          "status": "soldin"
        }
      ]
    }
  }
}
```

#### 请求接口
| 接口名称 | 创建产品卡密 |
| ------- | ----------- |
| 接口URL | 	https://gatepay.io/api/ka/create |
| 请求方式 | Post |
| 返回格式 | JSON |

#### 请求参数表
| 名称 | 类型 | 必选 | 描述 |
| ---- | --- | ---- | --- |
| appkey | string | 是 | 秘钥 |
| product_id | integer | 是 | 产品编号 |
| content | string | 是 | 卡密内容(可批量创建，一行一条记录，最多支持500条) |
| sign | string | 是 | 签名信息算法：sign = md5（md5（appkey + product_id + content）+appsecret） |

#### 返回结果表
| 数据 | 说明 |
| ---  | --- |
| code | 状态码 |
| msg | 状态描述 |
| time | 响应时间戳 |
| data | 卡密创建记录 |

#### 状态码表
| 状态码 | 说明 |
| ---- | ---- |
| 100 | 成功 |
| 101 | 参数不完整 |
| 102 | 产品编号不合法 |
| 103 | 产品不存在 |
| 104 | 商铺不存在 |
| 105 | 秘钥错误 |
| 106 | 签名失败 |
| 107 | 接口已关闭 |
| 109 | 卡密内容本身有重复 |
| 110 | 卡密内容为空 |
| 111 | 最多支持批量上传500条记录 |
| 112 | 未能录入有效内容，新卡密在数据库中均已存在 |
| 113 | 未能录入有效内容，批量插入数据库失败 |

#### 成功返回结果的例子
```
{
  "code": 100,
  "msg": "请求成功",
  "time": "1556271413",
  "data": "成功录入:1条卡密"
}
```

## 支付成功回调接口
#### 请求接口
| 接口名称 | 支付成功回调 |
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














