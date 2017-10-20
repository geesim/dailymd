#数据类型

1. Strings字符串
------------
######操作语法: 
	set key value; //设置
	get key; //获取
	setnx key value; //如果key已经存在，则不成功，返回0；nx表示not exist（不存在）
	setex key expire value; //设置以expire为有效期值
	setrange key index value; //以value从index位置开始替换key值
	mset key1 value1 key2 value2; //设置多个键值
	msetnx key1 value1 key2 value2; //同setnx,注意其中一个不成功则都不成功
	getset key value; //获取旧值并设置新值
	getrange key index length; //获取从index位置开始取length个字符
	mget key1 key2; //获取多个值
	incr key; //对key的值进行加加操作，加一操作；
	incrby key increment; //对key以increment进行增加
	decr key; //与incr相反，减一操作
	decrby key num; //与incrby相反
	append key value; //在key值末尾增添value
	strlen key; //查看长度

2. Hashes映射表
------------
######操作语法:
	hset table_name field value; //为哈希表table_name设置field字段为指定值；
	hget table_name field; //获取哈希表指定字段值
	hsetnx table_name field value; //如果字段field值已存在，则不成功，返回0
	hmset table_name field1 value field2 value; //同时设置哈希表table_name多个字段值
	hmget table_name field1 field2; //获取多个字段值
	hincrby table_name field increment; //对字段以increment为步值进行增加
	hexists table_name field; //检测字段是否存在
	hlen table_name; //查看表里的字段数量
	hdel table_name field; //删除指定字段
	hkeys table_name; //返回表中的所有字段名（键名）
	hvals table_name; //返回表中的所有值
	hgetall table_name; //获取全部字段和值

3. Lists链表
------------
######操作语法:
	lpush list_name value; //从链表头部进行压入数据 
	rpush list_name value; //从链表尾部压入数据
	lrange  list_name start stop; //从链表头位置start取到链表stop位置
	linsert list_name [before|after] value; //在链表指定位置插入值
	lset list_name index value; //设置指定下标index的值
	lrem list_name num value; //从list_name中删除num个与value相同的值
	ltrim list_name start stop; //对链表list_name进行裁剪，保留start到stop位置的数据
	lpop list_name; //从list_name的头部弹出元素
	rpop list_name; //从list_name的尾部弹出元素
	rpoplpush list_name1 list_name2; //从第一个链表尾部弹出一个元素压入到第二个链表的头部
	lindex list_name index; //返回list_name中对应index位置的值
	llen list_name; //返回list_name的长度

4. Set集合
-----------
######操作语法:
	sadd set_name value; //将一个（或多个）元素加入到集合中
	scard set_name; //查看集合中的元素数量
	sdiff set_name1 set_name2; //返回给定集合的差集
	sdiffstore store_set_name set_name1 set_name2; //将给定集合的差集存储在指定集合store_set_name中
	sinter set_name1 set_name2; //返回给定集合的交集
	sinterstore store_set_name set_name1 set_name2; //将给定集合的交集存储在指定集合store_set_name中
	sismember set_name value; //判断value是否是集合的成员
	smembers set_name; //返回集合中的所有成员
	smove set_name1 set_name2 value; //从第一个集合set_name1中移动指定元素value到第二个集合set_name2
	spop set_name; //随机弹出一个元素
	srandmember set_name count; //返回指定count个数的元素集合,注意count为正数和负数时的差异
	srem set_name value; //移除指定的一个（或多个）元素
	sunion set_name1 set_name2; //返回给定集合的并集
	suinonstore store_set_name set_name1 set_name2; //将给定集合的并集存储到指定集合store_set_name 中
	sscan set_name cursor pattern count; //从游标cursor处开始扫描出count个匹配pattern的元素，返回数组列表

