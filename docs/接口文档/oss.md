### OSS文件服务 - 接口文档

# 一、前言

​	本文档为OSS文件服务接口标准，默认数据交互格式为"json"，请严格按照文档要求进行使用。

### 版本记录

|    日期    | 版本号 | 修订人 |    说明    |
| :--------: | :----: | :----: | :--------: |
| 2023-11-16 |  V1.0  |        | 1.初次添加 |



------



# 二、API

### 获取Token

- 获取调用接口凭证
- JWT授权(数据在请求头的"Authorization"中) ,格式"Bearer {token}" 即可,注意两者之间有空格
- 本文档所有接口(获取token接口除外)都需携带token才可访问

> URI：auth/token/app

> 请求方式：

​	

|      |      |      |
| :--: | :--: | :--: |
|      |      |      |
|      |      |      |

------

## OSS文件接口

### 获取OSS上传链接

- 

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

|      |      |      |
| :--: | :--: | :--: |
|      |      |      |
|      |      |      |



------



------

# 附录

### 鉴权方式

​	本系统使用鉴权方式为"JWT"，请求是需要在请求头的"Authorization"传递token(格式为"Bearer {token}"，需注意两者之间有空格) ，本文档所有接口(获取token接口除外)都需携带token才可访问。

> 

|      |      |      |      |
| ---- | ---- | ---- | ---- |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |
|      |      |      |      |


