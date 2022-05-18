---
title: go语言除法四舍五入
date: 2022-05-18 16:03:13
tags: [Go]
categories: 后端开发
---
加0.5后向下取整
<!--more-->

```golang
func round(x float64) int64 {
	return int64(math.Floor(x + 0.5))
}
```