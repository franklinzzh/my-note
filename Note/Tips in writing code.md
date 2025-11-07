# Tips in writing code

## 1.

Convert char to int:

```java
char c = '7';
int i = Integer.parseInt(String.valueOf(c));
int i = c - '0';
int i = Character.getNumericValue(ch);
```

Convert String to int:

```java
String s = "7";
int i = Integer.parseInt(s);
int i = Integer.valueOf(s.substring(0, 1))
```

Reading: https://www.geeksforgeeks.org/java-program-to-convert-char-to-int/

