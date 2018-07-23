1. 使用复数名词表示资源，例如http://company.com/stores。

2. 使用HTTP Method来表示操作类型。

|  HTTP Method | 描述 | 示例 | 反例 |
| ------------ | ------------ | ------------ | ------------ |
|  GET | 查询 | GET http://company.com/stores | http://company.com/queryStores |
|  POST | 创建 | POST http://company.com/stores | http://company.com/createStores |
|  PUT | 修改 | PUT http://company.com/stores | http://company.com/modifyStores |
|  DELETE | 删除 | DELETE http://company.com/stores | http://company.com/deleteStores |

3. 使用HTTP状态码表示操作结果，而不是通过在响应体里面表示操作结果。

| HTTP状态码 | 描述  |
| ------------ | ------------ |
| 1XX  | 请求已接收并需要继续处理  |
| 2XX  | 请求成功  |
| 3XX  | 重定向  |
| 4XX  | Client端错误  |
| 5XX  | Server端错误  |

REST API常用状态码：

| 状态码  | 描述  |
| ------------ | ------------ |
| 200 OK  | GET, PUT, DELETE请求成功  |
| 201 Created  | POST请求成功，资源已创建  |
| 204 No Content  | 可用于表示GET请求结果为空  |
| 400 Bad Request  | 请求参数有误  |
| 401 Unauthorized  | 用户未认证  |
| 403 Forbidden  | 用户无权限访问资源  |
| 404 Not Found  | 资源不存在  |
| 409 Conflict  | 创建资源已存在  |
| 405 Method Not Allowed  | 用户不允许执行该操作，比如更新一个只读对象  |
| 429 Too Many Requests  | 请求超过允许的数量  |
| 500 Internal Server Error | 服务器内部错误  |

在状态码之外可以在响应体中描述具体错误的类型，比如400 Bad Request里面是哪个参数不合法，例如

    {
        "errorCode" : "1001",
        "errorMessage" : "User name is mandatory."
    }

常见的错误写法是所有响应都返回200 OK，并通过响应体内容区分请求成功失败与否，响应体夹杂着成功和失败的信息，例如

    {
        "statusCode" : "1001",
        "errorMessage" : "User name is mandatory.",
        "entity" : "Another JSON"
    }

4. 为API添加版本号,例如http://company.com/v1/stores。

当API引入不兼容的修改时（比如在请求中增加了一个必填字段），这种情况必须引入新的API版本。引入新版本API的同时需确保旧版本API仍然可用。

常用有两种方式添加API版本信息，一是在URL中，二是在Header里面Accept: application/vnd.example.com.v1+json

5. 使用分页来减少返回结果。

### Reference：
* [RESETful API 设计规范](https://godruoyi.com/posts/resetful-api-design-specifications)
* [Best Practices for Designing a Pragmatic RESTful API](http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api)