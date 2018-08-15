### mongodb 查询

#### 源生语句和pymongo查询的区别
*源生查询*
```
db.getCollection('表名').find()
```
*pymongo查询*

```python
db.表名.find()
# 查询时，所有字段需要控制格式，字符串加引号

# 排序
db.getCollection('#####').find({}).sort({date:-1})
```

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



