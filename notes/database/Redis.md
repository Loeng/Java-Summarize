<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Redis介绍](#redis%E4%BB%8B%E7%BB%8D)
  - [Redis特点](#redis%E7%89%B9%E7%82%B9)
  - [Redis和Memcached区别](#redis%E5%92%8Cmemcached%E5%8C%BA%E5%88%AB)
- [Redis内部数据结构](#redis%E5%86%85%E9%83%A8%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)
  - [字符串](#%E5%AD%97%E7%AC%A6%E4%B8%B2)
  - [字典](#%E5%AD%97%E5%85%B8)
  - [压缩列表](#%E5%8E%8B%E7%BC%A9%E5%88%97%E8%A1%A8)
  - [快速列表](#%E5%BF%AB%E9%80%9F%E5%88%97%E8%A1%A8)
  - [跳跃列表](#%E8%B7%B3%E8%B7%83%E5%88%97%E8%A1%A8)
    - [为什么Redis选择使用跳表而不是红黑树来实现有序集合？](#%E4%B8%BA%E4%BB%80%E4%B9%88redis%E9%80%89%E6%8B%A9%E4%BD%BF%E7%94%A8%E8%B7%B3%E8%A1%A8%E8%80%8C%E4%B8%8D%E6%98%AF%E7%BA%A2%E9%BB%91%E6%A0%91%E6%9D%A5%E5%AE%9E%E7%8E%B0%E6%9C%89%E5%BA%8F%E9%9B%86%E5%90%88)
- [Redis应用](#redis%E5%BA%94%E7%94%A8)
  - [分布式锁](#%E5%88%86%E5%B8%83%E5%BC%8F%E9%94%81)
  - [延时队列](#%E5%BB%B6%E6%97%B6%E9%98%9F%E5%88%97)
  - [位图](#%E4%BD%8D%E5%9B%BE)
  - [HyperLogLog](#hyperloglog)
  - [布隆过滤器](#%E5%B8%83%E9%9A%86%E8%BF%87%E6%BB%A4%E5%99%A8)
- [Gossip协议](#gossip%E5%8D%8F%E8%AE%AE)
- [Redis单进程单线程方式](#redis%E5%8D%95%E8%BF%9B%E7%A8%8B%E5%8D%95%E7%BA%BF%E7%A8%8B%E6%96%B9%E5%BC%8F)
  - [单进程单线程好处](#%E5%8D%95%E8%BF%9B%E7%A8%8B%E5%8D%95%E7%BA%BF%E7%A8%8B%E5%A5%BD%E5%A4%84)
  - [单进程单线程弊端](#%E5%8D%95%E8%BF%9B%E7%A8%8B%E5%8D%95%E7%BA%BF%E7%A8%8B%E5%BC%8A%E7%AB%AF)
  - [其他一些优秀的开源软件采用的模型](#%E5%85%B6%E4%BB%96%E4%B8%80%E4%BA%9B%E4%BC%98%E7%A7%80%E7%9A%84%E5%BC%80%E6%BA%90%E8%BD%AF%E4%BB%B6%E9%87%87%E7%94%A8%E7%9A%84%E6%A8%A1%E5%9E%8B)
  - [多路I/O复用模型](#%E5%A4%9A%E8%B7%AFio%E5%A4%8D%E7%94%A8%E6%A8%A1%E5%9E%8B)
- [Redis快的主要原因](#redis%E5%BF%AB%E7%9A%84%E4%B8%BB%E8%A6%81%E5%8E%9F%E5%9B%A0)
- [Redis主从复制](#redis%E4%B8%BB%E4%BB%8E%E5%A4%8D%E5%88%B6)
- [Redis持久化](#redis%E6%8C%81%E4%B9%85%E5%8C%96)
  - [Redis RDB和AOF的优缺点对比以及如何选择](#redis-rdb%E5%92%8Caof%E7%9A%84%E4%BC%98%E7%BC%BA%E7%82%B9%E5%AF%B9%E6%AF%94%E4%BB%A5%E5%8F%8A%E5%A6%82%E4%BD%95%E9%80%89%E6%8B%A9)
  - [RDB和AOF到底该如何选择？](#rdb%E5%92%8Caof%E5%88%B0%E5%BA%95%E8%AF%A5%E5%A6%82%E4%BD%95%E9%80%89%E6%8B%A9)
  - [为什么恢复的时候RDB比AOF快？](#%E4%B8%BA%E4%BB%80%E4%B9%88%E6%81%A2%E5%A4%8D%E7%9A%84%E6%97%B6%E5%80%99rdb%E6%AF%94aof%E5%BF%AB)
- [Redis常见的性能问题都有哪些？如何解决？](#redis%E5%B8%B8%E8%A7%81%E7%9A%84%E6%80%A7%E8%83%BD%E9%97%AE%E9%A2%98%E9%83%BD%E6%9C%89%E5%93%AA%E4%BA%9B%E5%A6%82%E4%BD%95%E8%A7%A3%E5%86%B3)
- [Redis六种淘汰key策略（默认时no-eviction）](#redis%E5%85%AD%E7%A7%8D%E6%B7%98%E6%B1%B0key%E7%AD%96%E7%95%A5%E9%BB%98%E8%AE%A4%E6%97%B6no-eviction)
- [Redis三种删除过期键策略](#redis%E4%B8%89%E7%A7%8D%E5%88%A0%E9%99%A4%E8%BF%87%E6%9C%9F%E9%94%AE%E7%AD%96%E7%95%A5)
  - [定时删除（并没有用到）](#%E5%AE%9A%E6%97%B6%E5%88%A0%E9%99%A4%E5%B9%B6%E6%B2%A1%E6%9C%89%E7%94%A8%E5%88%B0)
  - [惰性删除](#%E6%83%B0%E6%80%A7%E5%88%A0%E9%99%A4)
  - [定期删除](#%E5%AE%9A%E6%9C%9F%E5%88%A0%E9%99%A4)
- [Redis的内存优化](#redis%E7%9A%84%E5%86%85%E5%AD%98%E4%BC%98%E5%8C%96)
- [Redis4.0新特性](#redis40%E6%96%B0%E7%89%B9%E6%80%A7)
  - [一、主从数据同步机制](#%E4%B8%80%E4%B8%BB%E4%BB%8E%E6%95%B0%E6%8D%AE%E5%90%8C%E6%AD%A5%E6%9C%BA%E5%88%B6)
  - [二、命令优化](#%E4%BA%8C%E5%91%BD%E4%BB%A4%E4%BC%98%E5%8C%96)
  - [三、慢日志记录客户端来源IP地址](#%E4%B8%89%E6%85%A2%E6%97%A5%E5%BF%97%E8%AE%B0%E5%BD%95%E5%AE%A2%E6%88%B7%E7%AB%AF%E6%9D%A5%E6%BA%90ip%E5%9C%B0%E5%9D%80)
  - [四、混合RDB + AOF格式](#%E5%9B%9B%E6%B7%B7%E5%90%88rdb--aof%E6%A0%BC%E5%BC%8F)
  - [五、内存使用和性能改进](#%E4%BA%94%E5%86%85%E5%AD%98%E4%BD%BF%E7%94%A8%E5%92%8C%E6%80%A7%E8%83%BD%E6%94%B9%E8%BF%9B)
- [缓存解决方案分析](#%E7%BC%93%E5%AD%98%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88%E5%88%86%E6%9E%90)
  - [缓存雪崩](#%E7%BC%93%E5%AD%98%E9%9B%AA%E5%B4%A9)
  - [缓存穿透](#%E7%BC%93%E5%AD%98%E7%A9%BF%E9%80%8F)
  - [缓存击穿](#%E7%BC%93%E5%AD%98%E5%87%BB%E7%A9%BF)
  - [缓存预热](#%E7%BC%93%E5%AD%98%E9%A2%84%E7%83%AD)
  - [缓存更新](#%E7%BC%93%E5%AD%98%E6%9B%B4%E6%96%B0)
- [Redis Sentinel 与 Redis Cluster区别和各自适用场景](#redis-sentinel-%E4%B8%8E-redis-cluster%E5%8C%BA%E5%88%AB%E5%92%8C%E5%90%84%E8%87%AA%E9%80%82%E7%94%A8%E5%9C%BA%E6%99%AF)
  - [Redis Sentinel](#redis-sentinel)
  - [Redis Cluster](#redis-cluster)
- [为什么lua脚本结合Redis命令可以实现原子性？](#%E4%B8%BA%E4%BB%80%E4%B9%88lua%E8%84%9A%E6%9C%AC%E7%BB%93%E5%90%88redis%E5%91%BD%E4%BB%A4%E5%8F%AF%E4%BB%A5%E5%AE%9E%E7%8E%B0%E5%8E%9F%E5%AD%90%E6%80%A7)
- [Redis分布式锁会导致什么问题?](#redis%E5%88%86%E5%B8%83%E5%BC%8F%E9%94%81%E4%BC%9A%E5%AF%BC%E8%87%B4%E4%BB%80%E4%B9%88%E9%97%AE%E9%A2%98)
- [Redis有1000万个key，找出前缀为aaa的key的命令是什么？](#redis%E6%9C%891000%E4%B8%87%E4%B8%AAkey%E6%89%BE%E5%87%BA%E5%89%8D%E7%BC%80%E4%B8%BAaaa%E7%9A%84key%E7%9A%84%E5%91%BD%E4%BB%A4%E6%98%AF%E4%BB%80%E4%B9%88)
- [热key问题](#%E7%83%ADkey%E9%97%AE%E9%A2%98)
  - [怎么发现热key](#%E6%80%8E%E4%B9%88%E5%8F%91%E7%8E%B0%E7%83%ADkey)
    - [方法一:凭借业务经验，进行预估哪些是热key](#%E6%96%B9%E6%B3%95%E4%B8%80%E5%87%AD%E5%80%9F%E4%B8%9A%E5%8A%A1%E7%BB%8F%E9%AA%8C%E8%BF%9B%E8%A1%8C%E9%A2%84%E4%BC%B0%E5%93%AA%E4%BA%9B%E6%98%AF%E7%83%ADkey)
    - [方法二:在客户端进行收集](#%E6%96%B9%E6%B3%95%E4%BA%8C%E5%9C%A8%E5%AE%A2%E6%88%B7%E7%AB%AF%E8%BF%9B%E8%A1%8C%E6%94%B6%E9%9B%86)
    - [方法三:在Proxy层做收集](#%E6%96%B9%E6%B3%95%E4%B8%89%E5%9C%A8proxy%E5%B1%82%E5%81%9A%E6%94%B6%E9%9B%86)
    - [方法四:用redis自带命令](#%E6%96%B9%E6%B3%95%E5%9B%9B%E7%94%A8redis%E8%87%AA%E5%B8%A6%E5%91%BD%E4%BB%A4)
    - [方法五:自己抓包评估](#%E6%96%B9%E6%B3%95%E4%BA%94%E8%87%AA%E5%B7%B1%E6%8A%93%E5%8C%85%E8%AF%84%E4%BC%B0)
  - [怎么设置redis失效时间、怎么设置永久有效？](#%E6%80%8E%E4%B9%88%E8%AE%BE%E7%BD%AEredis%E5%A4%B1%E6%95%88%E6%97%B6%E9%97%B4%E6%80%8E%E4%B9%88%E8%AE%BE%E7%BD%AE%E6%B0%B8%E4%B9%85%E6%9C%89%E6%95%88)
- [Redis事务和MySQL事务有什么区别？](#redis%E4%BA%8B%E5%8A%A1%E5%92%8Cmysql%E4%BA%8B%E5%8A%A1%E6%9C%89%E4%BB%80%E4%B9%88%E5%8C%BA%E5%88%AB)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->



# Redis介绍
Redis 是完全开源免费的，遵守BSD协议，是一个高性能的key-value数据库。

Redis 与其他 key - value 缓存产品有以下三个特点：
- Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
- Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
- Redis支持数据的备份，即master-slave模式的数据备份。



## Redis特点
1. 速度快，因为数据存在内存中，类似于HashMap，HashMap的优势就是查找和操作的时间复杂度都是O(1)
2. 支持丰富数据类型，支持string，list，set，sorted set，hash
3. 支持事务，操作都是原子性，所谓的原子性就是对数据的更改要么全部执行，要么全部不执行
4. 丰富的特性：可用于缓存，消息，按key设置过期时间，过期后将会自动删除

##  Redis和Memcached区别
1. memcached所有的值均是简单的字符串，redis作为其替代者，支持更为丰富的数据类型
2. redis的速度比memcached快很多
3. redis可以持久化其数据
4. Redis支持数据的备份，即master-slave模式的数据备份。
5. 使用底层模型不同，它们之间底层实现方式 以及与客户端之间通信的应用协议不一样。Redis直接自己构建了VM 机制 ，因为一般的系统调用系统函数的话，会浪费一定的时间去移动和请求。
6. value大小：redis最大可以达到1GB，而memcache只有1MB


# Redis内部数据结构
## 字符串

Redis的字符串叫做[SDS]，即Simple Dynamic String。它的结构是一个带长度信息的字节数组

```c++
struct SDS<T> {
T capacity; // 数组容量
T len; // 数组长度
byte flags; // 特殊标识位，不理睬它
byte[] content; // 数组内容
}
```

1. content存储真正的字符串内容，capacity表示所分配数组的长度，len表示字符串的实际长度

2. SDS使泛型用T，是因为当字符串比较短时，len和capacity可以使用byte和short来表示
3. Redis的字符串有两种存储方式，当长度特别短使用`EMB`形式存储，当长度超过44时，使用`raw`形式存储

4. 字符串在长度小于 1M 之前，扩容空间采用加倍策略，也就是保留 100% 的冗余空间。当长度超过 1M 之后，为了避免加倍后的冗余空间过大而导致浪费，每次扩容只会多分配 1M 大小的冗余空间。

## 字典

字典，是一种用于保存键值对的抽象数据结构，Redis中的hash结构、zset中value和score值的映射关系、Redis所有的key和value、带过期时间的key都是使用字典（dict）这个数据结构。

![](https://github.com/zaiyunduan123/Java-Interview/blob/master/image/redis-1.png)

字典使用哈希表来作为底层实现，每个字典带有两个哈希表，一个平时使用，另外一个仅在进行渐进式搬迁时使用，这时候两个 hashtable 存储的分别是旧的 hashtable 和新的 hashtable。待搬迁结束后，旧的 hashtable 被删除，新的 hashtable 取而代之。



扩容：

1. 如果服务器没有正在执行bgsave令，并且哈希表中的元素个数大于等于一维数据的长度，自动开始对dict进行扩容扩容至2倍
2. 如果服务器正在执行bgsave命令，并且哈希表中的元素个数大于等于一维数据的长度的5倍，才进行强制扩容

缩容：

1. 当元素个数低于数组长度的 10%，Redis 会对 hash 表进行缩容来减少 hash 表的第一维数组空间占用。缩容不会考虑 Redis 是否正在做 bgsave。


SAVE和BGSAVE的区别：

1. SAVE  保存是阻塞主进程，客户端无法连接redis，等SAVE完成后，主进程才开始工作，客户端可以连接

2. BGSAVE  是fork一个save的子进程，在执行save过程中，不影响主进程，客户端可以正常链接redis，等子进程fork执行save完成后，通知主进程，子进程关闭。很明显BGSAVE方式比较适合线上的维护操作，两种方式的使用一定要了解清楚在谨慎选择。

## 压缩列表

zset 和 hash 容器对象在元素个数较少的时候，采用压缩列表 (ziplist) 进行存储。压缩列表是一块连续的内存空间，元素之间紧挨着存储，没有任何冗余空隙。

![](https://github.com/zaiyunduan123/Java-Interview/blob/master/image/redis-2.png)

- zlbytes：4字节，记录整个压缩列表占用内存的字节数
- zltail：4字节，记录压缩列表尾部节点距离起始地址的偏移量
- zllen：2字节，记录压缩列表包含的节点数量
- entry：不定，列表中的每个节点
- zlend：1字节，特殊值0xFF，标记压缩列表的结束



增加元素：

1. 因为 ziplist 都是紧凑存储，没有冗余空间 。意味着插入一个新的元素就需要调用 realloc 扩展内存。取决于内存分配器算法和当前的 ziplist 内存大小，realloc 可能会重新分配新的内存空间，并将之前的内容一次性拷贝到新的地址，也可能在原有的地址上进行扩展，这时就不需要进行旧内容的内存拷贝。
2. 如果 ziplist 占据内存太大，重新分配内存和拷贝内存就会有很大的消耗。所以 ziplist 不适合存储大型字符串，存储的元素也不宜过多。

级联更新：

1. 当前某个 entry 之前的节点 从小于254字节，变成大于等于254字节， 那么当前entry 的 previous_entry_length 从1字节变成5字节。如果因为从1字节变成5字节，使自己跨越了从小于254字节，到过了254字节这条线，就又会引起下一个节点的扩容。
2. 最坏的情况是：所有entry都是刚好处于250-253字节之间，然后在链表头插入一个大于等于254字节的entry，此时会触发全链级联更新。
3. 删除中间的某个节点也可能会导致级联更新



## 快速列表

考虑到链表的附加空间相对太高，prev 和 next 指针就要占去 16 个字节 (64bit 系统的指针是 8 个字节)，另外每个节点的内存都是单独分配，会加剧内存的碎片化，影响内存管理效率。后续版本对列表数据结构进行了改造，使用 quicklist 代替了 ziplist 和 linkedlist。

```c++
typedef struct quicklist {
    quicklistNode *head;        // 指向quicklist的头部
    quicklistNode *tail;        // 指向quicklist的尾部
    unsigned long count;        // 列表中所有数据项的个数总和
    unsigned int len;           // quicklist节点的个数，即ziplist的个数
    int fill : 16;              // ziplist大小限定，由list-max-ziplist-size给定
    unsigned int compress : 16; // 节点压缩深度设置，由list-compress-depth给定
} quicklist;

```



quicklist 是 ziplist 和 linkedlist 的混合体，它将 linkedlist 按段切分，每一段使用 ziplist 来紧凑存储，多个 ziplist 之间使用双向指针串接起来。

![](https://github.com/zaiyunduan123/Java-Interview/blob/master/image/redis-3.png)

1. quicklist 内部默认单个 ziplist 长度为 8k 字节，超出了这个字节数，就会新起一个 ziplist。ziplist 的长度由配置参数list-max-ziplist-size决定。
2. quicklist 默认的压缩深度是 0，也就是不压缩。压缩的实际深度由配置参数list-compress-depth决定。为了支持快速的 push/pop 操作，quicklist 的首尾两个 ziplist 不压缩，此时深度就是 1。如果深度为 2，就表示 quicklist 的首尾第一个 ziplist 以及首尾第二个 ziplist 都不压缩。


##  跳跃列表
Redis 的 zset 是一个复合结构，一方面它需要一个 hash 结构来存储 value 和 score 的对应关系，另一方面需要提供按照 score 来排序的功能，还需要能够指定 score 的范围来获取 value 列表的功能，这就需要另外一个结构「跳跃列表」。

![](https://github.com/zaiyunduan123/Java-Interview/blob/master/image/redis-4.png)

图中只画了四层，Redis 的跳跃表共有 64 层，意味着最多可以容纳 2^64 次方个元素。每一个 kv 块对应的结构如下面的代码中的zslnode结构，kv header 也是这个结构，只不过 value 字段是 null 值——无效的，score 是 Double.MIN_VALUE，用来垫底的。kv 之间使用指针串起来形成了双向链表结构，它们是 有序 排列的，从小到大。不同的 kv 层高可能不一样，层数越高的 kv 越少。同一层的 kv 会使用指针串起来。每一个层元素的遍历都是从 kv header 出发。

### 为什么Redis选择使用跳表而不是红黑树来实现有序集合？
Redis 中的有序集合(zset) 支持的操作：
1. 插入一个元素
2. 删除一个元素
3. 查找一个元素
4. 有序输出所有元素
5. 按照范围区间查找元素（比如查找值在 [100, 356] 之间的数据）

其中，前四个操作红黑树也可以完成，且时间复杂度跟跳表是一样的。但是，按照区间来查找数据这个操作，红黑树的效率没有跳表高。按照区间查找数据时，跳表可以做到 O(logn) 的时间复杂度定位区间的起点，然后在原始链表中顺序往后遍历就可以了，非常高效。


# Redis应用
## 分布式锁
Redis为单进程单线程模式，采用队列模式将并发访问变成串行访问，且多客户端对Redis的连接并不存在竞争关系。redis的SETNX命令可以方便的实现分布式锁。

分布式锁本质上要实现的目标就是在 Redis 里面占一个“茅坑”，当别的进程也要来占时，发现已经有人蹲在那里了，就只好放弃或者稍后再试。

占坑一般是使用 setnx(set if not exists) 指令，只允许被一个客户端占坑。先来先占， 用完了，再调用 del 指令释放茅坑。

setNX（SET if Not eXists 如果不存在，则 SET）
1. 当 key 不存在，将 key 的值设为 value 。
2. 若给定的 key 已经存在，则 SETNX 不做任何动作。

**如果一个持有锁的客户端失败或崩溃了不能释放锁，该怎么解决？**

如果一个客户端持有的锁超时了，任何客户端都可以检测超时并删除该锁，那么这里就会存在竞态关系，
```java
C0操作超时了，但它还持有着锁，C1和C2读取lock.foo检查时间戳，先后发现超时了。 
C1 发送DEL lock.foo 
C1 发送SETNX lock.foo 并且成功了。 
C2 发送DEL lock.foo 
C2 发送SETNX lock.foo 并且成功了。 
这样一来，C1，C2都拿到了锁！
```
所以使用执行下面的命令解决上面问题
```java
GETSET lock.foo <current Unix time + lock timeout + 1>
```
通过GETSET，C1拿到的时间戳如果是超时的，那就说明中间锁超时并且中间没有被其他客户端抢先获得锁，因此C1拿到锁。 
如果在C1之前，有个叫C2的客户端比C1快一步执行了上面的操作，那么C1拿到的时间戳是个未超时的值，这时C1没有如期获得锁，需要再次等待或重试。尽管C1没拿到锁，但它改写了C2设置的锁的超时值，不过这一点非常微小的误差带来的影响可以忽略不计。 

## 延时队列
延时队列可以通过 Redis 的 zset(有序列表) 来实现。我们将消息序列化成一个字符串作为 zset 的value，这个消息的到期处理时间作为score，然后用多个线程轮询 zset 获取到期的任务进行处理，多个线程是为了保障可用性，万一挂了一个线程还有其它线程可以继续处理。因为有多个线程，所以需要考虑并发争抢任务，确保任务不能被多次执行。

## 位图
Redis 提供了位图统计指令 bitcount 和位图查找指令 bitpos，bitcount 用来统计指定位置范围内 1 的个数，bitpos 用来查找指定范围内出现的第一个 0 或 1。
比如我们可以通过 bitcount 统计用户一共签到了多少天，通过 bitpos 指令查找用户从哪一天开始第一次签到。如果指定了范围参数[start, end]，就可以统计在某个时间范围内用户签到了多少天，用户自某天以后的哪天开始签到。
## HyperLogLog
HyperLogLog 数据结构是 Redis 的高级数据结构，HyperLogLog 提供不精确的去重计数方案，虽然不精确但是也不是非常不精确，标准误差是 0.81%，这样的精确度已经可以满足上面的 UV 统计需求了
## 布隆过滤器
布隆过滤器是一个神奇的数据结构，可以用来判断一个元素是否在一个集合中。很常用的一个功能是用来去重。

redis 在 4.0 的版本中加入了 module 功能，布隆过滤器可以通过 module 的形式添加到 redis 中，所以使用 redis 4.0 以上的版本可以通过加载 module 来使用 redis 中的布隆过滤器。但是这不是最简单的方式，使用 docker 可以直接在 redis 中体验布隆过滤器。

每个布隆过滤器对应到 Redis 的数据结构里面就是一个大型的位数组和几个不一样的无偏 hash 函数。所谓无偏就是能够把元素的 hash 值算得比较均匀。

向布隆过滤器中添加 key 时，会使用多个 hash 函数对 key 进行 hash 算得一个整数索引值然后对位数组长度进行取模运算得到一个位置，每个 hash 函数都会算得一个不同的位置。再把位数组的这几个位置都置为 1 就完成了 add 操作。

向布隆过滤器询问 key 是否存在时，跟 add 一样，也会把 hash 的几个位置都算出来，看看位数组中这几个位置是否都位 1，只要有一个位为 0，那么说明布隆过滤器中这个 key 不存在。如果都是 1，这并不能说明这个 key 就一定存在，只是极有可能存在，因为这些位被置为 1 可能是因为其它的 key 存在所致。

redis 布隆过滤器主要就两个命令：
- bf.add 添加元素到布隆过滤器中：bf.add urls https://baidu.com
- bf.exists 判断某个元素是否在过滤器中：bf.exists urls https://baidu.com

布隆过滤器存在误判的情况，在 redis 中有两个值决定布隆过滤器的准确率：
- error_rate：允许布隆过滤器的错误率，这个值越低,需要的存储空间就越大，对于不需要过于精确的场合，error_rate设置稍大一点也无伤大雅。
- initial_size：布隆过滤器可以储存的元素个数，估计的过大，会浪费存储空间，估计的过小，就会影响准确率。

redis 中有一个命令可以来设置这两个值：
>bf.reserve urls 0.01 100

代码三个参数的含义：
- 第一个值是布隆过滤器的名字。
- 第二个值为 error_rate 的值。
- 第三个值为 initial_size 的值。





# Gossip协议
Gossip协议是一个通信协议，一种传播消息的方式，灵感来自于：瘟疫、社交网络等。使用Gossip协议的有：Redis Cluster、Consul、Apache Cassandra等。

Gossip协议基本思想就是：**一个节点想要分享一些信息给网络中的其他的一些节点**。于是，它周期性的随机选择一些节点，并把信息传递给这些节点。**这些收到信息的节点接下来会做同样的事情**，即把这些信息传递给其他一些随机选择的节点。一般而言，信息会周期性的传递给N个目标节点，而不只是一个。这个N被称为fanout（这个单词的本意是扇出）

Gossip协议的主要用途就是**信息传播和扩散**：即把一些发生的事件传播到全世界。它们也被用于数据库复制，信息扩散，集群成员身份确认，故障探测等

特点：
1. **可扩展性**：即使某条消息传播过程中丢失，它也不需要做任何补偿措施
2. **失败容错**：因为一个节点会多次分享某个需要传播的信息，即使不能连通某个节点，其他被感染的节点也会尝试向这个节点传播信息。
3. **健壮性**：没有任何扮演特殊角色的节点（比如leader等）。任何一个节点无论什么时候下线或者加入，并不会破坏整个系统的服务质量。


# Redis单进程单线程方式

注意：这里我们一直在强调的单线程，只是在处理我们的网络请求的时候只有一个线程来处理，一个正式的Redis Server运行的时候肯定是不止一个线程的，这里需要大家明确的注意一下！例如Redis进行持久化的时候会以子进程或者子线程的方式执行（具体是子线程还是子进程待读者深入研究）；例如我在测试服务器上查看Redis进程，然后找到该进程下的线程

因为Redis是基于内存的操作，CPU不是Redis的瓶颈，Redis的瓶颈最有可能是机器内存的大小或者网络带宽。既然单线程容易实现，而且CPU不会成为瓶颈，所以就采用单线程



## 单进程单线程好处
1. 代码更清晰，处理逻辑更简单
2. 不用去考虑各种锁的问题，不存在加锁释放锁操作，没有因为可能出现死锁而导致的性能消耗
3. 不存在多进程或者多线程导致的切换而消耗CPU

## 单进程单线程弊端
1. 无法发挥多核CPU性能，不过可以通过在单机开多个Redis实例来完善；

## 其他一些优秀的开源软件采用的模型
1. 多进程单线程模型：Nginx （Nginx有两类进程，一类称为Master进程(相当于管理进程)，另一类称为Worker进程（实际工作进程））
2. 单进程多线程模型：MySQL、Memcached、Oracle（ Windows版本）；


## 多路I/O复用模型
1. 多路I/O复用模型是利用 select、poll、epoll 可以同时监察多个流的 I/O 事件的能力，在空闲的时候，会把当前线程阻塞掉，当有一个或多个流有 I/O 事件时，就从阻塞态中唤醒，于是程序就会轮询一遍所有的流（epoll 是只轮询那些真正发出了事件的流），并且只依次顺序的处理就绪的流，这种做法就避免了大量的无用操作。
2. 这里“多路”指的是多个网络连接，“复用”指的是复用同一个线程。采用多路 I/O 复用技术可以让单个线程高效的处理多个连接请求（尽量减少网络 IO 的时间消耗），且 Redis 在内存中操作数据的速度非常快，也就是说内存内的操作不会成为影响Redis性能的瓶颈，主要由以上几点造就了 Redis 具有很高的吞吐量。

我们知道Redis是用”单线程-多路复用IO模型”来实现高性能的内存数据服务的，这种机制避免了使用锁，但是同时这种机制在进行sunion之类的比较耗时的命令时会使redis的并发下降。因为是单一线程，所以同一时刻只有一个操作在进行，所以，耗时的命令会导致并发的下降，不只是读并发，写并发也会下降。而单一线程也只能用到一个CPU核心，所以可以在同一个多核的服务器中，可以启动多个实例，组成master-master或者master-slave的形式，耗时的读命令可以完全在slave进行。



# Redis快的主要原因
1. 完全基于内存
2. 采用单线程,避免了不必要的上下文切换和竞争条件
3. 数据结构简单，对数据操作也简单
4. 使用多路 I/O 复用模型





# Redis主从复制
过程原理：

1. 当从库和主库建立MS关系后,会向主数据库发送SYNC命令
2. 主库接收到SYNC命令后会开始在后台保存快照(RDB持久化过程),并将期间接收到的写命令缓存起来
3. 当快照完成后,主Redis会将快照文件和所有缓存的写命令发送给从Redis
4. 从Redis接收到后,会载入快照文件并且执行收到的缓存的命令
5. 之后,主Redis每当接收到写命令时就会将命令发送从Redis，从而保证数据的一致

缺点：所有的slave节点数据的复制和同步都由master节点来处理,会照成master节点压力太大,使用主从从结构来解决

# Redis持久化

## Redis RDB和AOF的优缺点对比以及如何选择
**RDB的优点**
- RDB文件是紧凑的二进制文件，比较适合做冷备，全量复制的场景。
- 相对于AOF持久化机制来说，直接基于RDB数据文件来重启和恢复Redis进程，更加快速；
- RDB对Redis对外提供的读写服务，影响非常小，可以让Redis保持高性能，因为Redis主进程只需要fork一个子进程，让子进程执行磁盘IO操作来进行RDB持久化即可;
- RDB使用单独子进程来进行持久化，主进程不会进行任何IO操作，保证了Redis的高性能 ；

**RDB的缺点**
- 如果想要在Redis故障时，尽可能少的丢失数据，那么RDB没有AOF好。
- RDB每次在fork子进程来执行RDB快照数据文件生成的时候，如果数据文件特别大，可能会导致对客户端提供的服务暂停数毫秒，或者甚至数秒；
- RDB无法实现实时或者秒级持久化

**AOF的优点**
- AOF可以更好的保护数据不丢失(每隔1秒，后台线程执行一次fsync操作)
- AOF日志文件以append-only模式写入，写入性能比较高
- AOF日志文件即使过大的时候，出现后台重写操作，也不会影响客户端的读写。
- 适合做灾难性的误删除紧急恢复

**AOF的缺点**
- 对于同一份数据来说，AOF日志文件通常比RDB数据快照文件更大，恢复速度慢；
- AOF开启后，支持的写QPS会比RDB支持的写QPS低，因为AOF一般会配置成每秒fsync一次日志文件，当然，每秒一次fsync，性能也还是很高的；


## RDB和AOF到底该如何选择？
重启Redis时，我们很少使用rdb来恢复内存状态，因为会丢失大量数据。我们通常使用AOF日志重写，

但是AOF重写性能相对rdb来说要慢很多，这样在Redis实例很大的情况下，启动需要花费很长的时间。 

Redis 4.0 为了解决这个问题，带来了一个新的持久化选项——混合持久化。

AOF在进行文件重写时将重写这一刻之前的内存rdb快照文件的内容和增量的AOF修改内存数据的命令日志文件存在一起，都写入新的aof文件，新的文件一开始不叫appendonly.aof，等到重写完新的AOF文件才会进行改名，原子的覆盖原有的AOF文件，完成新旧两个AOF文件的替换。


## 为什么恢复的时候RDB比AOF快？
- AOF，存放的指令日志，做数据恢复的时候，其实是要回放和执行所有的指令日志，来恢复出来内存中的所有数据的；
- RDB，就是一份数据文件，恢复的时候，直接加载到内存中即可；





#  Redis常见的性能问题都有哪些？如何解决？
1. Master写内存快照，save命令调度rdbSave函数，会阻塞主线程的工作，当快照比较大时对性能影响是非常大的，会间断性暂停服务，所以Master最好不要写内存快照。
2. Master AOF持久化，如果不重写AOF文件，这个持久化方式对性能的影响是最小的，但是AOF文件会不断增大，AOF文件过大会影响Master重启的恢复速度。Master最好不要做任何持久化工作，包括内存快照和AOF日志文件，特别是不要启用内存快照做持久化,如果数据比较关键，某个Slave开启AOF备份数据，策略为每秒同步一次。
3. Master调用BGREWRITEAOF重写AOF文件，AOF在重写的时候会占大量的CPU和内存资源，导致服务load过高，出现短暂服务暂停现象。
4. Redis主从复制的性能问题，为了主从复制的速度和连接的稳定性，Slave和Master最好在同一个局域网内


# Redis六种淘汰key策略（默认时no-eviction）
- volatile-lru：在设置了过期时间的键空间中，移除最近最少使用的key
- allkeys-lru：移除最近最少使用的key
- volatile-random：在设置了过期时间的键空间中，随机移除一个key
- allkey-random：随机移除一个key
- volatile-ttl：在设置了过期时间的键空间中，移除将要过期的key
- no-eviction：在内存使用达到阈值的时候，所有引起申请内存的命令会报错






# Redis三种删除过期键策略
- 定时删除： 在设置键的过期时间的同时，创建一个定时器，让定时器执行对键的删除操作
- 惰性删除： 每次取的时候先判断 expires 对象里面的键是否已经过期，如果过期，则删除键，否则，返回该键
- 定期删除： 每隔一段时间，程序对数据库遍历检查一遍，然后删除过期的键

## 定时删除（并没有用到）
在设置键的过期时间的同时，创建一个定时器，让定时器在键的过期时间来临时，立即执行对键的删除操作；

定时删除操作对于内存来说是友好的，内存不需要操作，而是通过使用定时器，可以保证尽快的将过期键删除，但是对于CPU来说不是友好的，如果过期键比较多的话，起的定时器也会比较多，删除的这个操作会占用到CPU的资源；

## 惰性删除
放任键过期不管，但是每次从键空间中获取键是，都检查取得的键的过期时间，如果过期的话，删除即可；

惰性操作对于CPU来说是友好的，过期键只有在程序读取时判断是否过期才删除掉，而且也只会删除这一个过期键，但是对于内存来说是不友好的，如果多个键都已经过期了，而这些键又恰好没有被访问，那么这部分的内存就都不会被释放出来；

## 定期删除
每隔一段时间，程序就对数据库进行一次检查，删除掉过期键；

定期删除是上面两种方案的折中方案，每隔一段时间来删除过期键，并通过限制删除操作执行的时长和频率来减少删除操作对CPU时间的影响，除此之外，还有效的减少内存的浪费；但是该策略的难点在于间隔时长，这个需要根据自身业务情况来进行设置；

>目前，Redis采用的是惰性删除+定期删除的方案，通过配合使用，服务器可以很好的平衡 CPU 和内存。


# Redis的内存优化
1. redisObject对象
2. 缩减键值对象
3. 共享对象池
4. 字符串优化
5. 编码优化
6. 控制key的数量

# Redis4.0新特性
包含几个重大改进：更好的复制（PSYNC2），线程DEL / FLUSH，混合RDB + AOF格式，活动内存碎片整理，内存使用和性能改进。

## 一、主从数据同步机制
- PSYNC2: 新的一种主从复制同步机制。
- SYNC1:2.8~4.0之前版本的同步为PSYNC1
- psync1因为网络中断或者阻塞导致主从中断，恢复后必须重新到主节点dump一份全量数据同步到从节点。psync2再中断恢复后只需要同步复制延迟的那部分数据。
## 二、命令优化
线程DEL / FLUSH 优化

Redis现在可以在不同的线程中删除后台的key而不会阻塞服务器。 
## 三、慢日志记录客户端来源IP地址
## 四、混合RDB + AOF格式
混合RDB + AOF格式: 混合的RDB-AOF格式。 如果启用，则在重写AOF文件时使用新格式：重写使用更紧凑和更快的方式来生成RDB格式，并将AOF流附加到文件。 这允许在使用AOF持久性时更快地重写和重新加载。
## 五、内存使用和性能改进
1. Redis现在使用更少的内存来存储相同数量的数据。
2. Redis现在可以对使用的内存进行碎片整理，并逐渐回收空间(这个功能依然是试用阶段，可以通过参数不开启即可)





# 缓存解决方案分析

## 缓存雪崩
缓存雪崩是指缓存中数据大批量到过期时间，而查询数据量巨大，引起数据库压力过大甚至down机。从而形成一系列连锁反应，造成整个系统崩溃。 一般有三种处理办法：
1. 缓存数据的过期时间设置随机，防止同一时间大量数据过期现象发生。
2. 一般并发量不是特别多的时候，使用最多的解决方案是加锁排队。
3. 给每一个缓存数据增加相应的缓存标记，记录缓存的是否失效，如果缓存标记失效，则更新数据缓存。

## 缓存穿透
缓存穿透是指缓存和数据库中都没有的数据，而用户不断发起请求，如发起为id为“-1”的数据或id为特别大不存在的数据。这时的用户很可能是攻击者，攻击会导致数据库压力过大。

解决方案：
1. 接口层增加校验，如用户鉴权校验，id做基础校验，id<=0的直接拦截；
2. 从缓存取不到的数据，在数据库中也没有取到，这时也可以将key-value对写为key-null，缓存有效时间可以设置短点，如30秒（设置太长会导致正常情况也没法使用）。这样可以防止攻击用户反复用同一个id暴力攻击
3. 采用布隆过滤器，将所有可能存在的数据哈希到一个足够大的 bitmap 中，一个一定不存在的数据会被这个 bitmap 拦截掉，从而避免了对底层存储系统的查询压力

## 缓存击穿
缓存击穿是指缓存中没有但数据库中有的数据（一般是缓存时间到期），这时由于并发用户特别多，同时读缓存没读到数据，又同时去数据库去取数据，引起数据库压力瞬间增大，造成过大压力。和缓存雪崩不同的是，缓存击穿指并发查同一条数据，缓存雪崩是不同数据都过期了，很多数据都查不到从而查数据库。

解决方案：
1. 设置热点数据永远不过期。
3. 加互斥锁，互斥锁

## 缓存预热
缓存预热就是系统上线后，提前将相关的缓存数据直接加载到缓存系统。避免在用户请求的时候，先查询数据库，然后再将数据缓存的问题！用户直接查询事先被预热的缓存数据！

缓存预热解决方案：
1. 直接写个缓存刷新页面，上线时手工操作下；
2. 数据量不大，可以在项目启动的时候自动进行加载；
3. 定时刷新缓存；

## 缓存更新
除了缓存服务器自带的缓存失效策略之外（Redis默认的有6中策略可供选择），我们还可以根据具体的业务需求进行自定义的缓存淘汰，常见的策略有两种：
1. 定时去清理过期的缓存；
2. 当有用户请求过来时，再判断这个请求所用到的缓存是否过期，过期的话就去底层系统得到新数据并更新缓存。


# Redis Sentinel 与 Redis Cluster区别和各自适用场景
## Redis Sentinel
Redis-Sentinel(哨兵模式)是Redis官方推荐的高可用性(HA)解决方案，当用Redis做Master-slave的高可用方案时，假如master宕机了，Redis本身(包括它的很多客户端)都没有实现自动进行主备切换，而Redis-sentinel本身也是一个独立运行的进程，它能监控多个master-slave集群，发现master宕机后能进行自懂切换。它的主要功能有以下几点：
- 不时地监控redis是否按照预期良好地运行;
- 如果发现某个redis节点运行出现状况，能够通知另外一个进程(例如它的客户端);
- 能够进行自动切换。当一个master节点不可用时，能够选举出master的多个slave(如果有超过一个slave的话)中的一个来作为新的master,其它的slave节点会将它所追随的master的地址改为被提升为master的slave的新地址。

## Redis Cluster
- Redis Cluster是Redis的分布式解决方案，在Redis 3.0版本正式推出的，有效解决了Redis分布式方面的需求。**当遇到单机内存、并发、流量等瓶颈时，可以采用Cluster架构达到负载均衡的目的**。分布式集群首要解决把整个数据集按照分区规则映射到多个节点的问题，即把数据集划分到多个节点上，每个节点负责整个数据的一个子集。
- Redis Cluster采用哈希分区规则中的虚拟槽分区。虚拟槽分区巧妙地使用了哈希空间，使用分散度良好的哈希函数把所有的数据映射到一个固定范围内的整数集合，整数定义为槽（slot）。Redis Cluster槽的范围是0 ～ 16383。槽是集群内数据管理和迁移的基本单位。采用大范围的槽的主要目的是**为了方便数据的拆分和集群的扩展，每个节点负责一定数量的槽**。
- Redis Cluster采用虚拟槽分区，所有的键根据哈希函数映射到0 ～ 16383，计算公式：slot = CRC16(key)&16383。每一个实节点负责维护一部分槽以及槽所映射的键值数据。下图展现一个五个节点构成的集群，每个节点平均大约负责3276个槽，以及通过计算公式映射到对应节点的对应槽的过程。



# 为什么lua脚本结合Redis命令可以实现原子性？
Redis 提供了非常丰富的指令集，但是用户依然不满足，希望可以自定义扩充若干指令来完成一些特定领域的问题。Redis 为这样的用户场景提供了 lua 脚本支持，用户可以向服务器发送 lua 脚本来执行自定义动作，获取脚本的响应数据。Redis 服务器会单线程原子性执行 lua 脚本，保证 lua 脚本在处理的过程中不会被任意其它请求打断。

redis会为lua脚本执行创建伪客户端模拟客户端调用redis执行命令，伪客户端执行lua脚本是排他的，再加上redis是原子性的。


# Redis分布式锁会导致什么问题?
- 互斥性。在任意时刻，只有一个客户端能持有锁。
- 不会发生死锁。即使有一个客户端在持有锁的期间崩溃而没有主动解锁，也能保证后续其他客户端能加锁。
- 具有容错性。只要大部分的Redis节点正常运行，客户端就可以加锁和解锁。
- 解铃还须系铃人。加锁和解锁必须是同一个客户端，客户端自己不能把别人加的锁给解了。

业务逻辑执行太慢，比锁失效时间还长怎么办，redisson的WatchDog 会每10秒轮询，延长锁。

如果你很在乎高可用性，希望挂了一台 redis 完全不受影响，可以考虑 redlock。

# Redis有1000万个key，找出前缀为aaa的key的命令是什么？
- SCAN cursor [MATCH pattern] [COUNT count],指令指定返回条数
- SCAN    0   MATCH  aaa*   COUNT    5  表示从游标0开始查询aaa开头的key，每次返回5条，但是这个5条不一定，只是给Redis打了个招呼，具体返回数量看Redis心情。


# 热key问题
热Key问题
- 所谓热key问题就是，突然有几十万的请求去访问redis上的某个特定key。那么，这样会造成流量过于集中，达到物理网卡上限，从而导致这台redis的服务器宕机。

## 怎么发现热key
### 方法一:凭借业务经验，进行预估哪些是热key
其实这个方法还是挺有可行性的。比如某商品在做秒杀，那这个商品的key就可以判断出是热key。缺点很明显，并非所有业务都能预估出哪些key是热key。
### 方法二:在客户端进行收集
这个方式就是在操作redis之前，加入一行代码进行数据统计。那么这个数据统计的方式有很多种，也可以是给外部的通讯系统发送一个通知信息。缺点就是对客户端代码造成入侵。
### 方法三:在Proxy层做收集
有些集群架构是下面这样的，Proxy可以是Twemproxy，是统一的入口。可以在Proxy层做收集上报，但是缺点很明显，并非所有的redis集群架构都有proxy。
### 方法四:用redis自带命令
1. monitor命令，该命令可以实时抓取出redis服务器接收到的命令，然后写代码统计出热key是啥。当然，也有现成的分析工具可以给你使用，比如redis-faina。但是该命令在高并发的条件下，有内存增暴增的隐患，还会降低redis的性能。
2.hotkeys参数，redis 4.0.3提供了redis-cli的热点key发现功能，执行redis-cli时加上–hotkeys选项即可。但是该参数在执行的时候，如果key比较多，执行起来比较慢。
### 方法五:自己抓包评估
Redis客户端使用TCP协议与服务端进行交互，通信协议采用的是RESP。自己写程序监听端口，按照RESP协议规则解析数据，进行分析。缺点就是开发成本高，维护困难，有丢包可能性。

## 怎么设置redis失效时间、怎么设置永久有效？
**设置redis失效时间**
- expire <KEY> <TTL> : 将键的生存时间设为 ttl 秒
- pExpire <KEY> <TTL> :将键的生存时间设为 ttl 毫秒
-  expireAt <KEY> <timestamp> :将键的过期时间设为 timestamp 所指定的秒数时间戳
- pExpireAt <KEY> <timestamp>: 将键的过期时间设为 timestamp 所指定的毫秒数时间戳。

**redis设置了数据永不过期 **
- persist key持久化key，不设置失效时间，并用noeviction:默认回收策略，不淘汰，如果内存已满，添加数据是报错。


# Redis事务和MySQL事务有什么区别？
![](https://github.com/zaiyunduan123/Java-Interview/blob/master/image/Redis-5.png)