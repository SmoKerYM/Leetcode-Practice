给你一个 **非严格递增排列** 的数组 `nums` ，请你**[ 原地](http://baike.baidu.com/item/%E5%8E%9F%E5%9C%B0%E7%AE%97%E6%B3%95)** 删除重复出现的元素，使每个元素 **只出现一次** ，返回删除后数组的新长度。元素的 **相对顺序** 应该保持 **一致** 。然后返回 `nums` 中唯一元素的个数。

考虑 `nums` 的唯一元素的数量为 `k` ，你需要做以下事情确保你的题解可以被通过：

* 更改数组 `nums` ，使 `nums` 的前 `k` 个元素包含唯一元素，并按照它们最初在 `nums` 中出现的顺序排列。`nums` 的其余元素与 `nums` 的大小不重要。
* 返回 `k` 。

### My Answer

与"delete_(element==val)_from_list"改题中的思路类似，使用快慢双指针实现在原数组上进行修改。

```Python
def removeDuplicates(self, nums: List[int]) -> int:
    sole_nums = set()
    left = 0
    n = len(nums)

    for right in range(0, n):
        e = nums[right]
        # if this element appear the first time
        if e not in sole_nums:
            sole_nums.add(e)
            nums[left] = e
            left += 1
  
    return left
```

### Analytics

使用快慢双指针的思路并没有错，但是我忽略了题目中的一个关键条件“ordered list”，这意味着重复元素会挨在一起，无需建立新的set去检测下一个元素是不是重复元素（因为不是随机排列）。

当我们把“ordered list”的条件纳入考量之后，数组只会以 `aabcccddeeee` 的形式排列，因此我们在”条件比较“的时候只需要把 `右指针` 指向的元素与 `右指针-1`指向的元素对比即可。

### Standard Answer

```Python
def removeDuplicates(self, nums: List[int]) -> int:  
	n = len(nums)
	# 从1开始是因为第一位肯定是要取的，减少遍历次数
    	fast = slow = 1
    	while fast < n:
        	if nums[fast] != nums[fast - 1]:
            		nums[slow] = nums[fast]
            		slow += 1
        	fast += 1
  
    	return slow

```

### Insights

1. 如果题目中提到"不严格递增""递增""有序"数组，则优先考虑在数组内进行比较，而非新建一个新的数据类型进行暂存。
2. 比较的条件与对象不一定与两个指针都有关系，在本题目中，左指针仅仅负责存放新数据，右指针仅仅负责逻辑判断与数值对比。
