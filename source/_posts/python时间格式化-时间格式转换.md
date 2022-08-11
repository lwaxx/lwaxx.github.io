---
title: python时间格式化/时间格式转换
date: 2022-03-09 15:29:40
tags: [python]
categories: 后端开发
---
python时间格式化/时间格式转换
<!--more-->

```python
"""获取某个时间"""
import datetime
import time
from dateutil import relativedelta

# 上月(eg: 202201)
last_month = (datetime.datetime.now() + relativedelta.relativedelta(months=-1)).strftime("%Y%m")

# 当月(eg: 202202)
issue_no = time.strftime("%Y%m")

# 下月(eg: 202203)
nextmonth = (datetime.date.today() + relativedelta.relativedelta(months=1)).strftime("%Y%m")

# 年月日（eg:2022-03-01）
now = datetime.datetime.now().strftime('%Y-%m-%d')
now = datetime.datetime.now().strftime("%Y%m%d")

# 年月日时分秒（eg:2022-03-01 00:00:00）
now = datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S')

# 当月第一天，下月第一天
month_first_day = datetime.date(year=today.year, month=today.month, day=1)
next_clear_day = month_first_day + relativedelta(months=1)

# 3天前的日期 
threeDayAgo = (datetime.datetime.now() - datetime.timedelta(days = 3)) 

# 31天后的日期
starttime = datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S')
endtime = (datetime.datetime.now() + datetime.timedelta(days=31)).strftime('%Y-%m-%d 00:00:00')
```

```python
"""时间转换"""
import time
import datetime

# 时间戳转字符串格式时间
timestamp = time.time()     # 当前时间戳
strtime = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime(timestamp))

# 字符串格式时间转时间戳
now_str = "2022-03-09 00:00:00"
now_time = time.strptime(now_str,'%Y-%m-%d %H:%M:%S')
timestamp = time.mktime(now_time)

# 当前时间30分钟后时间日期，35分钟后时间日期
start_time1 = (datetime.datetime.now()+datetime.timedelta(minutes=30)).strftime("%Y-%m-%d %H:%M:%S")
end_time1 = (datetime.datetime.now()+datetime.timedelta(minutes=30)+datetime.timedelta(minutes=5)).strftime("%Y-%m-%d %H:%M:%S")
print(start_time1)
print(end_time1)


# 下周一零点
today = datetime.datetime.today()
wd = today.weekday()    # 周几，从0开始算
next_monday = datetime.datetime(today.year, today.month, today.day) + datetime.timedelta(days=7-wd)
print(today)
print(wd)
print(next_monday)


# 24小时之后的时间
expire = today + datetime.timedelta(hours=24)
print(expire)
```

```python
# python日期格式化
week = time.strftime("%A")
```

> #### 附：python日期格式化符号
> 
> %y 两位数的年份表示（00-99）
%Y 四位数的年份表示（000-9999）
%m 月份（01-12）
%d 月内中的一天（0-31）
%H 24小时制小时数（0-23）
%I 12小时制小时数（01-12）
%M 分钟数（00=59）
%S 秒（00-59）
%a 本地简化星期名称
%A 本地完整星期名称
%b 本地简化的月份名称
%B 本地完整的月份名称
%c 本地相应的日期表示和时间表示
%j 年内的一天（001-366）
%p 本地A.M.或P.M.的等价符
%U 一年中的星期数（00-53）星期天为星期的开始
%w 星期（0-6），星期天为星期的开始
%W 一年中的星期数（00-53）星期一为星期的开始
%x 本地相应的日期表示
%X 本地相应的时间表示
%Z 当前时区的名称
%% %号本身
