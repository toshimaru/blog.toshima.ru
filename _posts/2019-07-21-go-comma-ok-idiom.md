---
layout: post
title: "[Go]comma ok idiom"
tags: go
---

Have you ever seen Go code like this?

```go
if seconds, ok := timeZone[tz]; ok {
    return seconds
}
```

This is called “comma ok” idiom

> For obvious reasons this is called the “comma ok” idiom.

via. [Effective Go - The Go Programming Language](https://golang.org/doc/effective_go.html)

## Simple Map 

Let's take a deeper look.

```go
var timeZone = map[string]int{
        "UTC": 0 * 60 * 60,
        "EST": -5 * 60 * 60,
        "CST": -6 * 60 * 60,
        "MST": -7 * 60 * 60,
        "PST": -8 * 60 * 60,
}
var val1 = timeZone["PST"]
var val2 = timeZone["invalid"]
fmt.Printf("val1: %d val2: %d\n", val1, val2)
```

The output is:

```
val1: -28800 val2: 0
```

If the key is found in map, it returns the value, otherwise, it returns zero value - in this examaple it returns `0`.

## Multiple Assignment

How about multiple assignment? let's see an examaple.

```go
var val1, ok1 = timeZone["PST"]
var val2, ok2 = timeZone["invalid"]
fmt.Printf("val1: %d ok1: %t val2: %d ok2: %t\n", val1, ok1, val2, ok2)
```

The output is:

```
val1: -28800 ok1: true val2: 0 ok2: false
```

If the key is found in map, it returns the value with `true`, otherwise, it returns `0` with `false`.

## comma ok idiom

Let's back to the first exmaple:

```go
if seconds, ok := timeZone[tz]; ok {
    return seconds
}
```

This means that if the key(`tz`) is found in `timeZone` map, it returns `seconds` with  `true`(`ok`).

This idiom is handy when you'd like to configure fallback value:

```go
if seconds, ok := timeZone[tz]; ok {
    return seconds
}

log.Println("unknown time zone:", tz)
return fallbackValue
```
