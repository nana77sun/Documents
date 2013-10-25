##JSHint
###简介
js静态代码检测工具

###使用
为了生成可视化报告,使用plato插件(内置JSHint插件).
https://github.com/es-analysis/plato

1.npm install -g plato  
2.在被检测的JS文件目录下,定义.jshintrc文件,  
3.plato -r -d report -l .jshintrc api  

命令行参数

	Usage : plato [options] file1.js file2.js ... fileN.js
	  -h, --help
	      Display this help text.
	  -q, --quiet
	      Reduce output to errors only
	  -v, --version
	      Print the version.
	  -x, --exclude : String
	      File exclusion regex
	  -d, --dir : String *required*
	      The output directory
	  -r, --recurse
	      Recursively search directories
	  -l, --jshint : String
	      Specify a jshintrc file for JSHint linting
	  -t, --title : String
	      Title of the report
	  -D, --date : String
	      Time to use as the report date (seconds, > 9999999999 assumed to be ms)
例:plato -r -d report -l .jshintrc -t "My Awesome App" -x .json routes/*.js

###yukari配置文件(.jshintrc)
	{
	    // YUKARI
	    // Enforcing,默认(false)不进行检查,true时检查
	    "bitwise"       : true,//禁止使用位运算符
	    "camelcase"     : true,//强制变量名使用驼峰式风格或者大写字母加下划线风格
	    "curly"         : true,//条件和循环语句中使用大括号
	    "eqeqeq"        : true,//使用===和!==，而不是==和!=
	    "ec3"           : false,//符合ECMAScript3规范(IE6,7,8)
	    "forin"         : true,//使用forin检查对象属性
	    "immed"         : true,//不允许定义一个匿名函数，并立即执行
	    "indent"        : 2,//缩进2空格
	    "latedef"       : true,//变量先定义,再使用
	    "newcap"        : true,//构造函数的名称以大写字母开头
	    "noarg"         : true,//禁止使用arguments.caller和argument.callee
	    "noempty"       : true, //不要使用空代码块
	    "nonew"         : true,//禁止使用new构造对象
	    "plusplus"      : false,//++,--的使用
	    "quotmark"      : "double",//引号都使用双引号
	    "undef"         : true,//禁止使用不声明的变量
	    "unused"        : true,//禁止有没有被使用的变量
	    "strict"        : true,//运行Strict mode
	    "trailing"      : true,//禁止代码行最后有空格
	    "maxparams"     : false,//设置函数最多允许的参数个数
	    "maxdepth"      : false,//设置大括号最大的嵌套次数
	    "maxstatements" : false,//设置每个函数允许的最多语句
	    "maxcomplexity" : false,//代码复杂度,TODO不理解
	    "maxlen"        : 120,//每行代码最大长度
	    // Relaxing,默认(false)进行检查,true时,不检查
	    "asi"           : false,//行尾写分号
	    "boss"          : false,//比较时不能出现赋值语句
	    "debug"         : false,//禁止使用debug语句
	    "eqnull"        : false,//禁止和null判断
	    "esnext"        : false,//禁止使用ECMAScript 6语法
	    "evil"          : false,//禁止使用evil
	    "expr"          : false,//TODO不理解,期望出现赋值语句或函数调用时，出现表达式是否警告
	    "funcscope"     : false,//禁止在控制语句里,生命变量,在作用域外使用
	    "globalstrict"  : true,//允许global strict mode
	    "iterator"      : false,//禁止使用__iterator__属性
	    "lastsemic"     : false,//禁止语句后面没有分号
	    "laxbreak"      : false,//禁止使用不安全的换行
	    "laxcomma"      : true,//允许使用前置逗号风格
	    "loopfunc"      : false,//禁止在循环里使用函数
	    "moz"	    : true,//Mozilla JavaScript extensions
	    "multistr"      : false,//禁止使用多行字符换,用\
	    "proto"         : false,//禁止使用__proto__属性
	    "scripturl"     : false,//TODO不理解
	    "smarttabs"     : false,//禁止tab和空格混用
	    "shadow"        : false,//禁止声明其他地方已经声明过的变量
	    "sub"           : false,//使用persion.name而不是persion['name']
	    "supernew"      : false,//TODO不理解
	    "validthis"     : false,//禁止在strict mode的非构造函数中使用this
	    // Environments,表示是否是运行在所指的环境下
	    "browser"       : true,//浏览器环境
	    "couch"         : false,//CouchDB环境
	    "devel"         : true,//开发环境
	    "dojo"          : false,//dojo环境
	    "jquery"        : true,//jquery
	    "mootools"      : false,//jquery
	    "node"          : true,//node环境
	    "nonstandard"   : false,//是否使用非标准方法，比如escape和unescape
	    "prototypejs"   : false,//Prototyps
	    "rhino"         : false,//Rhino环境
	    "worker"        : false,//Web Worker环境
	    "wsh"           : false,//Windows Script Host环境
	    "yui"           : false,//yui环境
	    "globals"       : {"describe": false, "it": false}
	}
	
###配置文件属性说明
系统默认配置文件.jshintrc  
JSHint的检测模式有四种：强制，放松，环境，遗留（Legacy）
######强制
选项设置为true或指定的值,则会在校验时显示此警告(默认不显示警告).

- 	bitwise  
禁止在js中使用位运算符，^ (XOR), | (OR) 容易和 &，￥￥混淆。
- 	camelcase  
变量名使用驼峰式风格或者大写字母加下划线风格
- 	curly  
条件和循环语句中使用大括号

	 	while(day)
	 		shuffle();

- 	eqeqeq   
总是使用===和!==，而不是==和!=
- 	es3  
符合ECMAScript 3规范 IE6,7,8
- 	forin   
必须使用hasOwnProperties过滤元素
   
	 	for (key in obj) {
	  		if (obj.hasOwnProperty(key)) {
	    	// We are sure that obj[key] belongs to the object and was not inherited.
	  		}
		}

- 	immed  
如果是true，则不允许定义一个匿名函数，并立即执行

		(function(){
		//
		}());
		//不好的写法
		(function(){
		//bla bla
		})();
- 	indent  
使用4个空格缩进。indent:4
- 	latedef  
变量应该先定义，再使用
- 	newcap  
构造函数的名称应该以大写字母开头
- 	noarg  
禁止使用arguments.caller and arguments.callee
- 	noempty  
不要使用空代码块
- 	nonew  
***This option prohibits the use of constructor functions for side-effects. Some people like to call constructor functions without assigning its result to any variable:***

		new MyConstructor();
- 	plusplus  
禁止使用递增，递减运算符.++,--
- 	quotmark  
设定值：true(引号保持一致),single(单引号),double(双引号)
- 	undef  
使用不声明的变量时，警告
- 	unused  
声明的变量不使用时，警告
- 	strict  
要求代码运行于Strict mode
- 	trailing   
代码行最后留有空格,警告
- 	maxparams  
函数允许的参数个数最大值
- 	maxdepth  
函数允许的最大深度
- 	maxstatements  
函数允许的语句条数最大值
- 	maxcomplexity  
最大循环复杂度
- 	maxlen  
设置每行代码最大长度
######放松
选项设置为true表示忽略此警告(默认显示警告).

- asi  
  如果是true，JSHint会无视没有加分号的行尾， 自动补全分号一直是Javascript很有争议的一个语法特性。默认，JSHint会要求你在每个语句后面加上分号，但是如果你认为自己理解了asi(automatic semicolon insertion)，你可以抛弃JSHint对分号的检查。
- boss  
如果为true，那么JSHint会允许在if，for，while里面编写赋值语句。 一般来说，我们会在循环、判断等语句中加入值的比较来做语句的运行条件，有时候会把==错写成赋值的=，通常，JSHint会把这个认定为一个错误，但是开启这个选项的化，JSHint就不会检查判断条件中的赋值 
- debug  
如果为true，JSHint会允许代码中出现debugger的语句。????
- eqnull  
如果为true，JSHint会允许使用"== null"作比较。 == null 通常用来判断一个变量是undefined或者是null（当时用==，null和undefined都会转化为false）。
- esnext  
如果为true,JSHint允许使用ECMAScript 6规范的语法,
- evil  
如果为真，JSHint会允许使用eval
- expr  

- funcscope
- globalstrict
- iterator  
__iterator__属性不是所有浏览器都支持,使用时注意
- lastsemic  
缺少分号  

		var name = (function() { return 'Anton' }());

- laxbreak  
如果为真，JSHint则不会检查换行。
Javascript会通过自动补充分号来修正一些错误，因此这个选项可以检查一些潜在的问题。
- laxcomma
comma-first coding style

		var obj = {
		    name: 'Anton'
		  , handle: 'valueof'
		  , role: 'SW Engineer'
		};
- loopfunc  
循环语句里,禁用函数.
- multistr  
字符串跨行定义时,连接符或者空格的检查

		/*jshint multistr:true */
		
		var text = "Hello\
		World"; // All good.
		
		text = "Hello
		World"; // Warning, no escape character.
		
		text = "Hello\
		World"; // Warning, there is a space after \
- proto   
\__proto\__属性检查
- scripturl  
不明白?
- smarttabs  
tab和空格混用检查
- shadow  
[]符号检查.当在.标记法中出现时person['name'] vs. person.name.
- sub
- supernew
- validthis  
禁止在strict mode的非构造函数中使用this
######环境
These options let JSHint know about some pre-defined global variables.

- browser
- couch
- devel
- dojo
- jquery
- mootools
- node
- nonstandard
- phantom
- prototypejs
- rhino
- worker
- wsh
- yui
- globals  
当，代码中使用了全局对象时，jihint会报没有定义的错误，这是可以在globals里定义来越过该检查
######环境
These options are deprecated and will be removed soon. DO NOT use them.

- nomen
- onevar
- passfail
- white

