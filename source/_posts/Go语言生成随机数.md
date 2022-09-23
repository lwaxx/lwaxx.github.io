---
title: Go语言生成随机数
date: 2022-01-04 11:22:24
tags: [Go]
categories: 后端开发
---
**使用go语言生成随机数**
<!--more-->

```golang
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main() {
	// 由于go语言未提供2个区间参数，只一个参数的情况下先随机0到(m-n)，再用加 n 的方式解决
	// 例：[5, 10], 先生成[0,5], 再加5

	// go取随机数需要指定一个随机种子
	// 种子一般使用当前的系统时间，这是完全随机的。

	for i := 0; i < 50; i++ {
		// res := getRandomWithAll(5, 10)
		// res := getRandomWithMin(5, 10)
		// res := getRandomWithMax(5, 10)
		res := getRandomWithNo(5, 10)
		fmt.Println(res)
	}

}

// 包含上下限 [min, max]
func getRandomWithAll(min, max int) int64 {
	rand.Seed(time.Now().UnixNano())
	return int64(rand.Intn(max-min+1) + min)
}

// 不包含上限 [min, max)
func getRandomWithMin(min, max int) int64 {
	rand.Seed(time.Now().UnixNano())
	return int64(rand.Intn(max-min) + min)
}

// 都不包含 (min, max]
func getRandomWithMax(min, max int) int64 {
	var res int64
	rand.Seed(time.Now().UnixNano())
Restart:
	res = int64(rand.Intn(max-min+1) + min)
	if res == int64(min) {
		goto Restart
	}
	return res
}

// 都不包含 (min, max)
func getRandomWithNo(min, max int) int64 {
	var res int64
	rand.Seed(time.Now().UnixNano())
Restart:
	res = int64(rand.Intn(max-min) + min)
	if res == int64(min) {
		goto Restart
	}
	return res
}
```