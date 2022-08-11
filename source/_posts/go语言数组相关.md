---
title: go语言数组相关
date: 2022-08-11 11:53:52
tags: [Go]
categories: golang开发
---

**go语言数组相关换算**
目前已有：交集，差集，去重
持续更新
<!--more-->

```go
package main

// 数组相关换算
// 交集，差集，去重

import (
    "fmt"
)

func main() {
    a := []int{98, 298, 588, 1598, 3698, 5000}
    b := []int{298, 588}

    // DiffArray 求两个切片的差集, 在a里面不在b里面
    diff_array := DiffArray(a, b)
    fmt.Println(diff_array)

    // 交集
    intersect_array := IntersectArray(a, b)
    fmt.Println(intersect_array)

    // 去重
    arr := []string{"a", "a", "b", "c"}
    remove_repeated := RemoveRepeatedElement(arr)
    remove_repeatedq := arrayUnique(arr)
    fmt.Println(remove_repeated)
    fmt.Println(remove_repeatedq)

}

// DiffArray 求两个切片的差集
func DiffArray(a []int, b []int) []int {
    var diffArray []int
    temp := map[int]struct{}{}

    for _, val := range b {
        if _, ok := temp[val]; !ok {
            temp[val] = struct{}{}
        }
    }

    for _, val := range a {
        if _, ok := temp[val]; !ok {
            diffArray = append(diffArray, val)
        }
    }

    return diffArray
}

// IntersectArray 求两个切片的交集
func IntersectArray(a []int, b []int) []int {
    var inter []int
    mp := make(map[int]bool)

    for _, s := range a {
        if _, ok := mp[s]; !ok {
            mp[s] = true
        }
    }
    for _, s := range b {
        if _, ok := mp[s]; ok {
            inter = append(inter, s)
        }
    }

    return inter
}

//切片去重实现
func arrayUnique(arr []string) []string {
    result := make([]string, 0, len(arr))
    temp := map[string]struct{}{}
    for i := 0; i < len(arr); i++ {
        if _, ok := temp[arr[i]]; ok != true {
            temp[arr[i]] = struct{}{}
            result = append(result, arr[i])
        }
    }
    return result
}

// RemoveRepeatedElement 切片去重实现
func RemoveRepeatedElement(arr []string) (newArr []string) {
    newArr = make([]string, 0)
    for i := 0; i < len(arr); i++ {
        repeat := false
        for j := i + 1; j < len(arr); j++ {
            if arr[i] == arr[j] {
                repeat = true
                break
            }
        }
        if !repeat {
            newArr = append(newArr, arr[i])
        }
    }
    return
}
```