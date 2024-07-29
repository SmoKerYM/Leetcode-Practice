给你两个按 **非递减顺序** 排列的整数数组 `nums1` 和 `nums2`，另有两个整数 `m` 和 `n` ，分别表示 `nums1` 和 `nums2` 中的元素数目。

请你 **合并** `nums2` 到 `nums1` 中，使合并后的数组同样按 **非递减顺序** 排列。

 **注意：** 最终，合并后数组不应由函数返回，而是存储在数组 `nums1` 中。为了应对这种情况，`nums1` 的初始长度为 `m + n`，其中前 `m` 个元素表示应合并的元素，后 `n` 个元素为 `0` ，应忽略。`nums2` 的长度为 `n` 。


### My Answer

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        # Establish a negative pointer (starting from the last element)
        i = -1
        while True:

            # if the pointer is bigger than the length of nums2, break
            if i * -1 > n:
                break

            # copy the element from nums2 to nums1
            nums1[i] = nums2[i]

            i -= 1
      
        nums1.sort()

```

### Standard Answer

直接使用 `[m:]`的取索引方式，将从 `nums1 `数组中的第 `m` 位开始的值变成nums2中的值

```python
nums1[m:] = nums2
nums1.sort()
```
