# matataki API
  matataki API Documentation

> 关于接口风格，和以前的设计有关，关于RESTful API可以看看[Egg的介绍](https://eggjs.org/zh-cn/tutorials/restful.html) or [REST](https://zh.wikipedia.org/wiki/REST)
>
> 接口调用的例子只是一个例子，希望大家根据实际的情况来写代码😄(承认我很菜~)
>
> 如果接口调用错误的话，可以参考目前网站最新的调用方式，因为文档可能会跟不上接口的迭代！！！

## Basic

所有接口前缀为：

> 如果有变动会在相应的地方做出说明

```
https://api.smartsignature.io
```

## 文章发布到ipfs
  - 发布文章需要先将内容发布到ipfs上

**POST**

```javascript
/post/ipfs
```

**Header**

| 字段           | 类型   | 描述  |
| -------------- | ------ | ----- |
| x-access-token | String | token |

**参数**

| 字段          | 类型   | 描述 |
| ------------- | ------ | ---- |
| data[title]   | String |      |
| data[author]  | String |      |
| data[desc]    | String |      |
| data[content] | String |      |

**举例调用**

```javascript
// 发布到ipfs
// ...
const stringifyData = qs.stringify({
  "data[title]": title,
  "data[author]": author,
  "data[desc]": desc,
  "data[content]": content
});
axios({
  method: "post",
  url: `${API}/post/ipfs`,
  data: stringifyData,
  headers: { "x-access-token": TOKEN }
});
 // ...
```

**返回**

| 字段    | 类型   | 描述                        |
| ------- | ------ | --------------------------- |
| code    | Number | 如果code等于 0 代表请求成功 |
| hash    | String | hash地址                    |
| message | String | 信息反馈                    |

```json
{
  "code":0,
  "message":"成功",
  "hash":"QmccEwKcepT9dWMHPmRyScNAqge8oPNTN12vsxh1QkHykp"
}
```



## 文章图片上传

  - 将图片上传到matataki

    > Todo：还有另一个版本的图片上传接口，后面我会更新
    >
    > 如果单独使用请配合前缀```'https://ssimg.frontenduse.top'```

**POST**

```javascript
/post/uploadImage
```

**Header**

| 字段           | 类型   | 描述  |
| -------------- | ------ | ----- |
| x-access-token | String | token |

**参数**

| 字段  | 类型 | 描述     |
| ----- | ---- | -------- |
| image | file | formdata |

**举例调用**

```javascript
axios({
  method: 'POST',
  url: `${API}/post/uploadImage`,
  headers: { "x-access-token": TOKEN },
  data: formdata
})
```

**返回**

| 字段        | 类型   | 描述                        |
| ----------- | ------ | --------------------------- |
| code        | Number | 如果code等于 0 代表请求成功 |
| message     | String | 信息反馈                    |
| data        | Object | data                        |
| &emsp;cover | String | 文章封面地址                |

```json
{
  "code":0,
  "message":"成功",
  "data": {
    "cover":"/image/2020/01/27/9285aa830488920cc16fb308a2a3d4c8.png"
  }
}
```



## 文章发布

**POST**

```javascript
/post/publish
```

**Header**

| 字段           | 类型   | 描述  |
| -------------- | ------ | ----- |
| x-access-token | String | token |

**参数**

| 字段            | 类型   | 描述                        |
| --------------- | ------ | --------------------------- |
| author          | String | formdata                    |
| cover           | String | 文章封面                    |
| fissionFactor   | Number | 系统遗留 不描述了 默认 2000 |
| hash            | String | ipfs hash地址               |
| platform        | String | 账号平台类型 email 等       |
| publickey       | String | 签名 可留空 null            |
| sign            | String | 签名 可留空 null            |
| msgParams       |        |                             |
| signId          |        |                             |
| title           | String | 文章标题                    |
| is_original     | Number |                             |
| tags            | String |                             |
| cc_license      |        |                             |
| commentPayPoint | Number | 评论积分 最少 1             |
| shortContent    | String | 文章摘要                    |

**举例调用**

```javascript
axios({
  method: "post",
  url: `${API}/post/publish`,
  data: data,
  headers: { "x-access-token": TOKEN }
});
```

```json
// data
{
  "author":"weixin@yopmail.com",
  "cover":"/image/2020/01/27/9285aa830488920cc16fb308a2a3d4c8.png",
  "fissionFactor":2000,
  "hash":"Qma4oWZL7GNEVkwSobVSgc3YB5TnhivdRyWE3gf4RDcc7*",
  "platform":"email",
  "publickey":null,
  "sign":null,
  "msgParams":null,
  "signId":null,
  "title":"????",
  "is_original":0,
  "tags":"",
  "cc_license":null,
  "commentPayPoint":1,
  "shortContent":""
}
```



**返回**

| 字段    | 类型   | 描述                        |
| ------- | ------ | --------------------------- |
| code    | Number | 如果code等于 0 代表请求成功 |
| message | String | 信息反馈                    |
| data    | Number | 文章ID                      |

```json
{
  "code":0,
  "message":"成功",
  "data":101674
}
```

