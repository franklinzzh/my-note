### Algorithm

#### -滑动窗口+双指针

#### -二分查找

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

#### -递归

​	递归分为`遍历`和`分解问题`

> `遍历型`递归的重点是「**走完所有路径**」，而不是「当前路径的值会如何影响最终结果」。它更关注**完整地访问状态空间**，而不是**组合子问题结果**。
>
> - 我们不关心 `path` 的值是否影响后面结果；
> - 关键是“**所有可能的 path 都被访问到**”；
> - 即使某条路径“没意义”，我们也会走到终点，然后自然被过滤掉。
>
> 遍历的主要作用：**收集叶子节点上的结果的作用**
>
> `分解型`递归关心**当前子问题的结果**，因为它要被合并进最终答案。
>
> - 每次递归返回一个“子问题的结果”；
> - 父层利用这些结果进行**计算 / 组合 / 汇总**
> - 当前路径的状态直接影响最终结果。

​	遍历：void	分解：return T

​	对于一些题目，两种方法都可行，只不过写起来不太一样，但效率相同

##### 	总结

- 首先，这个问题是否可以抽象成一棵**树结构**？如果可以，那么就要用递归算法了。
- 如果要用递归算法，那么就思考「**遍历**」和「**分解**问题」这两种思维模式，看看哪种**更适合**这个问题。
- 如果用「**分解**问题」的思维模式，那么一定要写清楚这个**递归函数的定义**是什么，然后利用这个定义来分解问题，利用子问题的答案推导原问题的答案；如果用「**遍历**」的思维模式，那么要用一个**无返回值**的递归函数，单纯起到遍历递归树，收集目标结果的作用。

> 「分解问题」的思维模式就对应着后面要讲解的 [动态规划算法](https://labuladong.online/algo/essential-technique/dynamic-programming-framework/) 和 [分治算法](https://labuladong.online/algo/essential-technique/divide-and-conquer/)，「遍历」的思维模式就对应着后面要讲解的 [DFS/回溯算法](https://labuladong.online/algo/essential-technique/backtrack-framework/)。



#### -二叉树核心算法

`traverse` 函数：一个遍历二叉树所有节点的函数

```java
//遍历数组
traverse(int[] arr, int i) {
	if (index == arr.length) {
        return;
    }
    // 前序位置
    traverse(arr, i + 1);
    // 后序位置	
}

// 迭代遍历单链表
void traverse(ListNode head) {
    for (ListNode p = head; p != null; p = p.next) {

    }
}
//遍历链表
traverse(ListNode head) {
    if (head.next == null) {
        return;
    }
    traverse(head.next);	
}
```

Binary Tree could also use `while` loop to traverse:

```java
void inorderIterative(TreeNode root) {
    Stack<TreeNode> stack = new Stack<>();
    TreeNode curr = root;

    while (curr != null || !stack.isEmpty()) {
        // go left as far as possible
        while (curr != null) {
            stack.push(curr);
            curr = curr.left;
        }

        curr = stack.pop();
        System.out.println(curr.val); // visit node
        curr = curr.right;            // go right next
    }
}

```

BFS use `queue` to do Level-Order traverse.

##### 前序 中序 后序

> 利用**递归**实现各个节点的**遍历**
>
> 而像层序遍历，就使用的不是递归方法

空间复杂度 `O(n)`  **时间复杂度 `O(n)`** 

> 每调用一个 `traverse()` 方法都要调用一个栈帧



**前(pre-order) 中(in-order) 后序(post-order)是遍历二叉树过程中处理每一个节点的三个特殊时间点**，绝不仅仅是三个顺序不同的 List：

- 前序位置的代码在刚刚进入一个二叉树节点的时候执行；
- 后序位置的代码在将要离开一个二叉树节点的时候执行；
- 中序位置的代码在一个二叉树节点左子树都遍历完，即将开始遍历右子树的时候执行。

LeetCode 226 [翻转二叉树](https://leetcode.cn/problems/invert-binary-tree/description/)

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        traverse(root);
        return root;
    }
    void traversePre(TreeNode root) {
        if (root == null) return;
      	// pre-order
        TreeNode memo = root.left;
        root.left = root.right;
        root.right = memo;
      
        traversePre(root.left);
        traversePre(root.right);
    }
  	void traverseIn(TreeNode root) {
        if (root == null) return;
      	//in-order
        traverseIn(root.left);
      	TreeNode memo = root.left;
        root.left = root.right;
        root.right = memo;
        traverseIn(root.left);
    }
}
```

> 此刻如果使用中序遍历，要注意此时root.left/root.right已经变化
>
> 所以 `traverseIn(root.right)` 就会将原始的 `root.left` 重新traverse一遍；
>
> 导致 `traverse(root.left)` 两遍 — 即返回最初状态；而 `root.right` 子树完全未触及
>
> * 输入： [4,2,7,1,3,6,9]
> * 输出： [4,7,2,6,9,1,3]
> * 预期结果： [4,7,2,9,6,3,1]



##### 序列化和反序列化

> **当二叉树中节点的值不存在重复时**：
>
> 1. 如果你的序列化结果中**不包含空指针的信息**，且你只给出**一种**遍历顺序，那么你无法还原出唯一的一棵二叉树。
>
> 2. 如果你的序列化结果中**不包含空指针的信息**，且你会给出**两种**遍历顺序，分两种情况：
>
>    （详情见二叉树构建 -- preorder/inorder/postorder）
>
>    * 如果你给出的是前序和中序，或者后序和中序，那么你可以还原出唯一的一棵二叉树。
>
>    * 如果你给出前序和后序，那么你无法还原出唯一的一棵二叉树。
>
> 3. 如果你的序列化结果中**包含空指针的信息**，且你只给出**一种**遍历顺序，也要分两种情况：
>
>    * 如果你给出的是前序或者后序，那么你可以还原出唯一的一棵二叉树。
>
>    * 如果你给出的是中序，那么你无法还原出唯一的一棵二叉树。



##### Lowest Common Ancestor

-LC236

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251215105034338.png" alt="image-20251215105034338" style="zoom:50%;" />

<img src="/Users/franklin/Desktop/NO_Drive/Code/myWeb/Note/Screenshot/image-20251215105049624.png" alt="image-20251215105049624" style="zoom:50%;" />

Only two possible cases.

* Case 1: Two nodes on differet left, right trees
* Case 2: Two nodes on the same subtree, with one node is a child of another.

The base case is, always return the node when finding the match one.

```java
if (root.val == p.val || root.val == q.val) return root;
```

Then in post-order place, handling the logic whether return `root`  , or `left/right node` returned from recursive calls.

```java
// for case 1
if (left != null && right != null) return root;

