今天刷了第一道 LeetCode 算法题, esay 级别,完事开头难:

1.Two Sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have ***exactly\*** one solution, and you may not use the *same* element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

刚开始想到的就是两个 for 循环遍历，如下：

~~~javascript
var twoSum = function(nums, target) {
    let indices = []
    let len = nums.length
    for(let i = 0; i < len; i++){
        for(let j = 0; j < len; j++) {
            if(i != j && target - nums[j] === nums[i]) {
                return [i, j]
            }
        }
    }
    return indices
};
twoSum([2, 7, 11, 15], 9)
~~~

但提交后，执行效率很惨，击败 16% 的 JavaScript。。。这也是意料之中，后面为什么会想到 map 去执行呢，我觉得还可以研究下 map 的数据结构

下面的代码终于是满意的结果，解题思路就懒得描述了

~~~JavaScript
var twoSum = function(nums, target) {
    const map = new Map()
    for (let i = 0; i < nums.length; i += 1) {
        const value = nums[i]
        const num1 = target - value
        const num2 = map.get(num1)
        if (num2 !== undefined) {
            return [num2, i]
        }
        map.set(value, i)
    }
};
~~~

执行效率击败 90+% JavaScript。



接着我又想用 Swift 写一下：

~~~swift
class Solution {
    func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
        var map = [Int:Int]()
        for (index, value) in nums.enumerated() {
            if map[target - value] != nil {
                return [index, map[target - value]!]
            }
            map[value] = index
        }
        return []
    }
}
~~~

