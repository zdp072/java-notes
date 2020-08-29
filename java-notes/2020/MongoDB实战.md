## mongodb数据逻辑结构
- 由文档(document)、集合(collection)、数据库(database)等三部分组成。
- 文档 - document，相当于关系型数据库中的一行记录。
- 集合 - collection，相当于关系型数据库的表。
- 一个MongoDB实例支持多个数据库database。

## mongodb增删操作

### 表操作
- db.createCollection('mytest'); # 建表
- db.mytest.drop();  # 删除表

### 数据插入操作
- 语法：db.collectionName.insert(document)
- 不指定文档的id，数据库会默认分配一个随机id
`db.mytest.insert({name:'zhangsan', age:23, sex:'f'});`
- 指定文档的id，插入单个文档
`db.mytest.insert({_id:5,name:'zhaos',age:23,sex:'f'});`
- 插入多个文档
`db.mytest.insert([{_id:2,name:'zhangs',age:21,sex:'m'},{_id:3,name:'wangw',age:22,sex:'m'},{_id:4,name:'zhaos',age:23,sex:'f'}]);`


### 数据删除操作
- 语法：db.collection.remove(查询表达式, 选项)。选项是指需要删除的文档数，默认是0，删除全部文档
- 将所有_id=7的文档删除
`db.mytest.remove({_id:7})`

- 将gender:'m'的所有文档删除
`db.mytest.remove({gender:'m'})`

- 只删除一个gender:'m'的文档，num是指删除的文档数
`db.mytest.remove({gender:'m'},1)`


### 数据修改操作
- 语法：db.collection.update(查询表达式, 新值);

- 下面写法只是在替换一个文档，并非修改一个文档字段，其他字段没了
`db.mytest.update({name:'zhangs'},{name:'liul'})`

- 修改文档某列的值，必须使用$set:{属性:'值'}
`db.mytest.update({name:'zhaos'},{$set:{name:'kongkong'}})`

- $unset 删除某个列
`db.mytest.update({name:'kongkong'},{$unset:{name:'kongkong'}})`

- $rename 重命名某个列
`db.mytest.update({_id:6},{$rename:{sex:'gender'}})`
`db.mytest.update({},{$rename:{'sex':'gender'}},{multi:true})`

- $inc 增长某个列
`db.mytest.update({_id:6},{$inc:{age:2}})`

### 数据查找操作
- 语法: db.collection.find(查询表达式, 显式查询的列)
- 查询一个表中的所有文档    
`db.mytest.find()`

- 查询特定属性的文档
`db.mytest.find({_id:3})`

- 查询所有文档，显示gender列，不显示id
`db.mytest.find({},{gender:1, _id:0})`

- 查询所有gender:'m'的文档,显示gender列,age列,不显示id
`db.mytest.find({gender:'m'},{gender:1, _id:0, age:1})`

### 数据高级查找
- not equal 不等于 $ne ---> != 查询表达式 （查询age不等于25的文档）
`db.mytest.find({age:{$ne:25}})`

- great than 大于  $gt ---> >  （查询age大于25的文档）
`db.mytest.find({age:{$gt:20}})`

- great than equal 大于等于 $gte ---> >=  （查询age大于等于25的文档）
`db.mytest.find({age:{$gte:25}})`

- less than 小于  $lt ---> <=  （查询age小于25的文档）
`db.mytest.find({age:{$lt:25}})`

- less than equal 小于等于 $lte ---> <=  （查询age小于等于25的文档）
`db.mytest.find({age:{$lte:25}})`


- $in --> in  (查询age为20和25的文档)
`db.mytest.find({age:{$in:[20,25]}})`

- $nin --> not in  (查询age不为20和25的文档)
`db.mytest.find({age:{$nin:[20,25]}})`


- $or  -->  {$or:[v1,v2..]}  是指取出field列是一个数组,且至少包含 v1,v2值
`db.mytest.find({$or:[{age:{$gte:30}},{name:"Zhaos"}]})`


- $and  --> {$and:[{<operator-expression>},{<operator-expression>}..]}是指取出field列是一个数组,且至少包含v1,v2值
`db.mytest.find({$and:[{age:{$lte:30}},{age:{$gte:5}}]})`


- $not  --> {field:{$not:{ <operator-expression> }}}是指取出field列是一个数组,且至少包含v1,v2值
`db.mytest.find({age:{$not:{$gt:25}}})`

- $all  --> {field:{$all:[v1,v2..]}} 是指取出field列是一个数组,且至少包含v1,v2值
`db.mytest.find({age:{$all:[30]}})`

- $exists  --> {field:{$exists:1}}  查询出含有field字段的文档

- 查询含有age列的文档
`db.mytest.find({age:{$exists:1}})`

- $mod  --> {field:{$mod:[ divisor(除数), remainder(余数)]}}  查询出含有mod字段的文档

- 查询含有age列的文档
`db.mytest.find({_id:{$mod:[5,0]}})`


- $nor  --> {$nor,[条件1,条件2]}  是指所有条件都不满足的文档为真返回, 查询所有age不为30，gender不为f的文档
`db.mytest.find({$nor:[{age:30},{gender:'f'}]})`


- 正则表达式查询, 查询所有以name:yang开头的文档 /patern/
`db.mytest.find({name:/yang*/})`
- 正则表达式查询, 查询所有以name:zhao开头的文档,且不区分大小写 /patern/i
`db.mytest.find({name:/zhao/i})`

- $where  查询age>6,且age<22的文档
`db.mytest.find({$where:"this.age>6" && "this.age<=22"})`