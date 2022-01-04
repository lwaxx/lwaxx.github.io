---
title: GO语言时间转换
date: 2022-01-04 11:19:53
tags: [Go]
categories: 后端开发
---

**使用go语言进行不同时间类型之间的转换**
<!--more-->

```golang
package main

import (
	"fmt"
	"time"
)

func main() {
	// 2021-07-23 15:36:00.346234 +0800 CST m=+0.000174001
	now := time.Now()

	// 格式化 2021-07-23 15:36:00
	time1 := time.Now().Format("2006-01-02 15:04:05")

	// unix时间戳格式化
	time2 := now.Unix()                                        // 1627025820
	time3 := time.Unix(time2, 0).Format("2006-01-02 15:04:05") // 2021-07-23 15:37:00

	// 当前时间加/减一分钟
	time4 := now.Add(time.Minute * time.Duration(1))
	time5 := now.Add(-(time.Minute * time.Duration(1)))

	// 时间比较大小，先转为以下格式
	// 1970-01-01 08:00:00 +0800 CST

	time6, _ := time.ParseInLocation("2006-01-02 15:04:05", time3, time.Local)
	if now.Before(time6) {
		fmt.Println("true")
	} else if now.After(time6) {
		fmt.Println("false")
	}
}
```