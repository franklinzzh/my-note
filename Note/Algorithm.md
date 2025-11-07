### Algorithm

###### 滑动窗口+双指针

###### 二分查找

框架：

```java
int binarySearch(int[] nums, int target) {
    int left = 0, right = ...;
    while(...) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            ...
        } else if (nums[mid] < target) {
            left = ...
        } else if (nums[mid] > target) {
            right = ...
        }
    }
    return ...;
}
```

[left, right]	

```java
// nums already sorted.
int binarySearch(int[] nums, int target) {
	int left = 0;
    int right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            return mid;
        }
    }
    return -1;
}
```

左侧边界（lowBoundary）

```java
int left_bound(int[] nums, int target) {
	int left = 0;
    int right = nums.length;
    while (left < right) {
        int mid =left + (right - left) / 2;
        if (nums[mid] == target) {
            right = mid;
        } else if (nums[mid] > target) {
            right = mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        }
    }
    return left;
    //若返回-1，需判断是否越界
    // 如果索引越界，说明数组中无目标元素，返回 -1
    if (left < 0 || left >= nums.length) {
        return -1;
    }
}
```

返回值： 第一个满足 `nums[i] >= target` 的位置

```java
// 在一个有序数组中，找到「小于 target 的最大元素的索引」
// 比如说输入 nums = [1,2,2,2,3]，target = 2，函数返回 0，因为 1 是小于 2 的最大元素。
// 再比如输入 nums = [1,2,3,5,6]，target = 4，函数返回 2，因为 3 是小于 4 的最大元素。
int floor(int[] nums, int target) {
    // 当 target 不存在，比如输入 [4,6,8,10], target = 7
    // left_bound 返回 2，减一就是 1，元素 6 就是小于 7 的最大元素
    // 当 target 存在，比如输入 [4,6,8,8,8,10], target = 8
    // left_bound 返回 2，减一就是 1，元素 6 就是小于 8 的最大元素
    return left_bound(nums, target) - 1;
}
```

**为什么 `left = mid + 1`，`right = mid` ？和之前的算法不一样？**

答：这个很好解释，因为我们的「搜索区间」是 `[left, right)` 左闭右开，所以当 `nums[mid]` 被检测之后，下一步应该去 `mid` 的左侧或者右侧区间搜索，即 `[left, mid)` 或 `[mid + 1, right)`。

**为什么返回 `left` 而不是 `right`？**

答：都是一样的，因为 while 终止的条件是 `left == right`。

```java
int lowBoundary(int[] nums, int target) {
        int left = 0;
        int right = nums.length;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] > target) {
                right = mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left;
        // if (left < 0 || left >= nums.length) {
        //     return -1；
        // }
        // return nums[left] == target ? left : -1;
    }

    int highBoundary(int[] nums, int target) {
        int left = 0;
        int right = nums.length;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] > target) {
                right = mid;
            // 小于target的最大索引
            // 因为一直在更新 left = mid + 1; 直到 left = right
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                left = mid + 1;
            }
        }
        return left - 1;
        // //未找到target 返回-1
        // if (left - 1 < 0 || left - 1 >= nums.length) {
        //     return -1;
        // }
        // return nums[left - 1] == target ? left - 1 : -1;
    }
```





