### mongodb 查询

#### 源生语句和pymongo查询的区别
*源生查询*
```
db.getCollection('表名').find()
```
*pymongo查询*

```python
db.表名.find()
# 查询时，所有字段需要控制格式，字符串加引号，返回一个pymongo对象，做遍历查询时需要list做转换成列表

db.表明.find_one()
返回一个mongodb文档，可以直接用字典方法提取

# 排序
db.getCollection('#####').find({}).sort({date:-1})

# python中查询id值时可以通过前段传来的id值通过objectid对象来传递查询
kw = db.表名.find_one({'_id': ObjectId(str(_id)))
```
*pymongo插入*
pymongo的数据格式是BSON格式
```python
#  生成唯一ID值的方法
from bson import ObjectId

#  ObjectId前4个字节表示时间戳，接下来的3个字节是机器标识码，紧接的两个字节由进程id组成（PID），最后三个字节是随机数。
a = ObjectId()

#  可以通过getTimestamp函数来获取文档的创建时间
ObjectId("5349b4ddd2781d08c09890f4").getTimestamp()
#  返回对象是ISO格式的文档穿件时间：
ISODate("2014-04-12T21:49:17Z")

```
mongodb 有固定集合可以覆盖之前的纪录
#### 聚合查询 pymongo和源生通用
*aggregate*
```python
# $match 匹配

    alarm = db.alarm.aggregate([
        {'$match': {'seat': seat}},
        {'$group': {
            #  按条件聚合查询
            '_id': {'company_id': '$company_id', 'seat': '$seat', 'customer': '$customer', 'date': '$date'},
            #  增加词组
            'wangwang': {'$addToSet': '$wangwang'},
            'alert_time': {'$addToSet': '$alert_time'},
            'emotion': {'$addToSet': '$emotion'},
            'keyword': {'$addToSet': '$keyword'},
            'rule': {'$addToSet': '$rule'},
        }},
        # 从第几条开始
        {'$skip': startIndex},
        # 返回数量限制
        {'$limit': limit}
    ])

```



