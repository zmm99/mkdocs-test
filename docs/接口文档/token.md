### 开放平台接口文档

# 一、前言

​	本文档为对接外部公司接口标准，默认数据交互格式为"json"，请严格按照文档要求进行使用。

### 版本记录

|    日期    | 版本号 | 修订人 |    说明    |
| :--------: | :----: | :----: | :--------: |
| 2023-11-16 |  V1.0  |        | 1.初次添加 |

> 

```
{
  "code": 1,
  "message": "成功",
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYmYiOiIxNjY0MzQ0MzU1IiwiZXhwIjoxNjY0MzQ0Mzg1LCJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9uYW1lIjoiMjY2OGNmZWU4NTQ4NDQ0YmI1ZjdkZWFkNGUxMzU2ZTYiLCJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9uYW1laWRlbnRpZmllciI6IlVZMzh5eXIvbllNdHMrK2o4L2M3VFpsNFBjaXFUNGhHRi9WMFhkTnAwcEU9IiwiaXNzIjoiWUZKd3RJc3N1ZXIiLCJhdWQiOiJZRkN1c3RvbWVyIn0.mlrDRLPpmDAzgnlYddAWSHOArDlaNVyCMLJO4Lnnv8A",
    "expirationTime": "2022-09-28 13:53:05"
  },
  "timestamp": "1664344355485"
}
```

> 返回Data参数：

|      参数      |   类型   |                   说明                   |
| :------------: | :------: | :--------------------------------------: |
|     token      |  string  |                token数据                 |
| expirationTime | datetime | token过期时间，yyyy-MM-dd HH:mm:ss格式。 |

------



------

# 附录

### 鉴权方式

​	本系统使用鉴权方式为"JWT"，请求是需要在请求头的"Authorization"传递token(格式为"Bearer {token}"，需注意两者之间有空格) ，本文档所有接口(获取token接口除外)都需携带token才可访问。

> Header：

|     参数      |  类型  |                    说明                    |
| :-----------: | :----: | :----------------------------------------: |
| Authorization | string | 例如token为“qwer”，那么值应为"Bearer qwer" |

### 参数说明

> 全局返回参数说明：

|   参数    |  类型  |              说明               |
| :-------: | :----: | :-----------------------------: |
|   code    |  int   |        返回码,成功为"1"         |
|  message  | string |            返回信息             |
|   data    | object |            返回数据             |
| timestamp |  long  | 13位时间戳，例如"1667351778075" |

> 全局部分错误码说明：

| 错误码 | 错误说明      | 响应码 | 排查方法                             |
| ------ | ------------- | ------ | ------------------------------------ |
| 1      | 请求成功      | 200    | 接口调用成功                         |
| -1     | 系统繁忙      | 200    | 服务器暂不可用或执行失败             |
| -20    | 未知错误      | 200    | 发生未知错误                         |
| -30    | 服务器异常    | 200    | 服务器内部异常                       |
| 404    | 无此资源      | 200    | 服务器查无此资源                     |
| 10003  | Token不合法   | 200    | Token格式错误、为空或者被内容被篡改  |
| 10002  | Token已过期   | 200    | Token过期了，请重新获取              |
| 16000  | API功能未授权 | 200    | 无权访问API                          |
| 15000  | 用户不存在    | 200    | 用户不存在                           |
| 12004  | 模型绑定失败  | 200    | 请求时的参数格式错误，检查请求的参数 |


