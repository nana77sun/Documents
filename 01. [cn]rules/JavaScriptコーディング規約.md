#JavaScript 编码规范  

##缩进		
######每一行的层级由4个空格缩进,禁止使用Tab
	// 不好的写法
	if (a && b) {	
      for (i = 0, i < 10; i++) {	
      		alert(i);	
    }	
    }
	// 好的写法  
    if (a && b) {	
        for (i = 0, i < 10; i++) {	
          alert(i);	
        }	
    }	

##行		
######每行不应该超过120个字符,如果一行多余120字符,在运算符前换行,第2行空8个空格	
	// 不好的写法
	callAFunction(document, element, window, "some string value", true, 123,
		navigator);

	callAFunction(document, element, window, "some string value", true, 123
		,navigator);

	var html = "<pThe sum of " + a + " and " + b + " plus " + c
	    + " is " + (a + b + c);
	// 好的写法			
	callAFunction(document, element, window, "some string value", true, 123
			, navigator);

	var html = "<pThe sum of " + a + " and " + b + " plus " + c +
	    " is " + (a + b + c);
######语句必须以分号作为结束符
	// 不好的写法
	var name = "dreamart"
	function sayName() {
		alert(name)
	}
	// 好的写法
	var name = "dreamart";
	function sayName() {
		alert(name);
	}

##空格		
- 运算符前后必须使用一个空格	
- 空行,行尾不要有空格;	
- 逗号和冒号后一定要跟空格;	
- for 循环条件中, 分号后留一空格.运算符前后加空格.	
- 变量声明语句, 数组值, 对象值及函数参数值中的逗号后留一空格
- 小括号内和中括号内不加空格,大括号内加空格.
	
        // 不好的写法
        if(condition) doSomething();
        while(!condition) iterating++;
        for(var i=0;i<100;i++) object[array[i]] = someFn(i);
        var map = { ready: 9,
            when: 4, "you are": 15 };
        // 好的写法
        var i = 0;
        
        if (a  b) {
            doSomething();
        } else if (otherCondition) {
            somethingElse();
        } else {
            otherThing();
        }
         
        while (!condition) {
            iterating++;
        }
         
        for (; i < 100; i ++) {
            object[array[i]] = someFn(i);
        }
         
        try {
            // Expressions
        } catch (e) {
            // Expressions
        }
        
        var map = { ready: 9, when: 4, "you are": 15 };
         
        var map = {
            ready: 9,
            when: 4,
            "you are": 15
        };
        
        var x = a ? b : c;
	
##空行
######适当的空行,能提高代码的可读性.		
- 函数之间
- 函数中局部变量和第一行语句之间
- 多行或单行注释之前
- 逻辑上独立的代码块使用空行分隔

		// 好的写法
		function total() {
		    var i = 100;

		    if (i < 10) {
		    }
		}

		function add() {
		}	

##注释 
######当代码不够清晰,难于理解时添加注释,代码很明了时,不应该追加注释.		
- 单行 描述语句.//后加一空格

		// 不好的写法:注释之前没有空行
		if (condithon) {
		    // 如果代码执行到这里,则表明通过了所有安全性检查
		    allowed();
		} 	
		// 不好的写法:注释没有缩进
		if (condithon) {
		// 如果代码执行到这里,则表明通过了所有安全性检查
		    allowed();
		} 	
		// 好的写法
		if (condithon) {

		    // 如果代码执行到这里,则表明通过了所有安全性检查
		    allowed();
		} 
	
- 多行 描述代码段

		/* 我的注释 */
		/**
		 * 我的注释
		 */

