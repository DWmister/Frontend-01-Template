## 随堂作业：

- 把课上老师的脑图里的这些实体补全
- 你能不能在 ECMA 中找到所有的类型（Type）
- 把库里边的 URL 解析代码写一下



### 第一题

- 何为实体：一段以`&`开头，`;`结尾，能够表示Unicode符号的字符串文本
- 作用：为那些不容易通过键盘键入的符号提供了表达的方法
- 注意：实体名称对大小写敏感
- 所有实体的预览地址：`https://dev.w3.org/html5/html-author/charref`

在以上链接中，选中tbody，输入以下代码即可获取所有实体

```js
Array.from($0.querySelectorAll('code')).map(char => char.innerText).filter(Boolean).join('\n')
```

![image-20200413142254788](./Entity.jpg)

### 第二题

ECMAScript Data Types

- [ECMAScript Language Types](https://tc39.es/ecma262/#sec-ecmascript-language-types)
- Undefined
  - Null
  - Boolean
  - String
  - Number
  - Object
  - Symbol
  
- [ECMAScript Specification Types](https://tc39.es/ecma262/#sec-ecmascript-specification-types)
- List and Record
  - Set and Relation
  - Completion Record
  - Reference
  - Property Descriptor
  - Lexical Environment and Environment Record
  - Abstract Closure
  - Data Blocks

### 第三题

#### [URL的语法结构](https://tools.ietf.org/html/rfc3986#section-3)

先贴一个完整版的URL: 

`Scheme://User Information@Host:Port/Path?Query#Fragment`

具体化的URL：`https://zhangsan:lisi@github.com:8080/unshiftio/url-parse?d=1&t=2#anchor`

| 名称             | 描述                 |
| ---------------- | -------------------- |
| Scheme           | 协议                 |
| User Information | 格式为 user:password |
| Host             | IP或主机名称         |
| Port             | 端口                 |
| Hostname         | Host:Port            |
| Origin           | Scheme://Hostname    |
| Path             | 资源路径             |
| Query            | 查询参数             |
| Fragment         | 片段标识             |

#### 解析

##### 方法一

使用`web APIs`的[HTMLAnchorElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLAnchorElement)获取对应属性值。

```js
const url = 'https://zhangsan:lisi@github.com:8080/unshiftio/url-parse?d=1&t=2#anchor'
function urlParse (url) {
    const a = document.createElement('a')
    a.href = url
    return {
        ptotocol: a.protocol,
        username: a.username,
        password: a.password,
        host: a.host,
        port: a.port,
        hostname: a.hostname,
        origin: a.origin,
        path: a.pathname,
        query: a.search,
        hash: a.hash
    }
}
urlParse(url)
```

因在**node环境中没有document对象**，可以使用[URL](https://developer.mozilla.org/en-US/docs/Web/API/URL)方法

```js
function urlParse (url) {
    const urlObj = new URL(url)
    return {
        ptotocol: urlObj.protocol,
        username: urlObj.username,
        password: urlObj.password,
        host: urlObj.host,
        port: urlObj.port,
        hostname: urlObj.hostname,
        origin: urlObj.origin,
        path: urlObj.pathname,
        query: urlObj.search,
        hash: urlObj.hash
    }
}
```

##### 方法二

直接使用`url`的解析库[url-parse](https://github.com/unshiftio/url-parse)

```js
# npm install url-parse
var Url = require('url-parse')
new Url(url)
```

##### 方法三

手写正则解析

```js
const regexp = /^(?<protocol>[^\/?#]+)?\/\/(?<userinfo>(?<username>[^:]*)(?<password>:?.*)@)?(?<hostname>(?<host>[^\/?#:]*):?(?<port>[0-9]+)?)?(?<path>[^?#]*)\\?(?<query>[^#]*)(?<hash>#(?:.*))?/
```

![regex](./regex.jpg)