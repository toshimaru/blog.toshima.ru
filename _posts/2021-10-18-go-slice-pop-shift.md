---
layout: post
title: "[Go]How to pop/shift slice"
tags: go
---

## slice

```go
s := []int{1, 2, 3, 4, 5}
fmt.Println(s) // [1 2 3 4 5]
```

## pop

```go
pop, s1 := s[len(s)-1], s[:len(s)-1]
fmt.Println(s1) // [1 2 3 4]
fmt.Println(pop) // 5
```

## shift

```go
shift, s2 := s[0], s[1:]
fmt.Println(s2) // [2 3 4 5]
fmt.Println(shift) // 1
```
