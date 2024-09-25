### 银丰基因OSS文件服务 - 接口文档

# 一、前言

​	本文档为银丰基因OSS文件服务接口标准，默认数据交互格式为"json"，请严格按照文档要求进行使用。

### 版本记录

|    日期    | 版本号 | 修订人 |    说明    |
| :--------: | :----: | :----: | :--------: |
| 2023-11-16 |  V1.0  | 张传强 | 1.初次添加 |

### BaseUrl

​	开发调试：https://ittest.yfgene.net:1507

​	测试环境：https://ittest.yfgene.net:1507

​	生产环境：https://api.yinfenggene.com 内网：http://172.21.190.69

------



# 二、API

### 获取Token

- 获取调用接口凭证
- JWT授权(数据在请求头的"Authorization"中) ,格式"Bearer {token}" 即可,注意两者之间有空格
- 本文档所有接口(获取token接口除外)都需携带token才可访问

> URI：auth/token/app

> 请求方式：

​	GET

> 请求参数：

|   参数    |  类型  | 是否必填 |     说明      |
| :-------: | :----: | :------: | :-----------: |
|   appId   | string |    是    | 调用方的AppId |
| appSecret | string |    是    |     密钥      |

> 请求示例：

GET http://www.xxx.com/auth/token/app?appId=xxx&appSecret=xxx

> 响应结果示例：

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

## OSS文件接口

### 获取OSS上传链接

- 获取OSS上传链接及授权策略

> URI：ossfile/link/upload/single

> 请求方式：

GET https://www.xxx.com/ossfile/link/upload/single

> 请求参数：

|    参数     |  类型  | 是否必填 |  传参方式   |                             说明                             |
| :---------: | :----: | :------: | :---------: | :----------------------------------------------------------: |
|  fileName   | string |    是    | querystring |              文件名称，要求带后缀，如“123.txt”               |
|  useSource  | string |    是    | querystring |                            调用方                            |
|     md5     | string |    是    | querystring | 文件md5，大写去“-”的md5，长度32，如“8087129A8E7A9AFF0E49F213826EB29B” |
|    path     | string |    否    | querystring |           文件路径，如default/，如有多层请用/隔开            |
|  bucketKey  | string |    否    | querystring |        存储空间，固定值，测试环境“1”，生产环境无需传         |
|  duration   |  int   |    否    | querystring |              有效期(秒)，默认3600，最大为86400               |
| useInternal |  bool  |    否    | querystring | 是否使用内网，内网指的是生产环境的内网环境，默认false，根据实际情况选择，建议能使用内网请务必使用内网 |

> 响应结果示例：

```
{
  "code": 1,
  "message": "成功",
  "data": {
    "fileId": 0,
    "uploadPolicy": {
      "key": "string",
      "host": "string",
      "issuingTime": "2023-12-05T06:16:26.783Z",
      "expirationTime": "2023-12-05T06:16:26.783Z",
      "bucket": "string",
      "ossAccessKeyId": "string",
      "policy": "string",
      "signature": "string",
      "callback": "string"
    }
  },
  "timestamp": "1664344355485"
}
```

> 返回Data参数：

|     参数     | 类型  |                             说明                             |
| :----------: | :---: | :----------------------------------------------------------: |
|    fileId    | long  | 文件ID,若为0，则需要使用uploadPolicy上传文件，若不为0，说明文件已存在，无需上传 |
| uploadPolicy | array | 上传授权策略,数据为上传oss所必须的授权策略，host为上传地址，请使用formdata上传，上传谓词为“post”，需注意的是file一定放到最后，如下所示 |

![image-20231205143101337](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20231205143101337.png)

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


