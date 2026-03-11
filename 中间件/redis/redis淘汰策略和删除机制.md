
**不淘汰数据**
内存满直接报错，禁止写入

**淘汰数据**
1. 对于设置了过期的key
	volatle- random	随机删除过期时间的key
	volatle-ttl	优先删除剩余存货时间最短的key
	volatle-lru	删除最久没有被访问的key
	volatle-lfu	淘汰访问频率最低的key
2. 针对于所有的key
	allkeys-random  随机删除key
	allkeys-lru    删除最久没有被访问的key
	allkeys-lfu    淘汰访问频率最低的key