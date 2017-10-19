mongodb语法（极简例子）
------------
1. 创建或切换到数据库
    use testDb;  //当前没有testDb数据库，则创建名为testDb的数据库
2. 删除数据库
    db.dropDatabase(); //注意删除前先切换数据库
3. 删除集合
    db.testTable.drop(); //删除数据库中名为testTable的集合
4. 往集合中插入文档
    db.testTable.insert({testField:'test'}); //往集合testTable中插入文档{testField:'test'}
5. 更新文档
    db.testTable.update({testField:'test'},{$set:{testField:'hello world!'}});
6. 删除文档
    db.testTable.remove({testField:'hello world!'}, 1); //删除testField='hello world!'的第一条文档，去掉第二个参数1则删除多条
    db.testTable.remove({}); //删除所有文档
7. 查询文档
    db.testTable.find();
    db.testTable.findOne();
8. 条件操作符
    大于 $gt
    小于 $lt
    大于等于 $gte
    小于等于 $lte
9. $type操作符
    1   Double
    2   String
    3   Object
    4   Array
    5   Binary data
    6   Undefined //已废弃
    7   Object id
    8   Boolean
    9   Date
    10  Null
    11  Regular Expression
    13  Javascript
    14  Symbol
    15  Javascript(with scope)
    16  32-bit integer
    17  Timestamp
    18  64-bit integer
    255 Min key
    127 Max key

    查询实例
    db.testTable.find(testField:{$type:2}); //查询testField为String的文档
10. limit和skip方法
    db.testTable.find().limit(3).skip(2); //查询第3～5条数据，limit参数为查询条数，skip参数为跳过的记录数
11. 排序
    db.testTable.find().sort({testField:1}); //集合中的数据按testField升序排序，  -1 为降序
12. 索引
    db.testTable.ensureIndex({testField:1}); //以testField为索引字段，创建升序索引， -1为降序
13. 聚合
    db.testTable.aggregate([$group:{title:"$testField",total:{$sum:1}}]); 
    以上语句等同于select testField as title, count(*) as total from testTable group by testField

    聚合表达式
    $sum        计算总和
    $avg        计算平均值
    $min        最小值
    $max        最大值
    $push       在结果文档中插入值到一个数组中
    $addToSet   在结果文档中插入值到一个数组中，但不创建副本
    $first      获取第一个文档数据
    $last       获取最后一个文档数据
    
