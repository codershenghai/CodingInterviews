# 题目描述

小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!

# 题解一

第一种是暴力法，即首先从一个数字开始，然后判断以它为起点的序列和是否等于s。如果以它为起点的序列和以及大于s，则进行剪枝。

```java
public ArrayList<ArrayList<Integer>> FindContinuousSequence(int sum) {
    ArrayList<ArrayList<Integer>> res = new ArrayList<>();
    int total = 0;
    for (int i = 1; i < sum; i++) {
        for (int j = i; j < sum; j++) {
            total += j;
            if (total > sum) {
                total = 0;
                break;
            }
            else if (total == sum) {
                ArrayList<Integer> arr = new ArrayList<>();
                for (int k = i; k <= j; k++)
                    arr.add(k);
                res.add(arr);
                total = 0;
                break;
            }
        }
    }
    return res;
}
```

# 题解二

第二种方法是使用双指针，只是这里的指针代表的不是数组下标，而是数字。开始时把left初始化为1，right初始化为2。每次使用求和公式求序列和：

- 如果序列和小于sum，则扩大序列的范围，即right++；
- 如果序列和大于sum，则缩小序列的范围，即left+；
- 如果序列和等于sum，则找到一个结果。然后扩大序列的范围，即right++。

```java
public ArrayList<ArrayList<Integer>> FindContinuousSequence(int sum) {
    int left = 1, right = 2;
    ArrayList<ArrayList<Integer>> res = new ArrayList<>();
    while (left < right && left <= sum/2) {
        int cur_sum = (left+right) * (right-left+1) / 2;
        if (cur_sum < sum)
            right++;
        else if (cur_sum > sum)
            left++;
        else {
            ArrayList<Integer> arr = new ArrayList<>();
            for (int i = left; i <= right; i++)
                arr.add(i);
            res.add(arr);
            left++;
        }
    }
    return res;
}
```