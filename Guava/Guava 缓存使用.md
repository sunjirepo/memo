### Guava 缓存使用实例

1. 登陆成功 保存token服务器存储。
2. 删除用户/修改用户密码 删除缓存token数据。
3. 每次校验 token 是否存在缓存中。



##### 内存型缓存 guava cache
	自动加载Key：创建自己的CacheLoader通常只需要简单地实现V load(K key) throws Exception方法。 =》 缓存元素也可以通过Cache.put方法直接插入，但自动加载是首选的，因为它可以更容易地推断所有缓存内容的一致性。
	从LoadingCache查询的正规方式是使用get(K)方法。这个方法要么返回已经缓存的值，要么使用CacheLoader向缓存原子地加载新值。由于CacheLoader可能抛出异常，LoadingCache.get(K)也声明为抛出ExecutionException异常。

	一篇翻译 + 一篇实战
	翻译：http://ifeve.com/google-guava-cachesexplained/
	实例：https://www.cnblogs.com/rickiyang/p/11074159.html

	延伸 github：
	https://github.com/google/guava/wiki / https://www.tfnico.com/presentations/google-guava

##### 1万个key，算下缓存最大空间。 =》 key=uid, value=jwt
	3290cf499a145fe22588c3130513eea3 uid=32bit string
	eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1aWQiOiI1MGU2MWEzZTMzZjBmNzZlYjQ3MGVjMWY0ZjdhMjY0MCIsIm5iZiI6MTYwNDMwNDE0OSwidXNlcl90eXBlIjoiQURNSU4iLCJpc3MiOiJocnRwcyIsImlhdCI6MTYwNDMwNDE0OX0.kUy-lJoQa4u22n_JLvCFIn6QQUna0izFdlQWyt7tJCY jwt=228bit string

	https://blog.csdn.net/mafei6827/article/details/87076371 40+2n 字节，uid=104字节， jwt=600字节 =》 700字节。 

	总大小 ～= 700 * 1w / 1024 / 1024 = 6.67M
	done 完全没问题。

##### 登陆操作 
	使用1 get(K, Callable<V>) "如果有缓存则返回；否则运算、缓存、然后返回"
	使用2 cache.put(key, value)方法可以直接向缓存中插入值，这会直接覆盖掉给定键之前映射的值。
		用2
	回收策略：expireAfterAccess(long, TimeUnit)：缓存项在给定时间内没有被读/写访问，则回收。请注意这种缓存的回收顺序和基于大小回收一样。
		测试定时回收：对定时回收进行测试时，不一定非得花费两秒钟去测试两秒的过期。你可以使用Ticker接口和CacheBuilder.ticker(Ticker)方法在缓存中自定义一个时间源，而不是非得用系统时钟。

##### 删除 / 修改密码
	个别清除：Cache.invalidate(key)


##### 验证token操作
	get(K)