5. Sorted set有序集合
-----------
######操作语法:
	zadd set_name score value; //将一个（或多个）元素及其分数score加入到集合中，如某元素已存在则更新分数值并按新分数大小变更元素位置
	zcard set_name; //返回集合中元素的数量
	zcount set_name min max; //计算有序集合指定分数区间min-max的元素数量
	zincrby set_name increment value; //对指定元素的分数加上指定增量
	zinterstore store_set_name num_sets set_name1 set_name2...; //计算给定的num_sets(需提前给定)个有序集合的交集，并且把结果放到store_set_name
	zlexcount set_name min max; //计算set_name中min-max区间内的元素数量 - 表示min，+ 表示max，元素前需加 '[' 或 '(', 
	zrange set_name start stop [withscores]; //返回set_name中start-stop区间内的元素,位置按从小到大
	zrangebylex set_name min max [limit offset count]; //返回指定区间内的元素，按元素成员字典正序排序，分数需相同，同 zlexcount
	zrangebyscore set_name min max [withscores] [limit offset count]; //返回指定分数区间内的元素
	zrank set_name value; //返回指定元素的排名，排名顺序时按分数小到大
	zrem set_name value; //移除指定的一个（或多个）元素
	zremrangebylex set_name min max; //移除set_name中给定元素成员字典区间中的所有元素
	zremrangebyrank set_name start stop; //移除set_name中给定排名区间的元素，位置按小到大
	zremrangebyscore set_name min max; //移除set_name中给定分数区间内的所有元素
	zrevrange set_name start stop [withscores]; //返回指定区间内的元素，按大到小排序
	zrevrangebyscore set_name max min [withscores]; //返回指定分数区间内的元素，按分数高到低排序
	zrevrank set_name value; //返回指定元素的排名，排名顺序按分数大到小
	zscore set_name value; //返回指定元素的分数值
	zunionstore store_set_name num_sets set_name1 set_name2...; //计算给定的num_sets(需提前给定)个有序集合的并集，并且把结构保存到store_set_name中
	zscan set_name cursor pattern count; //从游标cursor处开始扫描出count个匹配pattern的元素，返回数组列表

6. HyperLogLog基数统计算法
------------
######操作语法:
	pfadd key element; //添加指定元素到 HyperLogLog 中
	pfcount key; //返回给定 HyperLogLog 的基数估算值
	pfmerge dest_key source_key1 source_key2; //将多个 HyperLogLog 合并为一个 HyperLogLog

# Redis发布订阅命令
	psubscribe pattern; //订阅一个或多个给定模式的频道
	pubsub <subcommand> [argument [argument ...]]; //查看订阅与发布系统的状态，channels 活跃频道，numsub 订阅者数量， numpat 订阅者模式数量
	publish channel message; //将信息发送到指定频道
	punsubscribe pattern; //退订一个或多个给定模式的频道
	subcribe channel; //订阅指定的一个（或多个）频道
	unsubscribe channel; //退订指定的一个（或多个）频道

# Redis事务命令
	multi	标记一个事务块开始
	exec	执行所有事务块内的命令
	discard	取消事务，放弃执行事务块内的命令
	watch key [key]	监视一个(或多个)key，key被其他命令改动则事务打断
	unwatch	取消对所有key监视

# Redis管理命令
	keys pattern	返回匹配的所有键名
	exists	key 判断是否存在键名
	del key 删除键
	expire key 设置key的过期时间
	ttl key 返回key的有效时长
	move key db_number 将给定键名的数据移动到指定数据库
	persist key 设置key永不过期(取消过期时间)
	randomkey 随机返回key空间的一个key
	rename key 重命名key
	type key 返回数据类型
	------
	ping 测试连接是否存活
	echo 打印内容
	select  db_number 使用对应db_number数据库（数据库编号0~15）
	quit 退出命令行
	dbsize 返回当前数据库key数目
	info 返回redis服务器信息
	config get attribute 获取配置项信息
	flushdb 删除当前数据库所有的key
	flushall 删除所有数据库中的所有key

# Redis高级应用
	
	1. 安全性
	设置redis.conf中的requirepass配置项，并设置密码
	auth pass 授权命令
	redis-cli -a pass 登陆时授权
	
	2. 主从复制
	slaveof ip:port 从服务器配置文件配置项设置主服务器ip和端口
	masterauth pass 从服务器配置文件设置项设置主服务器登录口令
	
	3. 持久化机制
	snashotting 快照，默认

	append-only file 每一个写命令都会追加到文件里
	|-	append-only yes 启动aof方式
	|_	appendsync [always|everysec|no] 写入频率配置

	4. 虚拟内存
	vm-enabled yes 开启vm功能
	vm-swap-file to_swap_path 交换数据保存路径
	vm-max-memory 1000000 最大内存上限
	vm-page-size 32 每个页面大小32字节
	vm-pages 134217728 最多使用多少页面
	vm-max-thread 4 用于执行的工作线程数量


