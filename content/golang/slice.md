---
categories: Programming
topic: Golang
title: "Understanding slice in Golang"
author:
  - M. Hasan
contributor:
#  - Contributor 1
synopsis: >
  A comprehensive guide on using slices in Golang
seoImageS: slice-s.jpg
seoImageL: slice-l.jpg
seoArticleSection: Programming
date: 2021-03-10T16:04:55+01:00
lastmod:
doi: 10.5281/zenodo.4593893
license: CC BY-SA 4.0
reference:
version: 1
nextVersion:
weight: 20
mathjax: false
draft: false
---

*A comprehensive guide on using slices in Golang*


&nbsp;

### Abstract

A slice is a data type that is mutable and points to an underlying array
consisting of an ordered sequence of elements that belong together.
Since the length of a slice changes dynamically, in the Golang world it
is widely used when the total number of elements is unknown or not fixed.


&nbsp;

### Contents

- Abstract
- Introduction
- Definition and declaration
- Indexing
- Modifying elements
- Appending elements
- Removing elements
- Multidimensional slices
- Summary


&nbsp;

### Introduction

Three important points that help use slices in any Golang project
proficiently:

- A slice holds a pointer to an underlying array. The array contains
the values of the elements, not the slice.

```go
a := []int{10, 20, 30}
fmt.Printf("%p\n", a)		// 0xc000018100
```

&nbsp;

- Length of a slice means how many elements from the underlying array
it uses.

```go
a := make([]int, 3, 5)
fmt.Println(len(a))		// 3
```

&nbsp;

- Capacity of a slice means the maximum number of elements the
underlying array can contain.

```go
fmt.Println(cap(a))		// 5
```

&nbsp;

When more elements than the existing capacity of the underlying array
need to be appended, the slice automatically resizes the array by
copying elements to a new and extended array. This gives the program
the ability to allocate memory dynamically when the number of elements
is not fixed.

Unlike arrays, for slices index bounds are not checked at compile-time.
Therefore, only a run-time error happens when an out-of-index is called
during the execution of a program.

```go
a := []int{10, 20, 30}
fmt.Println(a[3])		// panic: runtime error: index out of range [3] with length 3
```


&nbsp;

### Definition and declaration

**General schema I for declaring a slice**

`[]data_type{elements}`

&nbsp;

- All elements must be the same data type, e.g. `int` or `byte` or
`string`, etc.
- If the values of the elements along with the length and capacity are
not declared, the default slice is empty, the length is zero and the
capacity is also zero which will be changed dynamically upon appending
new elements to the slice.

```go
a := []int{}			// a = [], length = 0, capacity = 0
```

&nbsp;

**General schema II for declaring a slice**

`var := make([]data_type, length, capacity (optional))`

&nbsp;

```go
a := make([]int, 3)
// a = [], length = 3, capacity = 0 --> zeroed slice with a length of 3

b := make([]int, 3, 5)
// b = [], length = 3, capacity = 5 --> pre-allocated capacity of
// 5 elements in the underlying array	
```

&nbsp;

Sometimes it is hard to understand the values of each element with
`Println()` function when the data type is `string`:

```go
msg := []string{"hello world", "mars", "hello saturn", "jupiter"}
fmt.Println(msg)
// output: [hello world mars hello saturn jupiter]
```

&nbsp;

With `Printf()` function and `%q` verb this problem can be solved:

```go
fmt.Printf("%q\n", msg)
// output: ["hello world" "mars" "hello saturn" "jupiter"]
```


&nbsp;

### Indexing

Each element saved in the underlying array of a slice corresponds to an
index number starting from 0 and counting up. In Golang, it is not
allowed to index backward with a negative number.

```go
fmt.Println(msg[0])		// hello world
fmt.Println(msg[1])		// mars
fmt.Println(msg[2])		// hello saturn
fmt.Println(msg[3])		// jupiter
```

&nbsp;

It is possible to concatenate the same data types using indices.

```go
fmt.Println(msg[0] + " and hello from " + msg[1])
// output: hello world and hello from mars
```


&nbsp;

### Modifying elements

With the index number of the underlying array, elements of a slice
can be updated.

```go
msg[1] = "hello mars"
fmt.Printf("%q\n", msg)
// output: ["hello world" "hello mars" "hello saturn" "jupiter"]
```


&nbsp;

### Appending elements

When a slice's underlying array capacity is full but a new element
needs to be appended, the slice will:

- declare a new array having a capacity of twice as large as the
existing array
- copy everything from the existing array to the newly created array
- append the new element to the new array

In this way, it dynamically changes its length and capacity during
run-time.

