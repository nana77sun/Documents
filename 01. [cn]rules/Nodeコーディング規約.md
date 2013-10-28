----
#### 代码目录结构
 - .gitignore
 - .npmignore
 - LICENSE
 - README.md
 - bin
 - doc
 - examples
 - lib
 - man
 - package.json
 - src
 ====
 - test
  - 写测试代码的注意事项
  测试对象代码，需要引用coverage目录下的文件，而非原始代码文件

  >     var _       = require("underscore")
  >       , should  = require('should')
  >       , company = require("../../coverage/modules/mod_company");

  - 测试代码使用的数据库，与生产环境的数据库是独立的。可以在配置文件的testdb节进行配置

  >       "testdb": {
  >           "host": "mongo"
  >         , "port": 27017
  >         , "dbname": "developer"
  >         , "pool": 5
  >       }

  - 测试，并生成覆盖率报告(该命令会执行test目录下的全部测试代码，并生成报告)

  >     # node tools/run_test.js

  - 当测试代码有问题，需要调试时，可以直接使用mocha执行测试代码

  >     # mocha test/*

 - routes
 - api
 - controllers
 ====
 - modules
 > 1. **文件名**  
  mod_ 开头，不用复数型 ex. mod_group.js, mod_user.js
 > 1. **Schema**  
  要明确字段的type和description，需要包含以下5个方法
 createat | 创建日
 createby | 创建者
 editat   | 最终编辑日
 editby   | 最终编辑者
 valid    | 有效
 > 1. **通用方法的命名**  
 get      | 使用_id获取一条记录
 getList  |
 add      | 添加
 update   | 更新
 remove   | 删除
 total    | 件数

 > 1. **删除**  
  所有的删除操作，都进行逻辑删除，而不是物理删除
 > 1. **其他**  
  对参数的转换，变化等操作及对结果的共通的过滤等操作，不写业务逻辑

 - views
 - public
 - core
 - injections
 - config
 - locales
 - logs
 - tools


----
#### nodejs编写风格
 - 面向对象的编程
  通常，我们的代码使用面向对象的编程风格，来提高可读性，降低参与门槛。

 - 基于原型的编程
  为了开发时易于使用，工具类共通类等，用可以使用基于原型的方法开发

----
#### 引用外部Module
 - 为了使代码依赖的外部包一目了然，require要集写在文件头中，禁止在代码途中使用。
 - 对个require的等号，要对齐
 - 外部包的引用顺序
  1. 第三方包
  2. 其他文件夹的代码文件
  3. 本文件夹的其他代码文件


----
#### 单元测试工具&报告生成原理
 - 测试工具
  - 单元测试框架 使用mocha
  >  http://visionmedia.github.io/mocha/
  >    #npm install -g mocha

  - 测试断言 使用should
  >  https://github.com/visionmedia/should.js

  - 代码覆盖率 使用jscoverage
  >  https://github.com/fishbar/jscoverage
  >    # npm install -g jscoverage

 - 报告生成原理
  1. 用jscoverage对源代码进行转换，这些转换后的代码可统计被执行的代码行数
  2. 用mocha对转换过的代码进行测试
  3. 根据上两步生成的统计的数据，用mocha生成覆盖率报告  
  **注意：** 为了保证经jscoverage转换的代码是最新的，  
  run_test会每都删除coverage目录，并重新生成coverage代码

 - 相关目录结构
  - coverage/ 用于保存coverage中间代码
  - coverage/coverage.html 覆盖率报告文件
  - test/ 测试代码存放目录
  - tools/run_test.js 执行测试并生成报告的脚本，为了跨平台需要用node启动

----
Travis CL

----
#### 其他
 - **引号**  
 代码中统一使用双引号，不使用单引号

 - **callback**  
 调用时，需要写返回语句 return callback(err, result); 明确函数调用的结束，也避免误执行后续代码

 - **代码顺序**  
 文件内变量声明 - 私有方法 - exports方法

