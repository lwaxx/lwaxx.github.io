---
title: 获取指定范围符合正态分布的随机数Go/Python
date: 2022-01-04 10:47:08
tags: [Go, Python]
categories: 后端开发
---

## Box-Muller算法
> 当x和y是两个独立且服从（0，1）均匀分布的随机变量时，有：
> <center>Z1 = cos(2\pi x)*\sqrt{-2ln(1-y))}</center>
> <center>Z2 = sin(2\pi x)*\sqrt{-2ln(1-y))}</center>
> 
> Z1和Z2独立且服从标准正态分布，当带入均值和方差时:
> <center>Z = Z1(Z2)*\sigma +\mu</center>
<!--more-->
​
### 均值sigma，标准差mu计算:

> 根据正态分布的 3sigma法则，5-10范围的均值和方差，和[5,6,7,8,9,10]差不多
> 故：5-10范围的均值：(5+10)/2=7.5
> 标准差：(10-7.5)/3
> s = [5,6,7,8,9,10]
> mu = np.mean(s) # 均值
> sigma = np.std(s) # 标准差
> var = np.var(s) # 方差


go生成符合正态分布随机数：
```golang
import (
	"fmt"
	"math"
	"math/rand"
	"time"
)

func GetGaussRandomNum(min, max int64) int64 {
	σ := (float64(min) + float64(max)) / 2
	μ := (float64(max) - σ) / 3
	rand.Seed(time.Now().UnixNano())
	x := rand.Float64()
	x1 := rand.Float64()
	a := math.Cos(2*math.Pi*x) * math.Sqrt((-2)*math.Log(x1))
	result := a*μ + σ
	return int64(result)
}

func main() {
	for i := 1; i < 1000; i++ {
		result := GetGaussRandomNum(30, 60)
		fmt.Println(result)
	}
}
```

python生成符合正态分布随机数：
```python
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
import random


# 方法一
def getGaussRandomNum(min, max):
    # 比如 生成   50-100  范围内的正态分布的数，均值为75
    # 据 3 sigma 法则，取标准差为 （100-75）/3 = 8.33
    # mu, sigma = 75, 8.33
    # 30-60 mu=45 sig=(60-45)/3=5
    mu = (min + max) / 2
    sigma = (max - mu) / 3
    s = np.random.normal(mu, sigma, 1)
    return int(s)
    # sns.set_palette("hls") #设置所有图的颜色，使用hls色彩空间
    # sns.distplot(s,color="r",bins=1000,kde=True) #绘制直方图，color设置颜色，bins设置直方图的划分数
    # plt.show() #显示验证结果


# 方法二
def getGaussRandomNum1(min, max):
    mu = (min + max) / 2
    sigma = (max - mu) / 3
    s = random.gauss(mu, sigma)
    return int(s)
```