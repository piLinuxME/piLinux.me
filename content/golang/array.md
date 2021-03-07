---
categories: Programming
topic: Golang
title: "Understanding array in Golang"
author:
  - M. Hasan
contributor:
#  - Contributor 1
synopsis: >
  A comprehensive guide on using arrays in Golang
seoImageS: array-s.png
seoImageL: array-l.png
seoArticleSection: Programming
date: 2021-03-07T00:53:22+01:00
lastmod:
doi: 10.5281/zenodo.4587469
license: CC BY-SA 4.0
reference:
  - 1. 6.2 Array Types - Computer Science Programming Basics in Ruby [Book], accessed March 6, 2021, https://www.oreilly.com/library/view/computer-scienceprogramming/9781449356835/sixdot2_array_types.html
  - 2. i Gopher Guides, Understanding Arrays and Slices in Go, DigitalOcean, accessed March 6, 2021, https://www.digitalocean.com/community/tutorials/understanding-arrays-and-slices-in-go
version: 1
nextVersion:
weight: 10
mathjax: false
draft: false
---

*A comprehensive guide on using arrays in Golang*


&nbsp;

### Abstract

An array is a data structure or a collection of an ordered sequence of elements[1] that belong together.
Arrays enable condensing the code and performing the same methods and operations on multiple values at once[2].


&nbsp;

### Contents

- Abstract
- Introduction
- Definition and declaration
- Indexing
- Counting elements
- Modifying elements
- Summary
- References


&nbsp;

### Introduction

In Golang, an array refers to a continuous memory of a segment that stores elements of the same data type.
Its capacity is defined at creation time which can no longer be changed. If the capacity is unknown during
creation time, a programmer should take the privilege of using slices. While slices have the dynamic capacity,
it comes at a cost - less performant.

- Unlike slices, arrays are not reference or pointer types. It saves the actual values.
- Arrays are hashable which can be used as keys in maps and this makes it comparable.
- Index bounds are checked at compile-time that gives the array higher compile-time safety.

```go
a := [5]int{}
a[5] = 10 // compile-time error: invalid array index 5 (out of bounds for 5-element array)
```

&nbsp;

- Assigning array values makes a copy of the entire array implicitly.

```go
a := [5]int{1, 2, 3, 4, 5}
b := a
b[2] = 10 // it affects only b; a remains the same
```

&nbsp;

- Arrays are quite useful for sequences of fixed size, e.g. IP addresses. For IPv4, `[4]byte` provides a
compile-time guarantee that the value passed to the function will have exactly 4 bytes, while for IPv6
`[16]byte` provides the compile-time guarantee.

It is wise to use arrays where the data structure does not need a dynamic number of elements since one-time
memory allocation increases the speed and performance of the program besides many other advantages.


&nbsp;

### Definition and declaration

General schema for declaring an array:

`[size]data_type{elements}`

&nbsp;

- All elements must be the same data type, e.g. `int` or `byte` or `string`, etc.
- If the values of the elements are not declared, the default is zero-valued.

```go
a := [5]int{}     // a = [0 0 0 0 0]
b := [5] byte{}   // b = [0 0 0 0 0]
c := [5] string{} // c = [    ]
```

&nbsp;

If an array stored in a variable is printed out with `Println()` function, sometimes it is hard to
understand the values of each element:

```go
msg := [5]string{"hello world", "mars", "hello saturn", "jupiter"}
fmt.Println(msg)
// output: [hello world mars hello saturn jupiter ]
```

&nbsp;

With `Printf()` function and `%q` verb this problem can be solved:

```go
fmt.Printf("%q\n", msg)
// output: ["hello world" "mars" "hello saturn" "jupiter" ""]
```


&nbsp;

### Indexing

Each element in an array corresponds to an index number starting from 0 and counting up. In Golang,
it is not allowed to index backward with a negative number.

```go
fmt.Println(msg[0])  // hello world
fmt.Println(msg[1])  // mars
fmt.Println(msg[2])  // hello saturn
fmt.Println(msg[3])  // jupiter
fmt.Println(msg[4])  // 
```

&nbsp;

It is possible to concatenate the same data types.

```go
fmt.Println(msg[0] + " and hello from " + msg[1])
// output: hello world and hello from mars
```


&nbsp;

### Counting elements

With the built-in `len()` function, the length of the array can be found.

```go
fmt.Println(len(msg)) // 5
```


&nbsp;

### Modifying elements

Indexing provides greater control over the data in an array by allowing changing the elements.

```go
msg[1] = "hello mars"
fmt.Printf("%q\n", msg)
// output: ["hello world" "hello mars" "hello saturn" "jupiter" ""]
```

&nbsp;

**Note:** It is not possible to change the size or capacity of an array once it is defined.
Therefore, only an existing element can be changed, but a new element cannot be added or
removed from the array.


&nbsp;

### Summary

This tutorial demonstrates how array works, discusses the advantages and limitations.
When the size of the data structure is known, an array can act as a powerful tool to
increase the overall performance of the program. Slices play an amazing role when
data structure size is unknown.