- 文档注释 所有的方法,所有的构造函数,所有包含文档化方法的对象.
 ######文件

		/**
		 * @file Description of file, its uses and information
		 * about its dependencies.
		 * @author dac@dreamarts.com.cn
		 * @copyright DA Corporation. All Rights Reserved.
		 */
 ######Class

		/**
		 * This is a description of the MyClass constructor function.
		 * @class
		 * @classdesc This is a description of the MyClass class.
		 */
		function MyClass() {
		}
 ######函数 param,returns,example

		/**
		 * @param {string} somebody Somebody's name.
		 */
		function sayHello(somebody) {
		    alert('Hello ' + somebody);
		}
		/**
		 * This callback type is called `requestCallback` and is displayed as a global symbol.
		 *
		 * @callback requestCallback
		 * @param {number} responseCode
		 * @param {string} responseMessage
		 */
		/**
		 * Does something asynchronously and executes the callback on completion.
		 * @param {requestCallback} cb - The callback that handles the response.
		 */
		function doSomethingAsynchronously(cb) {
		    // code
		};
		/**
		 * Returns the sum of a and b
		 * @param {Number} a
		 * @param {Number} b
		 * @param {Boolean} retArr If set to true, the function will return an array
		 * @returns {Number|Array} Sum of a and b or an array that contains a, b and the sum of a and b.
		 */
		function sum(a, b, retArr) {
		    if (retArr) {
		        return [a, b, a + b];
		    }
		    return a + b;
		}
		/**
		 * Uploader
		 * @param {Object} config 组件配置（下面的参数为配置项，配置会写入属性，详细的配置说明请看属性部分）
		 * @param {Button} config.button *，Button按钮的实例
		 * @param {Queue} config.queue *，Queue队列的实例
		 * @param {String|Array} config.type *，采用的上传方案
		 * @param {Object} config.serverConfig *，服务器端配置
		 * @param {String} config.urlsInputName *，存储文件路径的隐藏域的name名
		 * @param {Boolean} config.isAllowUpload 是否允许上传文件
		 * @param {Boolean} config.autoUpload 是否自动上传
		 * @example
		 * var uploader = new Uploader({button:button,queue:queue,serverConfig:{action:'test.php'}})
		 */
		function Uploader(config) {
		}
 ######属性 type,const,private,public,protect
		/**
		 * @type {number}
		 * @const
		 */
		var FOO = 1;
		/** @const {number} */
		var FOO = 1;
		/** @type {(string|Array.<string)} */
		var foo;
		/** @type {number} */
		var bar = 1;
		/**
		 * My PrivateDiary.
		 * @private
		 */
		var privateDiary= 2;
		/**
		 * My PublicDiary.
		 * @public
		 */
		var publicDiary= 2;
		/**
		 * My ProtectDiary.
		 * @protect
		 */
		var protectDiary= 2;

 ######tag
 //待续
		
##命名		
######数字,字母,下划线.数字不能开头.禁止其它字符集.采用驼峰命名格式.避免使用没有意义的单词.见名释义
		
- 常量	
所有字母大写,单词之间用下划线隔开

		// 好的写法
		var MAX_COUNT = 10;
		var URL = "http://www.nczonline.net";
		
- 变量	
首字母小写,每个单词首字母大写.第一个单词是名词,不要使用下划线.布尔型变量前可以使用动词.

		// 好的写法
		var count = 10;
		var myName = "dreamarts";
		var found = true;
		var isFound = true;
		// 不好的写法
		var getCount = 10;

		
- 函数	
首字母小写,每个单词首字母大写.第一个单词是动词,不要使用下划线.
常用动词 can,has,is,get,set

		// 好的写法
		function getName() {
		    return myName;
		}
		// 不好的写法
		function theName() {
		    return myName;
		}
		
- 构造函数	
首字母大写.非动词开头.

		// 好的写法
		function Person(name) {
		    this.name = name;
		}

- 私有变量	
		
- 私有函数	
		
- 保护变量	
		
- 保护函数	
		
- 参数 参数后面加"_".	
字符  
数值   
数组  
对象   
可选参数   
参数个数不固定  
		
- 文件名	 应全部使用小写字符, 且不包含除"_"外的标点符号
		
- 临时的重复变量	
		以 i, j, k, ..., 命名
		
##声明
######声明变量必须加上var关键字,可以多个变量共用一个var.
- 常量 禁止使用const,因为IE不能识别

- 字符串	
字符串使用双引号定义,换行禁止使用"\"

		var name = "Hello World!";
		var name = "Hello" + "World!";
					
