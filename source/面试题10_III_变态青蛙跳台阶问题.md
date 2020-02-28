# 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

# 题解一

使用动态规划的思想，当台阶只有1级时，显然只有1种跳法；当台阶有2两级时，有2种跳法（分两次跳或者一次直接跳上）。当台阶有i级时，有可能是从第i-1级跳上来，也可能是从第i-2级跳上来，也可能是从第i-1级跳上来......故有状态转移方程：
$$
dp[i] = dp[0] + dp[1] + ... + dp[i-1]
$$


```java
public int JumpFloorII(int target) {
    int[] dp = new int[target+1];
    dp[0] = 1;

    // dp[i] = dp[0] + dp[1] + ... + dp[i-1]
    for (int i = 1; i <= target; i++)
        for (int j = 0; j < i; j++)
            dp[i] += dp[j];
    
    return dp[target];
}
```

# 题解二

由于最后一个台阶必须存在，且青蛙可以一步登上第n级台阶，那么前n-1个台阶可以任意选择是否存在。假设跳上第n级台阶共有JumpFloorII(n)个选择，那么JumpFloorII(n) = 2 * JumpFloorII(n-1)。

```java
public int JumpFloorII(int target) {
    if (target == 1)
        return 1;
    return JumpFloorII(target-1) * 2;
}
```
