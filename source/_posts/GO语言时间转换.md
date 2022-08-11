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

		// 周一
	on_monday, next_monday := getBgnEnd(now)
	fmt.Println(on_monday, next_monday)

	// 下月1号零点
	next_month_0 := GetNextMonthStartTs()
	fmt.Println(next_month_0)

	// 本月1号零点
	on_month_0 := GetFirstDateOfMonth(now)
	fmt.Println(on_month_0)
}

//返回周一的字符串和下周一零点的字符串
func getBgnEnd(curT time.Time) (string, string) {
	curW := int(curT.Weekday()) - 1
	if curW == -1 { //星期天当成7
		curW = 6
	}
	curM := curT.AddDate(0, 0, -curW)
	tmpMondayTime := time.Date(curM.Year(), curM.Month(), curM.Day(), 0, 0, 0, 0, time.Local).Format("2006-01-02 15:04:05")
	tmpMondayStr := curM.Format("20060102")
	tmpT, _ := time.ParseInLocation("20060102", tmpMondayStr, time.Local)
	tmpDeadLineTime := tmpT.AddDate(0, 0, 7).Format("2006-01-02 15:04:05")
	return tmpMondayTime, tmpDeadLineTime
}

//返回周一的字符串和下周一零点的时间
func getBgnEnd1(curT time.Time) (string, time.Time) {
	// 一天滚一次
	tmpDayStr := curT.Format("20060102")
	tmpT, _ := time.ParseInLocation("20060102", tmpDayStr, time.Local)
	tmpDeadLineTime := tmpT.AddDate(0, 0, 1)
	return tmpDayStr, tmpDeadLineTime
}

// 下月1号零点
func GetNextMonthStartTs() time.Time {
	now := time.Now()
	nowYeah, nowMonth, _ := now.Date()
	loc := now.Location()
	return time.Date(nowYeah, nowMonth, 1, 0, 0, 0, 0, loc).AddDate(0, 1, 0)
}

// 本月1号零点
func GetFirstDateOfMonth(d time.Time) time.Time {
	d = d.AddDate(0, 0, -d.Day()+1)
	return GetZeroTime(d)
}

//获取某一天的0点时间
func GetZeroTime(d time.Time) time.Time {
	return time.Date(d.Year(), d.Month(), d.Day(), 0, 0, 0, 0, d.Location())
}

```