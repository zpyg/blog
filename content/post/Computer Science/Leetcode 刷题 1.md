---
title: "Leetcode 刷题 1"
description: "written in python"
date: 2022-07-16T11:53:30+08:00
categories:
  - Computer Science
tags: [algorithms, leetcode, python]
math: true
---

https://www.bilibili.com/video/BV1sy4y1q79M

## 1. 两数之和

> 有人相爱，有人夜里开车看海，有人 leetcode 第一题都做不出来。

### 暴力法

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i+1, len(nums), 1):
                if nums[i] + nums[j] == target:
                    return i, j
```

### 哈希表法

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # hashtable {num: num_index, ...}
        M = {nums[index]: index for index in range(len(nums))}
        for a_index in range(len(nums)):
            a = nums[a_index]
            # a + b = target ==> a = target - b
            b = target - a # 假设存在这样的 b
            if b in M.keys() : # 存在则说明没问题
                b_index = M[b]
                if a_index != b_index: # 还不能是同一个元素（题目要求元素不可重复使用）
                    return a_index, b_index
```

## 时间复杂度

### 定义

对算法执行效率的估计

算法执行时间与输入的关系

常用`大O表示法`，其他可参考《算法导论》

### 计算

忽略常数，找 for、while 等循环语句

常见的有
$O(N)$、$O(M + N)$、$O(N^2)$、$O(2^N)$、$O(\log{N})$、$O(N \log{N})$

#### _e.g._$O(N)$

```python
def f(N):
  total = 0
  for i in range(N): # 执行 N 次
    total += i
  return total
```

#### _e.g._ $O(log N)$

```python
def binary_search(sorted_collection: list[int], item: int) -> int | None:
    """二分搜索

    :param sorted_collection: some ascending sorted collection with comparable items
    :param item: item value to search
    :return: index of found item or None if item is not found

    Examples:
    >>> binary_search([0, 5, 7, 10, 15], 0)
    0

    >>> binary_search([0, 5, 7, 10, 15], 15)
    4

    >>> binary_search([0, 5, 7, 10, 15], 5)
    1

    >>> binary_search([0, 5, 7, 10, 15], 6)

    """
    left = 0
    right = len(sorted_collection) - 1

    while left <= right:
        midpoint = left + (right - left) // 2
        current_item = sorted_collection[midpoint]
        if current_item == item:
            return midpoint
        elif item < current_item:
            right = midpoint - 1
        else:
            left = midpoint + 1
    return None
```

每次问题规模减小一半, _i.e._

$$
  n * (\frac{1}{2})^k = 1
$$

n 为问题的规模，在 k 次后等于 1, 即问题解决；
在这个例子中，
则意为待搜索的数组每次都会减小一半，在 k 次后就会确定要搜索的数。

归纳一下可得

$$
  n * \frac{1}{2^k} = 1
$$

$$
  n = 2^k
$$

$$
  k = \log_2{n}
$$

这也就有了二分搜索的时间复杂度 $O(log N)$

## 空间复杂度

O(1) 空间，变量等
O(n) 空间，一维数组等
...

log 用不上

## 数组

### 485. 最大连续 1 的个数

```python
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
    # 若题目未给出 nums 不为空
    # if not nums:
    #   return 0
    count = 0
    result = 0
    for i in nums:
       if i == 1:
         count = count + 1
       else: # i 不是 0 就是 1<分类讨论>
         result = max(result, count)
         count = 0
    return max(result, count)
```

### 283. 移动零

#### 脑洞大开解法

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        # nums.sort(key=lambda i: 1 if i == 0 else 0), i.e.
        nums.sort(key= lambda i: i == 0)
```

#### （算是一种）双指针法

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        # 将所有非 0 元素移到前面
        index = 0
        for i in nums:
            if i != 0:
                # 第 index 个非零元素移动到nums[index]
                nums[index] = i
                index += 1
        # 将剩下部分以 0 填充
        for i in range(index, len(nums)):
            nums[i] = 0
```

#### 27. 移除元素

##### 类似 283

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        # 把不等与 val 的都移到前面
        index = 0
        for i in nums:
            if i != val:
                nums[index] = i
                index += 1
        # 把后面几个等于 val 的都删掉
        for _ in range(index, len(nums)):
            nums.pop(-1)
        return len(nums)
```

#### 标准双指针法

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
      if not nums:
        return 0
      l = 0
      r = len(nums) - 1
      while l < r:
        while l < r and nums[l] != val:
          l += 1
        while l < r and nums[r] == val:
          r -= 1
        # 双指针的目的 通过交换 将 val 与 !val 划分开
        nums[l], nums[r] = nums[r], nums[l]
      return l if nums[l] == val else l + 1
```
