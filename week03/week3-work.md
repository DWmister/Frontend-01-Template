## 本周作业

- JavaScript | 表达式，类型准换
  - 根据这节课上讲师已写好的部分，补充写完函数 convertStringToNumber
  - 以及函数 convertNumberToString
- JavaScript | 语句，对象
  - 根据课上老师的示范，找出 JavaScript 标准里所有的对象，分析有哪些对象是我们无法实现出来的，这些对象都有哪些特性？写一篇文章，放在学习总结里。



### 第一题

```js
/**
 * 转number类型为string类型
 * @param number  数字
 * @param hex     进制
 */
const maps = new Map().set(10, 'A').set(11, 'B').set(12, 'C').set(13, 'D').set(14, 'E').set(15, 'F')
const convertNumberToString = (number: number, hex = 10) => {
    if (hex === 1) {
        return false
    }
    // number的整数部分
    let integer = Math.floor(number)
    // 整数部分的转换结果
    let int_result = ''
    while (integer) {
        let remainder: number | string = integer % hex
        if (hex === 16 && remainder > 9) {
            remainder = maps.get(remainder)
        }
        int_result = remainder + int_result
        integer = Math.floor(integer / hex)
    }

    // number的小数部分
    let fraction: number | RegExpMatchArray | null = String(number).match(/\.\d*$/)
    // 小数部分的转换结果
    let fra_result = ''
    if (fraction) {
        fraction = +fraction[0].substr(1)
        while (fraction) {
            let remainder: number | string = fraction % hex
            if (hex === 16 && remainder > 9) {
                remainder = maps.get(remainder)
            }
            fra_result = remainder + fra_result
            fraction = Math.floor(fraction / hex)
        }
        return `${int_result}.${fra_result}`
    }

    return int_result
}

```

### 第二题

```js
function convertStringToNumber(str, type){
    // default convert string to decimal
	if(arguments.length < 2){
		type = 10;
	}
	var chars = str.split('');
	var number = 0;
	var i = 0;
	if(type <= 10){
		while(i < chars.length && chars[i] != '.'){
			number *= type;
			number += chars[i].codePointAt(0) - '0'.codePointAt(0);
			i ++
		}
		// jump the point
		if(chars[i] == '.'){
			i ++
		}
		var fraction = 1;
		while(i < chars.length){
			fraction /= type;
			number += (chars[i].codePointAt(0) - '0'.codePointAt(0)) * fraction;
			i ++
		}
	}else if(type <= 16){
		var hexTable = {
			'0':0,
			'1':1,
			'2':2,
			'3':3,
			'4':4,
			'5':5,
			'6':6,
			'7':7,
			'8':8,
			'9':9,
			'a':10,
			'b':11,
			'c':12,
			'd':13,
			'e':14,
			'f':15,
		};
		while(i < chars.length){
			number *= type;
			number += hexTable[chars[i].toLowerCase()];
			i ++
		}
	}
	return number ;
}
```

### 第三题

#### js中特殊对象

- Function Object

  - [[call]] 视为函数Function
  - [[Construct]] 可以被new 操作符调用，根据new的规则返回对象。

- Array Object

  - [[DefineOwnProperty]]

    - Property == length

      设置对象的length属性，根据length的变化对对象进行操作

      newLength > length 用空扩充数组

      newLength < length 截取数组

- String Object

  string的length是不可写不可配的。

- Arguments Object

  [[callee]] 视为函数参数对对象，伪数组 caller

- Object

  [[Get]] property被访问时调用 get

  [[Set]] property被赋值时调用 set

  [[GetPrototypeOf]] 对应getPrototypeOf方法 获取对象原型

  [[SetPrototypeOf]] 对应setPrototypeOf方法 设置对象原型

  [[GetOwnProperty]] getOwnPropertyDescriptor 获取对象私有属性的描述列表

  [[HasProperty]] hasOwnProperty 私有属性判断

  [[IsExtensible]] isExtensible对象是否可扩展

  [[PreventExtensions]] preventExtension控制对象是否可以添加属性

  [[DefineOwnProperty]] defineProperty 定义对象属性

  [[Delete]] delete 操作符

  [[OwnPropertyKeys]] Object.keys() Object.entries() Object.values()

  [[Call]] 能够调用call

- Module Namespece

  [[Module]] 视为一个引入的模块

  [[Exports]] 视为一个导出的模块