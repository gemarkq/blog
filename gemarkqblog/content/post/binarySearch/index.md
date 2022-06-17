---
author: "Jiankun Qiu"
title: "Bug Free Binary Search Implementation"
date: "2022-06-17"
description: "This article shows about two different ways to write a bug free Binary Search Code"
enableEmoji: true
tags: ["binarySearch"]
categories: ["algorithm"]
series: ["Algorithm Learning"]
image: "mountain.png"
---

The cover picture is salt piles and condenser ponds in Bonaire, Dutch Caribbean. *[Picture source.](https://www.theatlantic.com/photo/2020/02/top-shots-2019-international-landscape-photographer-year/606505/)*

## What is Binary Search?

***Binary Search*** is a searching algorithm used in a sorted array by **repeatedly dividing the search interval in half**. The idea of binary search is to use the information that the array is sorted and reduce the time complexity to ```O(log n)```

**Steps:**

- Begin with the mid element of the whole array as a search key.
- if the value of the search key is equal to the item then return an index of the search key
- Or if the value of the search key is less than the item in the middle of the interval, narrow the interval to the lower half.
- Otherwise, narrow it to the upper half
- Repeatedly check from the second point until the value is found or the interval is empty.

:flags: Although the logic of the algorithm is very simple, I believe we all meet the problem :shit: whether to use ```<= ``` or ```<```, whether to use ```left = mid + 1``` or ```left = mid```. When the iteration is end, which result (```left or right```) should I return?

I will introduce two different implementation of the algorithm. Of Course, they are bug free !!!!!!!! :satisfied::satisfied::satisfied::satisfied:

## Return the first value that is no less than the target

**The array should be non-descending order !!!**

```java
public int lower_bound(int[] array, int left, int right, int target) {
    while(left < right) {
        int mid = left + (right - left) / 2;
        if(array[mid] < target) {
            left = mid + 1;
        }else {
            right = mid;
        }
    }
    return left;
}


int left = 0;
int right = array.length;

For example:
array: 0 1 2 3 3 3 4 5 6
target: 3
Return index: 3
    
array: 0 1 2 4 5 6
target: 3
Return index:3 (the result is index 3, which is 4)
```

**The searching interval is ```[left, right)```**

```int mid = left + (right - left) / 2;``` is to **avoid the Integer overflow.**

## Return the first value that is greater than the target

**The array should be non-descending order !!!**

```java
public int upper_bound(int[] array, int left, int right, int target) {
    while(left < right) {
        int mid = left + (right - left) / 2;
        if(array[mid] <= target) {
            left = mid + 1;
        }else {
            right = mid;
        }
    }
    return left;
}


int left = 0;
int right = array.length;

For example:
array: 0 1 2 3 3 3 4 5 6
target: 3
Return index: 6 (the reuslt is index 6, which is 4)

array: 0 1 2 4 5 6
target: 3
Return index: 3 (the result is index 3, which is 4) 
```

**The searching interval is ```[left, right)```**

**The biggest difference** between ```upper_bound``` and ```lower_bound```

- if the target is existed, the ```upper_bound``` will return the first value that is greater than the target.
- if the target is existed, the ```lower_bound``` will return the first index of the target in the array.

**The common** of the two functions:

- if the target is not existed, they will return a index. if we insert target in this index, the array will be sill sorted.



## Reference

> [Binary Search - GeeksforGeeks](https://www.geeksforgeeks.org/binary-search/)

