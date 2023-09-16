---
title: mysql批量插入数据 excutemany
date: 2022-01-04 11:25:31
tags: [Python, Mysql, Databse]
categories: 后端开发
# top: true
---

> 问题：
> 往数据库批量插入10条数据的时候，在for循环里面使用excute插入，接口请求耗时>1s，严重影响效率；
<!--more-->
> 遂考虑使用excutemany批量插入，接口请求耗时400ms

> 逐条插入：cursor.excute()
> 批量插入：cursor.excutemany()
> 使用：executemany(templet, args)
> templet：sql模板字符串，例如：insert into table(id,name) values(%s,%s)
> args: 模板字符串中的参数，是一个list或者tuple, eg: [(1,"a"),(2,"b")] 或者 ((1,"a"),(2,"b"))

```python
# 实例-节选
import time

draw_list = [...]   # len(draw_list) = 10
sql = ''' insert into table(remix_uid, stage, tp, price, draw_result) values (%s,%s,%s,%s,%s)'''

cursor = db.cursor()
start_time = time.time()
for i in draw_list:
    cursor.excute(sql, [args])
end_time = time.time() - start_time
print(end_time)  # >1s
```

修改为以下：
```python
cursor = db.cursor()
start_time = time.time()

data = ((item[''], item[''], ...) for item in draw_list)
cursor.executemany(sql, data)

end_time = time.time() - start_time
print(end_time)  # 400ms
```

