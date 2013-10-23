----
#### 文件夹结构
.gitignore
.npmignore
LICENSE
README.md
bin
doc
examples
lib
man
package.json
src
test


 - routes
 - api
 - controllers
 - modules
 > 1. **文件名** mod_ 开头，不用复数型 ex. mod_group.js, mod_user.js
 > 1. **Schema** 要明确字段的type和description，需要包含以下5个方法
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

 > 1. **删除** 所有的删除操作，都进行逻辑删除，而不是物理删除
 > 1. **其他** 对参数的转换，变化等操作及对结果的共通的过滤等操作，不写业务逻辑

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
  提高可读性，降低参与门槛

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
#### 测试脚本
 - **文件命名** 
 - **** 

----
Travis CL

----
#### 其他
 - **引号** 代码中统一使用双引号，不使用单引号
 - **callback** 调用时，需要写返回语句 return callback(err, result); 明确函数调用的结束，也避免误执行后续代码

 - **顺序** 文件内变量声明 - exports方法 - 私有方法的顺序


