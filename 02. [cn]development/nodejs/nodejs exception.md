Nodejs 异常处理
====================

异步处理原则
---------------------
#### 思路
1. API层，生成Handler实例，并向后续函数传递
2. 通常的程序捕获的异常，通过Handler明确的emit出去，然后由API层捕获并返回
2. 没有捕获的非异步异常，会由Express的错误处理函数捕获，并返回
3. 异步异常，或有可能产生异步异常的地方，要用domain捕获，捕获之后返回并杀掉当前进程
4. node进程的重启依靠forever的重启功能，NGINX配置成不能访问时，对其他的AP做请求

#### 根据Nodejs官方文档对Domain的描述，产生异常时会有以下问题。最安全的方法，还是结束进程。

 - without leaking references.  参照リーク
 - creating some other sort of undefined brittle state. 未定義の脆弱な状態

#### 关于Cluster

利用nodejs的cluster，也可以实现自动启动新worker的功能，但鉴于cluster还处于
Stability: 1 - Experimental阶段，所以暂时不采用。

**********


关于Handler
---------------------
#### Handler带有一下信息
 1. domain
 2. event
 3. parameter（body + query），允许追加内容
 4. session

**********


参考：常见的异常方式
---------------------

#### Exception 异步异常产生方式的例子
	try {
	    setTimeout(function () {
	        throw new Error('who will catch me?');
	    }, 1);
	} catch (e) {
	    console.log('not me');
	}
	
#### Domains 通过Nodejs的Domain控制异常（Domain还处于Stability: 2 - Unstable级别）
	var mainDomain = domain.create();
	mainDomain.run(function() {
	    fs.readFile(filename, 'utf8', mainDomain.intercept(function(data) {
	        return cb(null, JSON.parse(data));
	      }));
	});
	mainDomain.on("error", function(error){
	    console.error(error);
	})
	
#### EventEmitters 通过消息机制传递异常
	var util = require('util'),
	  EventEmitter = require('events').EventEmitter;

	var MyClass = function () {
	  if (!(this instanceof MyClass)) return new MyClass();
	  EventEmitter.call(this);
	};
	util.inherits(MyClass, EventEmitter);
	
#### Express.js 带有4个参数，可以捕获非异步异常
	app.use(function(err, req, res, next){
	  console.error(err.stack);
	  res.send(500, 'Something broke!');
	});



