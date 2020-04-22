## 作业：

- 写一个正则表达式 匹配所有 Number 直接量
- 写一个 UTF-8 Encoding 的函数
- 写一个正则表达式，匹配所有的字符串直接量，单引号和双引号



### 第一题

1. 整数 `/^-?[0-9]+$/`

2. 浮点数：`/^-?[0-9]*\.[0-9]+$/`

3. 十六进制：`/^0[xX][0-9a-fA-F]+$|^[0-9a-fA-F]+$/`

4. 二进制：`/^0[bB][01]+$|^[01]+$/`

5. 八进制：`/^0[oO][0-7]+$|^[0-7]+$/`

6. 整体匹配：

   ```js
   const regex = /(?<int>^-?[0-9]+$)|(?<float>^-?[0-9]*\.[0-9]+$)|(?<hex>^0[xX][0-9a-fA-F]+$|^[0-9a-fA-F]+$)|(?<binary>^0[bB][01]+$|^[01]+$)|(?<octal>^0[oO][0-7]+$|^[0-7]+$)/
   ```

### 第二题

```js
// UTF-8 Encoding
const utf8Encode = (str) => {
    str = encodeURIComponent(str)
    const bytes = []
    let i = 0
    while (i < str.length) {
        let code = str.charCodeAt(i++)
        // 当字符为%时
        if (code === 37) {
            bytes.push(parseInt(str.substr(i, 2), 16))
            i += 2
        } else {
            bytes.push(code)
        }
    }
    return new Uint8Array(bytes)
}
// UTF-8 decoding
const utf8Decode = (bytes) => {
    let str = ''
    for (let b of bytes) {
        str += '%' + b.toString(16)
    }
    return decodeURIComponent(str)
}
```

### 第三题

```js
const regex = /'.+?'|".+?"|`.+?`/
```

