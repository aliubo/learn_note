## UUID

优点：性能好，本地生成，全局唯一。
缺点：
1. UUID长度固定为32位，对于Mysql索引来说，所有的非主键索引都会包含一个主键，UUID长度过长会不利于MySql的存储和性能。
2. UUID是乱序的，每一次UUID数据的插入都会对主键地城的b+树进行很大的修改。
3. 信息不安全，UUID里包含了MAC地址，芯片ID码能信息。会造成信息泄露。

## 数据库自增ID

对于多台数据库，可以设定不同的起始值以及跨度，可以实现全局自增ID，例如：
> 数据库1：起始1 跨度4 -> 1,5,9,...
> 数据库2：起始2 跨度4 -> 2,6,10,...
> 数据库3：起始3 跨度4 -> 3,7,11,...
> 数据库4：起始4 跨度4 -> 4,8,12,...

优点：容易存储，可以直接用数据库存储。
缺点：
1. 统水平扩展比较困难，定义好步长和机器台数之后,再增加数据库需要重调整所有的数据库起始值增值和自增值的跨度。
2. 数据库压力大，每次获取ID都会写一次数据库。
3. 信息不安全，递增性太强。很容根据两个ID的差值判断竞争对手的中间的出单量。

## Snowflake

生成一个64bit，由1bit标识位+41bit时间戳+10bit机器位+12bit序列号构成

优点：趋势递增，不依赖第三方组件（数据库等），性能更高，可以根据自身业务特点动态分配bit位。  
缺点：强依赖机器时钟，如果出现时钟回拨，那么整个系统生成的ID将会不可用。  



## nanoid