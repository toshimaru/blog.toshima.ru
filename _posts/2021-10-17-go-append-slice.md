---
layout: post
title: "[Go]Append item to slice"
tags: go
---

## `append` Usage

```go
func append(slice []Type, elems ...Type) []Type
```

> The append built-in function appends elements to the end of a slice.

[builtin package - builtin - pkg.go.dev](https://pkg.go.dev/builtin#append)

## Example

### Add a item to slice

```go
var s []int
s = append(s, 1)
fmt.Println(s) // [1]
```

### Add multiple items to slice

```go
var s []int
s = append(s, 1)
fmt.Println(s) // [1 2 3 4 5]
```

### Add another slice to slice

```go
var s []int
s2 := []int{3, 4, 5}
s = append(s, s2...)
fmt.Println(s) // [3 4 5]
```

## See also

- [Appending to a slice \| A Tour of Go](https://tour.golang.org/moretypes/15)
- [builtin package - builtin - pkg.go.dev](https://pkg.go.dev/builtin)
