今天看PLM产品代码时，看原作自己写了个WeakList做缓存用，于是一并学习了下WeakHashMap；

做为Map的一个实现类，没有实现线程安全，这块需要自己加控制；

        Map map = Collections.synchronizedMap(new WeakHashMap<>());
具体怎么用呢，put时，与普通Map一样，如果想让它在不用的时候及时回收，则需要些处理
- 不需要处理它的key，而是把它的value置为null，这样下次GC时，这个key值清除出map，value进入待回收队列；
- 再次GC时，value对象彻底清除。

它存在的意义到底是什么呢，一般情况下，大家只知道不常用的对象，JVM会自动回收，但怎么回收的，哪些能回收，
好多小伙伴并不清楚，这块需要记住的是，放到List、Map这类集合对象里的对象，不会被回收，这便是问题所在，
想让它回收，就得用特殊的Map去装它们，这就是WeakHashMap存在的意义，更加及时准确的定义哪些数据需要回收。