```go
length := 0
c := "Array Capacity: "
l := "Slice Length: "
p := "Pointed to: "

scores := make([]int, length)
fmt.Println(scores)		// []
fmt.Print(c)
fmt.Println(cap(scores))	// Array Capacity: 0
fmt.Print(l)
fmt.Println(len(scores))	// Slice Length: 0
fmt.Print(p)
fmt.Printf("%p\n", scores)	// Pointed to: 0x589a28
fmt.Println("")

scores = append(scores, 100)
fmt.Println(scores)		// [100]
fmt.Print(c)
fmt.Println(cap(scores))	// Array Capacity: 1 (capacity increased)
fmt.Print(l)
fmt.Println(len(scores))	// Slice Length: 1
fmt.Print(p)
fmt.Printf("%p\n", scores)	// Pointed to: 0xc0000140d0
fmt.Println("")			// (new location for a new array)

scores = append(scores, 200)
fmt.Println(scores)		// [100 200]
fmt.Print(c)
fmt.Println(cap(scores))	// Array Capacity: 2 (capacity doubled)
fmt.Print(l)
fmt.Println(len(scores))	// Slice Length: 2
fmt.Print(p)
fmt.Printf("%p\n", scores)	// Pointed to: 0xc0000140e0
fmt.Println("")			// (new location for a new array)

scores = append(scores, 300)
fmt.Println(scores)		// [100 200 300]
fmt.Print(c)
fmt.Println(cap(scores))	// Array Capacity: 4 (capacity doubled)
fmt.Print(l)
fmt.Println(len(scores))	// Slice Length: 3
fmt.Print(p)
fmt.Printf("%p\n", scores)	// Pointed to: 0xc000018120
fmt.Println("")			// (new location for a new array)

scores = append(scores, 400)
fmt.Println(scores)		// [100 200 300 400]
fmt.Print(c)
fmt.Println(cap(scores))	// Array Capacity: 4
fmt.Print(l)
fmt.Println(len(scores))	// Slice Length: 4
fmt.Print(p)
fmt.Printf("%p\n", scores)	// Pointed to: 0xc000018120
fmt.Println("")

scores = append(scores, 500)
fmt.Println(scores)		// [100 200 300 400 500]
fmt.Print(c)
fmt.Println(cap(scores))	// Array Capacity: 8 (capacity doubled)
fmt.Print(l)
fmt.Println(len(scores))	// Slice Length: 5
fmt.Print(p)
fmt.Printf("%p\n", scores)	// Pointed to: 0xc0000160c0
fmt.Println("")			// (new location for a new array)

scores = append(scores, 600)
fmt.Println(scores)		// [100 200 300 400 500 600]
fmt.Print(c)
fmt.Println(cap(scores))	// Array Capacity: 8
fmt.Print(l)
fmt.Println(len(scores))	// Slice Length: 6
fmt.Print(p)
fmt.Printf("%p\n", scores)	// Pointed to: 0xc0000160c0
fmt.Println("")

scores = append(scores, 700)
fmt.Println(scores)		// [100 200 300 400 500 600 700]
fmt.Print(c)
fmt.Println(cap(scores))	// Array Capacity: 8
fmt.Print(l)
fmt.Println(len(scores))	// Slice Length: 7
fmt.Print(p)
fmt.Printf("%p\n", scores)	// Pointed to: 0xc0000160c0
fmt.Println("")

scores = append(scores, 800)
fmt.Println(scores)		// [100 200 300 400 500 600 800]
fmt.Print(c)
fmt.Println(cap(scores))	// Array Capacity: 8
fmt.Print(l)
fmt.Println(len(scores))	// Slice Length: 8
fmt.Print(p)
fmt.Printf("%p\n", scores)	// Pointed to: 0xc0000160c0
fmt.Println("")

scores = append(scores, 900)
fmt.Println(scores)		// [100 200 300 400 500 600 900]
fmt.Print(c)
fmt.Println(cap(scores))	// Array Capacity: 16 (capacity doubled)
fmt.Print(l)
fmt.Println(len(scores))	// Slice Length: 9
fmt.Print(p)
fmt.Printf("%p\n", scores)	// Pointed to: 0xc00001e100
fmt.Println("")			// (new location for a new array)
```

&nbsp;

When the capacity is defined during the definition of the slice, its
capacity is doubled based on that pre-defined capacity.

```go
a := make([]int, 3, 5)
a[0] = 10
a[1] = 20
a[2] = 30

fmt.Println(a)			// [10 20 30]
fmt.Print("Length: ")
fmt.Println(len(a))		// Length: 3
fmt.Print("Capacity: ")
fmt.Println(cap(a))		// Capacity: 5
fmt.Println("")

a = append(a, 40, 50, 60)

fmt.Println(a)			// [10 20 30 40 50 60]
fmt.Print("Length: ")
fmt.Println(len(a))		// Length: 6
fmt.Print("Capacity: ")
fmt.Println(cap(a))		// Capacity: 10
```

&nbsp;

*Note:* Defining the capacity is optional. But the performance of a
program is enhanced significantly when the underlying array's initial
capacity is defined.


&nbsp;

### Removing elements

Golang does not have any built-in function to delete elements from a
slice. To remove an element, the slice needs to be sliced out and
appended together again.

If an element needs to be removed whose index is `i`, first all the
items before and after the `i-th` index must be sliced out and then
those sliced out items have to be appended together. 

So, the new slice will be,

`slice = append(slice[:i], slice[i+1:]...)`

&nbsp;

Since the removal process does not require the slice to increase the
capacity of the underlying array, the array capacity remains the same.
A slice does not decrease the capacity of the underlying array
dynamically.

```go
a = append(a[:0], a[1:]...)	// removing the element at index 0

fmt.Println(a)			// [20 30 40 50 60]
fmt.Print("Length: ")
fmt.Println(len(a))		// Length: 5
fmt.Print("Capacity: ")
fmt.Println(cap(a))		// Capacity: 10
fmt.Println("")

a = append(a[:3], a[4:]...)	// removing the element at index 3

fmt.Println(a)			// [20 30 40 60]
fmt.Print("Length: ")
fmt.Println(len(a))		// Length: 4
fmt.Print("Capacity: ")
fmt.Println(cap(a))		// Capacity: 10
```


&nbsp;

### Multidimensional slices

A slice can consist of other slices as elements to provide multidimensional
feature.

```go
Array2x := [][]string{{"lion", "tiger", "wolf"}, {"hawk", "eagle"}}

fmt.Println(Array2x[0][0])	// lion
fmt.Println(Array2x[0][1])	// tiger
fmt.Println(Array2x[0][2])	// wolf

fmt.Println(Array2x[1][0])	// hawk
fmt.Println(Array2x[1][1])	// eagle
```


&nbsp;

### Summary

This tutorial demonstrates the concept of slices in Golang, how they
ease the development phase, and dynamically increases the capacity
of the underlying array during run-time.
