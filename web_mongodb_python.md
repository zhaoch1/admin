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



```

```

