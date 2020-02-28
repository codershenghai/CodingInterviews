# 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

示例:

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

# 题解

创建MinStack作为所求的数据结构。首先初始化两个栈，一个栈和普通栈一样，用于正常的push和pop，另一个作为辅助栈用于存放最小值。
 * push()：普通栈正常push，如果辅助栈为空，那么当前push的值肯定是最小值，直接存入辅助栈。如果push的值比当前辅助栈栈顶元素小，也可以存入辅助栈。
 * pop()：普通栈正常pop，如果普通栈pop的元素与辅助栈栈顶元素相同，那么辅助栈也pop。
 * top()：返回普通栈栈顶元素（不用删除）。
 * min()：辅助栈栈顶就是普通栈中的最小值，直接输出栈顶元素。

```java
class MinStack {
    public Stack<Integer> stack;
    public Stack<Integer> assist_stack;

    MinStack() {
        stack = new Stack<>();
        assist_stack = new Stack<>();
    }

    public void push(int node) {
        stack.push(node);
        if (assist_stack.empty() || node < assist_stack.peek())
            assist_stack.push(node);
    }

    public void pop() {
        int valPop = stack.pop();
        if (valPop == assist_stack.peek() && !stack.contains(valPop))
            assist_stack.pop();
    }

    public int top() {
        return stack.peek();
    }

    public int min() {
        return assist_stack.peek();
    }
}
```

