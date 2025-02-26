## 88. Merge Sorted Arrays 🧩

**Difficulty**: `Easy` - **Tags**: `Array`, `Two Pointers`, `Sorting`

---

### Description 📋

You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

Merge `nums1` and `nums2` into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to 0 and should be ignored. `nums2` has a length of `n`.

### Examples 🌟

**Example 1:**

**Input:**
```python
nums1 = [1,2,3,0,0,0]
m = 3
nums2 = [2,5,6]
n = 3
```

**Output:**
```python
[1,2,2,3,5,6]
```

**Explanation:**
The arrays we are merging are `[1,2,3]` and `[2,5,6]`. The result of the merge is `[1,2,2,3,5,6]` with the underlined elements coming from `nums1`. ✨

**Example 2:**

**Input:**
```python
nums1 = [1]
m = 1
nums2 = []
n = 0
```

**Output:**
```python
[1]
```

**Explanation:**
The arrays we are merging are `[1]` and `[]`. The result of the merge is `[1]`. 🎯

**Example 3:**

**Input:**
```python
nums1 = [0]
m = 0
nums2 = [1]
n = 1
```

**Output:**
```python
[1]
```

**Explanation:**
The arrays we are merging are `[]` and `[1]`. The result of the merge is `[1]`. Note that because `m = 0`, there are no elements in `nums1`. The 0 is only there to ensure the merge result can fit in `nums1`. 🛠️

### Constraints ⚙️

- `nums1.length == m + n`
- `nums2.length == n`
- `0 <= m, n <= 200`
- `1 <= m + n <= 200`
- `-10^9 <= nums1[i], nums2[j] <= 10^9`

### Solution 💡

```charp
1. 复制到一个数组中，用Collections API排序
    public class Solution {
        public void Merge(int[] nums1, int m, int[] nums2, int n) {
            for (int i = m, j = 0; j < n; i++, j++) {
                nums1[i] = nums2[j];
            }
            Array.Sort(nums1);
        }
    }
    
    public class Solution {
        public void Merge(int[] nums1, int m, int[] nums2, int n) {
            Array.Copy(nums2, 0, nums1, m, n);
            Array.Sort(nums1);
        }
    
    时间复杂度：O((m+n)log(m+n))，其中 m 和 n 分别是数组 nums1和 nums2的元素个数。复制元素需要 O(n) 的时间，排序需要 O((m+n)log(m+n)) 的时间。
    空间复杂度：O(log(m+n))，其中 m 和 n 分别是数组 nums 1和 nums 2的元素个数。排序需要 O(log(m+n)) 的递归调用栈空间。

2.  双指针
    public class Solution {
        public void Merge(int[] nums1, int m, int[] nums2, int n) {
            int i = m - 1, j = n - 1, k = m + n - 1;
            while (i >= 0 && j >= 0) {
                if (nums1[i] >= nums2[j]) {
                    nums1[k--] = nums1[i--];
                } else {
                    nums1[k--] = nums2[j--];
                }
            }
            while (i >= 0) {
                nums1[k--] = nums1[i--];
            }
            while (j >= 0) {
                nums1[k--] = nums2[j--];
            }
        }
    }
    
    时间：O(m+n),空间O(1)

    作者：Storm
    链接：https://leetcode.cn/problems/merge-sorted-array/solutions/1765744/by-stormsunshine-aoru/
    来源：力扣（LeetCode）
    著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
    ```

