# Interesting Knowledge

### - XOR

###### AND

> 0 AND 0 = 0
> 1 AND 0 = 0
> 0 AND 1 = 0
> 1 AND 1 = 1

###### OR

> 0 OR 0 = 0
> 1 OR 0 = 1
> 0 OR 1 = 1
> 1 OR 1 = 1

###### [XOR](https://www.chiark.greenend.org.uk/~sgtatham/quasiblog/xor/)	

> XOR is Exclusive OR;
>
> -  if either input is true, then the result is true; 
> -  but if both inputs are true, then the result is false.
>
> 0 XOR 0 = 0
> 1 XOR 0 = 1
> 0 XOR 1 = 1
> 1 XOR 1 = 0





### - 子集

Subset(子集)：不连续

Subsequence(子序列)：按顺序 但可不连续

Subarray(子数组)：必须连续





# Tips

Convert char to int:

```java
char c = '7';
int i = Integer.parseInt(String.valueOf(c));
int i = c - '0';
int i = Character.getNumericValue(ch);
```

Convert String to int:

```java
String seq = "20001001";
int Year = Integer.praseInt(seq.substring(0,4));
int Day = Integer.valueOf(s.substring(6, 8))
```

> ```
> str.substring(begin, end)
> ```

> Params: 
>
> * `beginIndex`  – the begin index, inclusive.
>
> * `endIndex`  – the end index, exclusive.

[Reading](https://www.geeksforgeeks.org/java-program-to-convert-char-to-int/) for more Convert.



