## LeetCode Design

### Data Structure

##### Find value

> Every time try to find a value index in int[], worst case is each value is the last element.
>
> Time complexity: O(n^2)

```java
for (int i = in_begin + 1; i <= in_end; i++) {
    if (inorder[i] == root.val) {
      in_root_index = i;
      break;
    }
}
```

> Same as list.indexOf(val)

```java
List<Integer> inorderList = Arrays.stream(inorder).boxed().collect(Collectors.toList());
inorderList.indexOf(root_val)
```

> Optimization: Add space complexity to reduce time complexity

```

```

