# Redis数据类型

---------------

#### 1. 5大基本数据类型

- **String**

  - 基本命令

    ```bash
    set key1 “abc”
    get key1
    keys *
    EXISTS key1
    APPEND key1 "hellow" # 如果当前key不存在，则相当于setkey
    STRLEN key1
    ###################################################
    
    set views 0
    incr views   # ++操作
    decr views   # --操作
    
    INCRBY views 10 # +10
    DECRBY VIEWS 10 # -10
    
    GETRANGE key1 0 3 # 截取字符串0到3   [0, 3]
    SETRANGE key1 1 xxxx # 将第1开始替换为xxxx 覆盖式
    
    
    setex   # 设置过期时间  set with expire time
    setex key3 30 “hello”
    setnx   # set if not exists 如果不存在就设置
    setnx key3 “asda”
    
    mset k1 v1 k2 v2 k3 v3  # 多个设置
    mget	k1 k2 k3    # 多个获取
    
    ####################################
    
    set user:1{name:zhangsan,age:3}  # 设置user:1对象 值为json字符串
    # 这里的key是一个巧妙的设计： user:{id}:{filed}，如此设计在redis完全ok
    
    mset user:1:name zhangsan user:1:age 2
    mget user:1:name user:1:age
    ###################################
    
    getset db redis  # 先get db 再setdb为redis
    
    
    
    ```
    
  
- List

  在Reids里面。List可以实现堆栈、队列、阻塞队列

  **所有的list命令都是以l开头**。

  - 基本命令

    ```bash
    ######
    LPUSH list one  # LPUSH  插入到头部
    LPUSH list two  
    
    RPUSH list three         #  插入到尾部
    
    LPOP list
    RPOP list
    
    Llen list # 返回列表长度
    
    LRANGE list 0 1
    
    Lrem list 1 one # 移除list集合中指定的value，包括指定其个数
    
    ################################
    ltrim list 1 2   # 截取指定的长度  [1,2]
    
    rpoplpush list1 list2 # 将lit1的最后元素移除，移动到新的list
    
    
    #########
    LINSERT mylist before "world" "orther"
    LINSERT mylist after "world" "orther"
    ```

  - 小结

    - 实际上是一个链表，before Node after。
    - 如果key不存在，就创建新的链表
    - 如果key存在，新增内容
    - 如果移除了所有值，空链表，也代表不存在
    - 在两边插入或者改动值，效率最高。

- SET

  无序不重复集合

  - 基本命令

    ```bash
    sadd myset "hello"
    smembers myset     # 查看set所有值
    sismember myset hello  # 判断摸个元素是否在集合中
    
    scard myset # 获取set集合中内容元素的个数
    
    spop myset # 随机移除元素
    
    srem myset hello #移除set集合中的指定元素
    
    #####################
    SRANDMEMBER  myset 1  # 从myset中随机抽选出一个元素
    
    smove myset1 myset2 "kuangshen" # 将指定的值移动到另外一个set集合中
    	
    ##############
    数字集合类：
    - 差集    
    sdiff set1 set2
    - 交集
    sinter set1 set2
    - 并集
    sunion set1 set2
    
    ```

- Hash

  Map集合，key-Map 集合

  - 基本命令

    ```bash
    hset myhash field1 kuangshen
    hget myhash filed1
    hmset myahs field1 hellow filed2 world
    hmget myhash field1 field2 
    
    hdel myhash field1 
    ###########
    
    hlen myhash   # hash表字段是否存在
    hexists myhash f1  判断hash中指定字段是否存在
    
    ##### ######3
    hkeys myhash   # 获取所有key
    hvals myhash   # 获取所有value
    
    
    ######
    
    ```

- **ZSET**

  - 概念

    有序集合，排序

    在set的基础上增加了一个值。

    set k1 v1   zset k1 score v1

  - 基本命令

    ```bash
    zadd salary 2500 xiaohong
    zadd salary 5000 zhangsan
    zadd salary 500 kuangshen
    zrange 0 -1
    
    zrangebyscore salary -inf +inf Withscores # 显示全部用户并且附带成绩  升序排列
    
    
    zrem salary "xiaohong"
    
    zcard salary # 显示多少元素
    
    
    
    zrevrange salary 0 -1 # 反转 显示
    
    
    
    zcount myset 1 3   # 获取指定区间的成员数量
    

-----------------

#### 2. 3种特殊数据类型

- **geospatial  地理位置**   

  经度、纬度和名称。

  这个功能可以推算地理位置信息，两地之间的距离。

  方圆几里的人。

  - 基本命令

    ```bash
    geoadd china:city 116.40 39.90 beijing
    geoadd china:city 121.47 31.23 shanghai
    geoadd china:city 106.50 29.54 chongqin
    geoadd china:city 114.05 22.52 shenzheng
    geoadd china:city 120.16 30.24 hangzhou
    geoadd china:city 108.96 34.26 xian
    
    
    ######
    geopos china:city beijing   # 获取指定的经纬度
    
    #####  返回两个地点之间的举例
    geodist china:city beijing shanghai km
    1067.3788   
    
    ####  找附近的城市   以某点为中心找附近 1000km的城市
    georadius  china:city 110 30 1000 km  withdist
    georadius  china:city 110 30 1000 km  withcoord count 1
    
    
    #### 找出位于指定元素周围的其他元素
    georadiusbymember china:city beijing 1000km
    
    
    #### geohash 返回一个或者多个位置元素11个字符的hash长度（经纬度转换为，hash字符串）
    geohash china:city beijing 
    
    # 查看全部元素
    ZRANGE china:city 0 -1
    zrem china:city beijing
    
    ```

- Hyperloglog

  - 什么是基数

    不重复元素，可以接受误差

    做基数统计的算法

    优点：占用内存是固定的。2^64不同的元素的基数，只需要12kb内存。

    如果从内存角度比较的化，Hyperloglog是首选。（0.81%的错误率，可以接受）

    统计UV（网站用户）任务。

  - 基础命令

    ```bash
    #### 测试基数使用
    pfadd mykey a b c d e f g h i j
    pfcount mykey 
    pfadd mykey2 i j z x c v b n m
    pfcount mykey2
    
    pfmerge mykey3 mykey mykey2
    ```

- bitmaps

  - 位存储

    2个状态，使用bitmaps解决

    统计用户信息，活跃不活跃。登录，未登录。打卡，365打卡。

    365天=365bit， 1字节=8bit  46个字节左右。

  - 基本命令

    比如7天打卡

    ```bash
    setbit sign 0 1
    setbit sign 1 1
    setbit sign 2 0
    setbit sign 3 0
    setbit sign 4 1
    setbit sign 5 0
    setbit sign 6 1
    
    bitcount sign 
    ==》 4
    ```

    



