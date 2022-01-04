---
title: python时间时间换算 精确到毫秒
date: 2022-01-04 11:23:41
tags: Python
categories: 后端开发
---
**python时间时间换算 精确到毫秒**
<!--more-->
```python
import time
import datetime


def time_stamp1():
    """
    时间戳  精确到毫秒，17位
    :return:
    """
    ct = time.time()
    local_time = time.localtime(ct)
    data_head = time.strftime("%Y%m%d%H%M%S", local_time)
    data_secs = (ct - int(ct)) * 1000
    time_stamp = "%s%03d" % (data_head, data_secs)      # 17位时间戳
    return time_stamp
```

```python
def time_stamp2():
    """
    时间戳  精确到毫秒，20位
    :return:
    """
    time = datetime.datetime.now().strftime('%Y%m%d%H%M%S%f')       # 20位时间戳
    random_digit = ''.join(str(random.choice(range(8))) for _ in range(8))      # 8位随机数
    return (time+random_digit)
```