- 数值	
尽量使用十进制,十六进制.禁止使用八进制.小数点前后至少保留一位数字

		// 好的写法
		// 整数
		var count = 10;
		// 小数
		var price = 10.0;
		var price = 10.00;
		// 十六进制
		var num = 0xA2;
		// 不好的写法
		var price = 10.;
		var price = .1;
		// 八进制
		var num = 010;
		
- 数组

		// 不好的写法
		var colors = new Array("red", "green", "blue");
		var numbers = new Array(1, 2, 3, 4);
		// 好的写法
		var colors = ["red", "green", "blue"];
		var numbers = [1, 2, 3, 4];	
		
- 对象	
直接声明对象的属性

		// 不好的写法
		var book = new Object();
		book.title = "JavaScript";
		book.author = "dreamarts";
		// 好的写法
		var book = {
			title: "JavaScript",
			author: "dreamarts"
	    };
		
- 函数

		// 不好的写法
		function DoSomething() {
		}
		// 好的写法
		function doSomething() {
		}	

##语句		
		
- 赋值

		// 不好的写法
		var flag = 1 < count;
		// 好的写法
		var flag = (i < count);	
		
- 等号运算符	===,!== 替代 ==, != 避免弱类型转换错误

		// 不好的写法
		var same = (a == b);
		// 好的写法
		var same = (a === b);
		
- 三元操作符	仅用在条件赋值语句中

		// 不好的写法
		condition ? doSomething() : doSomethingElse();
		// 好的写法
		var value = condition ? value1 : value2;
		
- 简单语句 每行最多包含一条语句

		// 不好的写法
		count++; a = b;
		// 好的写法
		count++;
		a = b;
		
- 返回语句

		//好的写法
		return;
		return collection.size();
		return (size  0 ? size : defaultSize);
			
- if语句	 不允许省略大括号

		if (condition) {
		    doSomething();
		}

		if (condition) {
		    doSomething();
		} else {
		    doSomethingElse();
		}
		
- for语句
		for (i = 0; i < 10; i ++) {
		    // 代码
		}
		
		for (variable in object) {
		    // 代码
		}	
		
- while语句

		while (condition) {
		    // 代码
		}	
		
- do语句

		do {
		    // 代码
		} while (condition);
		
- switch语句

		switch (expression) {
		  case expression:
		    // 代码
		   
		  default:
		    // 代码
		}
		// 好的写法
		switch (value) {
		  case 1:
		    /* falls through */

		  case 2:
		    doSomething();
		    break;

		  case 3:
		    return true;

		  default:
		    throw new Error("Error");
		}
		
- try语句

		try {
		    // 代码
		} catch (variable) {
		    // 代码
		} finally {
		    // 代码
		}	
		
##最佳实践
---
- 用===,!== 取代 ==,!=,防止类型转换.
- for-in 语句,hasOwnProperty判断必要.	???	
- 不要在块内声明函数

		if (x) {
		    function foo() {}
		}
	
- 不要封装基本类型 number, string 或 boolean

 	    var x = new Boolean(false);
		if (x) {
  	  	    alert('hi');  // Shows 'hi'.
		}

- 禁止使用 with 	
- 减少使用 continue 和 break 	
- 仅在函数内使用 this	
- 禁止修改内置对象的原型	
- 使用 Array/Object 直接量, 避免使用 Array/Object 构造器
- True 和 False 布尔表达式
 下面的布尔表达式都返回 false:  

        null   
        undefined   
        '' 空字符串   
        0 数字0
   
 都返回 true:   

        '0' 字符串0   
        [] 空数组  
        {} 空对象   
例:

		// 不好的写法
		while (x != null) {
		}
		if (y != null && y != '') {
		}
		// 好的写法
		while (x) {
		}
		if (y) {
		}

- 条件语句中,禁止写函数

		// 不好的写法
		if (user.isAdmin() || user.isModerator()) {
		  console.log('losing');
		}
		// 好的写法
		var isAuthorized = (user.isAdmin() || user.isModerator());
		
		if (isAuthorized) {
  		  console.log('winning');
		}

