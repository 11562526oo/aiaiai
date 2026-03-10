String
	最常用的数据类型，存储文本、数字、最大512MB。
	
		场景：缓存页面数据，会话等
		
Hash
	键值对的集合，适合存储对象属性
	
		场景：比如id存商品  value：Hash存商品信息

List
	有序的字符串列表。底层是双向链表
	
		场景：消息队列，Lpush生产消息   Rpop消费消息

Set
	无序且元素不重复的集合，查找和去重效率高
	
		场景：共同关注

ZSet
	每个元素都是带一个score分数排序，底层哈希表 + [[跳表]]实现。member查score用哈希表
	
		场景：排行榜，热搜榜




**拓展**bitMap（0，1利用率高，签到） ，Stream

大key会影响redis的效率，10kb比较健康 ，超过100kb建议拆分。还会影响主从同步，删除策略过期删除等。

如何查找大Key：
```
# Redis 4.0+ 内置的大 key 扫描，采样分析
redis-cli --bigkeys

# 更精确的方式，用 SCAN 遍历 + DEBUG OBJECT
redis-cli SCAN 0 COUNT 1000
redis-cli DEBUG OBJECT your_key

# Redis 4.0+ 可以用 MEMORY USAGE
redis-cli MEMORY USAGE your_key
```

怎么解决大key
开发层面上，进行大key拆分，用到的时候组装，或者进行数据压缩。如果是json可以考虑转为hash
业务层面上，只存储必要的数据，冷数据用到的时候查询数据库。