// for case 2
return left != null ? left : right;
```

Why this base case works for case 2?

> Since it is placed in the pre-order place, it always reach the `root` first. 
>
> Also, `p` and `q` always exist in the tree. 





#### - 分治

Divide and conquer

#### - 遍历

traverse

* 回溯（backtrack）
* DFS



#### - 回溯

```java
// 回溯算法框架
void backtrack(...) {
    // base case
    if (...) return;

    for (int i = 0; i < ...; i++) {
        // 做选择
        ...

        // 进入下一层决策树
        backtrack(...);

        // 撤销刚才做的选择
        ...
    }
}
```



#### -回溯/DFS/动态规划 区别联系

##### 回溯/DFS

回溯/DFS是针对递归不同需要，在for loop内/外 「做选择」，进行的递归算法，本质一样。

`backtrack` / `dfs` / `travese` 均不需要返回值 

* 遍历思维 -- 无返回值
* 分解问题 -- 有返回值

##### base case && 剪枝

 ... 待补充

```java
void backtrack(...) {
    // base case
    if (reached the leaf node) {
        // 到达叶子节点，结束递归
        return;
    }

    for (int i = 0, i < n; i++) {
        // 剪枝逻辑
        if (...) {
            // 第 i 个选择不满足条件则跳过
            continue;
        }

        // 做选择
        ...

        backtrack(...)

        // 撤销选择
        ...
    }
}
```



##### 回溯/DFS vs DP

- 动态规划算法属于分解问题（分治）的思路，它的关注点在整棵「子树」。
- 回溯算法属于遍历的思路，它的关注点在节点间的「树枝」。[[LC46-全排列](https://leetcode.cn/problems/permutations/)]
- DFS 算法属于遍历的思路，它的关注点在单个「节点」。

```java
// DFS 算法把「做选择」「撤销选择」的逻辑放在 for 循环外面
void dfs(Node root) {
    if (root == null) return;
    // 做选择
    print("enter node %s", root);
    for (Node child : root.children) {
        dfs(child);
    }
    // 撤销选择
    print("leave node %s", root);
}

// 回溯算法把「做选择」「撤销选择」的逻辑放在 for 循环里面
void backtrack(Node root) {
    if (root == null) return;
    for (Node child : root.children) {
        // 做选择
        print("I'm on the branch from %s to %s", root, child);
        backtrack(child);
        // 撤销选择
        print("I'll leave the branch from %s to %s", child, root);
    }
}
```

> DFS  关注单个当前节点的信息
>
> 回溯 则考虑两节点之间的信息
>
> **回溯 = 带状态恢复的 DFS。**
>  DFS 只走路；回溯在走路的同时考虑“走哪条、撤回来再试另一条”。



#### 层序遍历

```java
// 输入一棵二叉树的根节点，层序遍历这棵二叉树
void levelTraverse(TreeNode root) {
    if (root == null) return;
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    int depth = 1;
    while (!q.isEmpty()) {
        int size = q.size();
        for (int i = 0; i < size; i++) {
            TreeNode cur = q.poll();
           	if (cur.left != null) {
                q.offer(cur.left);
            }
            if (cur.right != null) {
                q.offer(cur.right);
            }
        }
        depth++;
    }
}
```