- 避免if 深层嵌套

		// 不好的写法
		function isPercentage(val) {
		    if (val = 0) {
		        if (val < 100) {
		            return true;
		        } else {
		            return false;
		        }
		    } else {
		        return false;
		    }
		}
		// 好的写法
		function isPercentage(val) {
		    if (val < 0) {
		        return false;
		    }
		
		    if (val = 100) {
		        return false;
		    }
		
		    return true;
		}
		// 更好的写法
		function isPercentage(val) {
		    var isInRange = (val = 0 && val < 100);
		    return isInRange;
		}

- 类型check 禁止使用typeof 检测null,因为返回值是object
 原始类型

		// 检测字符串
		if (typeof name === "string") {
		    anotherName = name.substring(3);
		}
		
		// 检测数字
		if (typeof count === "number") {
		    updateCount(count);
		}

		// 检测布尔值
		if (typeof found === "boolean" && found) {
		    message("Found");
		}
		
		// 检测undefined
		if (typeof myApp === "undefined") {
		    myApp = {
		    };
		}
		
 引用类型
 
		console.log(typeof null); //"object"
		console.log(typeof {}); //"object"
		console.log(typeof []); //"object"
		console.log(typeof new Date()); //"object"
		console.log(typeof new RegExp()); //"object"
		
		// 检测日期
		if (value instanceof Date) {
		    console.log(value.getFullYear());
		}
		
		// 检测正则表达式
		if (value instanceof RegExp) {
		    if (value.test(anotherValue)) {
		        console.log("Matches");
		    }
		}
		
		// 检测Error
		if (value instanceof Error) {
		    throw value;
		}

检测函数

		// 检测函数 
		function myFunc() {}
		console.log(typeof myFunc === "function"); // true
		
		// IE8 以前 DOM对象的检测
		if ("querySelectorAll" in document) {
		    images = document.querySelectorAll("img");
		}
		
检测数组

		// 检测数组
		function isArray(value) {
		    // ECMAScript5 增加了Array.isArray函数
		    if (typeof Array.isArray === "function") {
		        return Array.isArray(value);
		    } else {
		        return Object.prototype.toString.call(value) === "[object Array]";
		    }
		}

检测属性   

		// 不好的写法: 检测假值
		if (object[propertyName]) {
		    // 代码
		}
		// 不好的写法: 和null比较
		if (object[propertyName] != null) {
		    // 代码
		}
		// 不好的写法: 和undefined比较
		if (object[propertyName] != undefined) {
		    // 代码
		}
		//---上面的代码,是通过给定的名字来检查属性的值,而非判断给定的名字所指的属性是否存在.
		//---0,""(空字符串),false,null,undefined 都会返回false
		// 好的写法
		var object = {
		    count:0,
		    related: null
		};
		
		if ("count" in object) {
		    // 代码
		}
		
		// 不好的写法
		if (object["count"]) {
		    // 这里的代码不会执行
		}
		
		// 不好的写法
		if (object["related"] != null) {
		    // 这里的代码不会执行
		}
		
		// 好的写法
		if ("related" in object) {
		    // 代码会执行
		}
		
		// 对于非DOM对象,检查实例对象的属性
		if (object.hasOwnProperty("related")) {
		    // 代码
		}
		
		// 所有对象
		if ("hasOwnProperty" in object && object.hasOwnProperty("related")) {
		    // 代码
		}

- Named closures
Feel free to give your closures a name. It shows that you care about them, and will produce better stack traces:

		// 不好的写法
		req.on('end', function() {
		    console.log('losing');
		});
		// 好的写法
		req.on('end', function onEnd() {
		    console.log('winning');
		});

- Nested Closures
Use closures, but don't nest them. Otherwise your code will become a mess.

		// 不好的写法
		setTimeout(function() {
	        client.connect(function() {
	    	  console.log('losing');
		    });
		}, 1000);
		// 好的写法
		setTimeout(function() {
		    client.connect(afterConnect);
		}, 1000);

		function afterConnect() {
		    console.log('winning');
		}

- 配置数据(hardcoded),从代码中分离
URL  
需要展现给用户的字符串  
重复的值  
设置  
任何可能发生变更的值

- 对象继承
- 类继承
##Sample 代码
---
