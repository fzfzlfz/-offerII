#### [剑指 Offer 03. 数组中重复的数字](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

**示例 1：**

```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

 

**限制：**

```
2 <= n <= 100000
```



我的代码

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        //1.用set
        // Set<Integer> set = new HashSet<>();
        // for(int i = 0; i < nums.length; i++){
        //     if(set.contains(nums[i])) return nums[i];
        //     set.add(nums[i]);
        // }
        // return -1;

        //2.改变正负
        for(int i = 0; i < nums.length; i++){
            int idx = Math.abs(nums[i]);
            if(nums[idx] < 0){
                return idx;
            }
            nums[idx] = -nums[idx];
        }
        return 0;
    }
}
```

解题思路：

**方法一**： 用set， 向set中放入元素

每次放入前判断set中是否已有该元素

if**有**，那么证明**这个元素是重复的那个**

else 直接放入set中

重复如上步骤， 如果完成循环还没找到重复的元素，那么证明没有重复的元素，返回-1



**方法二**：利用数组下标

本质思想和set一致，由于数组中的元素都是 0～n-1，因此可以通过改变正负来标记是否在set中

比如访问的数组是 2 1 1 1

```apl
一开始会把下标为2的标记

因此变为 2 1 -1 1

然后会把下标为1 的标记

因此变为 2 -1 -1 1

然后会把下标为1的标记

此时发现已经是负数了，因此可知 1 这个位置已经被访问过了

1就是重复的元素

```

这里需要注意，这道题目的前提是，一定是有重复的数

因此，对于方法二，可能会出现0变为负数，仍然是0的情况

因此如果没有找到重复的元素，那就说明那个重复的元素是 0 



#### [剑指 Offer 04. 二维数组中的查找](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

[思路](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/#)

难度中等739

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

 

**示例:**

现有矩阵 matrix 如下：

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = `5`，返回 `true`。

给定 target = `20`，返回 `false`。

 

**限制：**

```
0 <= n <= 1000
0 <= m <= 1000
```



我的代码

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        //左下角比右上角更好，因为可以直接避免[]空数组的特例化情况
        int m = matrix.length - 1;
        int n = 0;
        while (m >= 0 && n < matrix[0].length) {
            if (matrix[m][n] == target) {
                return true;
            } else if (matrix[m][n] > target) {
                m--;
            } else {
                n++;
            }
        }
        return false;
    }
}
```



解题思路：

[无效的图片地址](C:%5CUsers%5Cl50023467%5CDocuments%5C%E7%AC%94%E8%AE%B0%5Cpic%5Cimage-20220725103330054.png)

可以看出沿着红色的线，是一棵二叉树

例如左下角18为例子

它的上方为10，比它小

它的右边为21，比它大

因此，可以按照二叉树来处理

同时注意边界情况，如果出界了--》说明不在数组中

**TIP: 注意左下角和右上角都可作为开始的点，用左下角是因为可以避免空数组的特例化情况**

比如

左下角开始的循环情况为

```java
while (m >= 0 && n < matrix[0].length) 
```

遇到空数组[] m = matrix.length - 1 即 -1，所以直接不进入循环



右上角开始的循环情况为

```java
while(i < n && j >= 0){
```

int i = 0, j = matrix[0].length - 1, 因此会抛出异常，需要在初始化i j前写一个判断



#### [剑指 Offer 05. 替换空格](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

[思路](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/#)

难度简单319

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

 

**示例 1：**

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

 

**限制：**

```
0 <= s 的长度 <= 10000
```



我的代码

```java
class Solution {
    public String replaceSpace(String s) {
        return (s.replace(" ", "%20"));
    }
    public String replaceSpace(String s) {
        String res = new String();
        for(int i=0;i<s.length();i++) {
            char c=s.charAt(i);
            if(c!=' ')
                res+=c;
            else
                res+="%20";
        }
        return res;
    }
}


```

解题思路：

方法一： 利用api

方法二：for循环一遍，遇到' '就进行替换



#### [剑指 Offer 06. 从尾到头打印链表](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

[思路](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/#)

难度简单320

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

 

**示例 1：**

```
输入：head = [1,3,2]
输出：[2,3,1]
```

 

**限制：**

```
0 <= 链表长度 <= 10000
```



我的代码

```java
public int[] reversePrint(ListNode head) {
    ListNode curr = head;
    int cnt = 0;
    while(curr != null){
        curr = curr.next;
        cnt++;
    }
    curr = head;
    int[] ret = new int[cnt];
    for(int i = cnt-1; i >= 0; i--){
        ret[i] = curr.val;
        curr = curr.next;
    }
    return ret;
}
```



解题思路：

**方法一**：

利用数据结构--stack，第一遍遍历链表，全部入栈

第二遍一个个pop出栈，进入数组

**方法二**：

知道了链表长度就可以定义数组，并且再次遍历链表，从后往前放入元素，如上



#### [剑指 Offer 07. 重建二叉树](https://leetcode.cn/problems/zhong-jian-er-cha-shu-lcof/)

输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

 

**示例 1:**

![img](https://pic.leetcode.cn/1660876520-sqELRc-tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

**示例 2:**

```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

**限制：**

```
0 <= 节点个数 <= 5000
```



我的代码

```java
 public TreeNode buildTree(int[] preorder, int[] inorder) {
     int n = preorder.length - 1;
     return buildNode(preorder, 0, n, inorder, 0, n);
 }
public TreeNode buildNode(int[] preorder, int preL, int preR, int[] inorder, int inL, int inR){
    //null情况
    if(inL > inR || preL > preR) return null;
    TreeNode root = new TreeNode(preorder[preL]);
    //分左右子树
    int idx = inL;
    while(idx <= inR){
        if(inorder[idx] == root.val)
            break;
        idx++;
    }
    int len = idx - inL;
    root.left = buildNode(preorder, preL + 1, preL + len, inorder, inL, idx - 1);
    root.right = buildNode(preorder, preL + len + 1, preR, inorder, idx + 1, inR);

    return root;
}
```



解题思路：

利用递归，进行分治

核心思路：preorder的第一个就是root，根据这个在inorder中找到对应的idx

左边就是它的左子树，右边就是它的右子树

然后继续递归

basecase：当左右子树的左右边界异常，即 left > right时

因此递归就是

root.left = funciton(preorder，preorder的左右指针，inorder，inorder的左右指针)

root.right = 也是一样的



#### [剑指 Offer 09. 用两个栈实现队列](https://leetcode.cn/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)



用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail` 和 `deleteHead` ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead` 操作返回 -1 )

 

**示例 1：**

```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```

**示例 2：**

```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

**提示：**

- `1 <= values <= 10000`
- `最多会对 appendTail、deleteHead 进行 10000 次调用`



我的代码

```java
class CQueue {
    LinkedList<Integer> store;
    LinkedList<Integer> tool; 
    public CQueue() {
        store = new LinkedList<>();
        tool = new LinkedList<>(); 
    }
    
    public void appendTail(int value) {
        store.add(value);
    }
    
    public int deleteHead() {
        if(store.size() == 0 && tool.size() == 0) return -1;
        if(tool.size() == 0){
            while(!store.isEmpty()){
                tool.add(store.pop());
            }
        }
        return tool.pop();
    }
}
```



解题思路：

先往store里面放，如果遇到了需要取出的情况，看看tool中有没有

如果tool中没有，就把store的全部倒进去，pop出栈顶元素

以此类推,如下图

[无效的图片地址](C:%5CUsers%5Cl50023467%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220725114609243.png)

这个时候要删除头节点，即 1

[无效的图片地址](C:%5CUsers%5Cl50023467%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220725114724146.png)

然后pop出去

[无效的图片地址](C:%5CUsers%5Cl50023467%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220725114745317.png)

如果下面还要删除头结点的话，可以直接对tool进行pop

如果要添加尾节点，直接往store中添加

当tool为空时，再把store倒进去



#### [剑指 Offer 10- I. 斐波那契数列](https://leetcode.cn/problems/fei-bo-na-qi-shu-lie-lcof/)

写一个函数，输入 `n` ，求斐波那契（Fibonacci）数列的第 `n` 项（即 `F(N)`）。斐波那契数列的定义如下：

```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```

斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

 

**示例 1：**

```
输入：n = 2
输出：1
```

**示例 2：**

```
输入：n = 5
输出：5
```

 

**提示：**

- `0 <= n <= 100`



我的代码

```java
public int fib(int n) {
    if(n == 0) return 0;
    int fib1 = 0, fib2 = 1;
    for(int i = 2; i <= n; i++){
        int tmp = fib2;
        fib2 += fib1;
        fib2 %= 1000000007;
        fib1 = tmp;
    }
    return fib2;
}
```



解题思路：

利用memo来完成的，但是实际上只需要用到F(N - 1) + F(N - 2)，因此把memo从长度N简化为两个int整形



#### [剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode.cn/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 `n` 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

**示例 1：**

```
输入：n = 2
输出：2
```

**示例 2：**

```
输入：n = 7
输出：21
```

**示例 3：**

```
输入：n = 0
输出：1
```

**提示：**

- `0 <= n <= 100`



我的代码

```java
class Solution {
    public int numWays(int n) {
        if(n == 0 || n == 1) return 1;
        int[] memo = new int[n];
        memo[0] = 1;//跳上1级台阶 共 1 种跳法
        memo[1] = 2;//跳上2级台阶 共 2 种跳法
        for(int i = 2; i < n ; i++){
            memo[i] = (memo[i-2] + memo[i -1]) % 1000000007;
        }
        return memo[n - 1];
    }
}
```



解题思路：

每次只能跳一格或者两格

那么如果青蛙现在在第n格，它可能的跳法就是memo[n - 1] +  memo[n - 2]

剩下的只需要初始化一下就可以了

```java
memo[0] = 1;//跳上1级台阶 共 1 种跳法
memo[1] = 2;//跳上2级台阶 共 2 种跳法
```



#### [剑指 Offer 11. 旋转数组的最小数字](https://leetcode.cn/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

难度简单664

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。

给你一个可能存在 **重复** 元素值的数组 `numbers` ，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的**最小元素**。例如，数组 `[3,4,5,1,2]` 为 `[1,2,3,4,5]` 的一次旋转，该数组的最小值为 1。 

注意，数组 `[a[0], a[1], a[2], ..., a[n-1]]` 旋转一次 的结果为数组 `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]` 。

 

**示例 1：**

```
输入：numbers = [3,4,5,1,2]
输出：1
```

**示例 2：**

```
输入：numbers = [2,2,2,0,1]
输出：0
```

 

**提示：**

- `n == numbers.length`
- `1 <= n <= 5000`
- `-5000 <= numbers[i] <= 5000`
- `numbers` 原来是一个升序排序的数组，并进行了 `1` 至 `n` 次旋转



我的代码

```java
public int minArray(int[] numbers) {
    //二分法
    int l = 0, r = numbers.length - 1, mid = (l + r) / 2;
    while(l < r && numbers[l] >= numbers[r]){
        mid = (l + r) / 2;
        if(numbers[mid] > numbers[r]){
            l = mid + 1;
        }else if(numbers[mid] < numbers[r]){
            r = mid;
        }else{
            r--;
        }
    }
    return numbers[l];
}
```



解题思路：

通过二分法可以知道mid是属于哪个部分

[无效的图片地址](C:%5CUsers%5Cl50023467%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220725143607338.png)

如图，如果mid比right 大，那么说明mid是被旋转的那部分--> mid不可能是最小的值 l = mid + 1

[无效的图片地址](C:%5CUsers%5Cl50023467%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220725143836112.png)

如图，如果mid比right小，那么说明mid属于没被旋转的部分--> mid有可能是最小的值 r = mid

如果mid = right，会有两种情况

mid属于没被旋转的部分， 则 mid---right都是一样的值

mid属于被旋转的部分， 则 如果该值不为最小值，right --，如果该值是最小值，则mid--right都是一样的值，right也可以--





#### [剑指 Offer 13. 机器人的运动范围](https://leetcode.cn/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

地上有一个m行n列的方格，从坐标 `[0,0]` 到坐标 `[m-1,n-1]` 。一个机器人从坐标 `[0, 0] `的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

 

**示例 1：**

```
输入：m = 2, n = 3, k = 1
输出：3
```

**示例 2：**

```
输入：m = 3, n = 1, k = 0
输出：1
```

**提示：**

- `1 <= n,m <= 100`
- `0 <= k <= 20`



我的代码

```java
public int movingCount(int m, int n, int k) {
    boolean[][] visited = new boolean[m][n];
    return dfs(0, 0, visited, m, n, k);
}

public int dfs(int i, int j, boolean[][] visited, int m, int n, int k){
    if(i < 0 || j < 0 || i >= m || j >= n) return 0; // 越界
    if(visited[i][j]) return 0; // 已访问
    if(i / 10 + i % 10 + j / 10 + j % 10 > k) return 0; //个数和超过k

    visited[i][j] = true;
    int val = 1;

    return val + dfs(i + 1, j, visited, m, n, k) + dfs(i, j + 1, visited, m, n, k); //向下 & 向右
}
```



解题思路：

其实就是BFS/DFS

每次只需要判断--》是否访问过+下表是否合理即可确定cnt

提升：这里需要找到规律

```apl
当k = 8;
  0  1  2  3  4  5  6 7  8  9 10
0 可 可 可 可 可 可 可 可 可 不 可
1 可 可 可 可 可 可 可 可 不 不 可
2 可 可 可 可 可 可 可 不 不 不 可
3 可 可 可 可 可 可 不 不 不 不 可
4 可 可 可 可 可 不 不 不 不 不 可
5 可 可 可 可 不 不 不 不 不 不 可
6 可 可 可 不 不 不 不 不 不 不 可                      （可为可到达的，不为不可到达的）
7 可 可 不 不 不 不 不 不 不 不 可  
8 可 不 不 不 不 不 不 不 不 不 不  
9 不 不 不 不 不 不 不 不 不 不 不  
10可 可 可 可 可 可 可 可 可 可 不
```

即可发现可到达的点是等腰三角形，因此不存在下图这种情况

[无效的图片地址](C:%5CUsers%5Cl50023467%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220725120038652.png)

黑色：不可到达

红色：可到达

因此只需要向右和向下遍历就可以了



#### [剑指 Offer 14- I. 剪绳子](https://leetcode.cn/problems/jian-sheng-zi-lcof/)

给你一根长度为 `n` 的绳子，请把绳子剪成整数长度的 `m` 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m-1]` 。请问 `k[0]*k[1]*...*k[m-1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

**示例 1：**

```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```

**示例 2:**

```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

**提示：**

- `2 <= n <= 58`



**我的代码**

```java
public int cuttingRope(int n) {
    if(n == 2 || n == 3) return n - 1;
    int sum  = 1;
    while(n > 4){
        sum *= 3;
        n -= 3;
    }

    return sum * n;
}
```



**解题思路**：基础思路是dp，

比如当长度为n时，它可以被分成长度为 k 和 n-k的情况

所以dp[n] = max(dp[n], dp[k] * dp[n - k], k * (n - k))

第三位的情况就是 直接分为长度为 k和n-k两段



从数学的角度来看，这个问题会简单很多

数论

1. 任何大于1的数都可由2和3相加组成（**奇偶证明**）
2. 因为2* 2=1* 4，2* 3>1* 5, 所以将数字拆成2和3，能得到的积最大



#### [剑指 Offer 14- II. 剪绳子 II](https://leetcode.cn/problems/jian-sheng-zi-ii-lcof/)

给你一根长度为 `n` 的绳子，请把绳子剪成整数长度的 `m` 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m - 1]` 。请问 `k[0]*k[1]*...*k[m - 1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

 

**示例 1：**

```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```

**示例 2:**

```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

 

**提示：**

- `2 <= n <= 1000`

我的代码

```java
public int cuttingRope(int n) {
    if(n == 2 || n == 3) return n - 1;
    long sum  = 1;
    while(n > 4){
        sum = sum * 3 % 1000000007;
        n -= 3;
    }

    return (int)(sum * n % 1000000007);
}
```



解题思路：

相比于上一题，这里的n范围更大了，因此会出现大数问题，所以只需要每次乘积取模 1e9+7（1000000007）即可



#### [剑指 Offer 15. 二进制中1的个数](https://leetcode.cn/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数（也被称为 [汉明重量](http://en.wikipedia.org/wiki/Hamming_weight)).）。

 

**提示：**

- 请注意，在某些语言（如 Java）中，没有无符号整数类型。在这种情况下，输入和输出都将被指定为有符号整数类型，并且不应影响您的实现，因为无论整数是有符号的还是无符号的，其内部的二进制表示形式都是相同的。
- 在 Java 中，编译器使用 [二进制补码](https://baike.baidu.com/item/二进制补码/5295284) 记法来表示有符号整数。因此，在上面的 **示例 3** 中，输入表示有符号整数 `-3`。

 

**示例 1：**

```
输入：n = 11 (控制台输入 00000000000000000000000000001011)
输出：3
解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。
```

**示例 2：**

```
输入：n = 128 (控制台输入 00000000000000000000000010000000)
输出：1
解释：输入的二进制串 00000000000000000000000010000000 中，共有一位为 '1'。
```

**示例 3：**

```
输入：n = 4294967293 (控制台输入 11111111111111111111111111111101，部分语言中 n = -3）
输出：31
解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。
```

 

**提示：**

- 输入必须是长度为 `32` 的 **二进制串** 。

我的代码

```java
//方法一：java api
public int hammingWeight(int n) {
    return Integer.bitCount(n);
}
//方法二：利用api转成字符串，数'1'的数目
public int hammingWeight(int n) {
    String s = Integer.toBinaryString(n);
    int cnt = 0;
    for(int i = 0; i < s.length(); i++){
        if(s.charAt(i) == '1')
            cnt++;
    }
    return cnt;
}
//方法三：数学方法
public int hammingWeight(int n) {
    int count=0;
    while(n!=0){
        count++;
        n=n&(n-1);
    }
    return count;
}
//方法四：暴力法
 public int hammingWeight(int n) {
     int count=0;
     int flag=1;
     while(flag!=0){
         if((n&flag)!=0){
             count++;
         }
         flag<<=1;
     }
     return count;
 }
```

解题思路：

方法三：**把一个整数减去1，再和原整数做与运算**，即`n & (n - 1)`会把该整数最右边一个1变成0.那么一个整数的二进制有多少个1，就可以进行多少次这样的操作。

方法四：直接用数的方式去进行&运算，遍历32位，得到1的个数，整体思路和方法二一致，只不过方法二需要调用api转换为字符串，这个只需要通过数的方式进行遍历。

注意：**1 左移 32 位后为 0**

#### [剑指 Offer 16. 数值的整数次方](https://leetcode.cn/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

[思路](https://leetcode.cn/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/#)

难度中等324

实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 x 的 n 次幂函数（即，xn）。不得使用库函数，同时不需要考虑大数问题。

 

**示例 1：**

```
输入：x = 2.00000, n = 10
输出：1024.00000
```

**示例 2：**

```
输入：x = 2.10000, n = 3
输出：9.26100
```

**示例 3：**

```
输入：x = 2.00000, n = -2
输出：0.25000
解释：2-2 = 1/22 = 1/4 = 0.25
```

 

**提示：**

- `-100.0 < x < 100.0`
- `-231 <= n <= 231-1`
- `-104 <= xn <= 104`

 我的代码

```java
//best 优雅
public double myPow(double x, int n) {
    if(n == 0) return 1;
    if(n == 1) return x;
    if(n == -1) return 1 / x;
    double half = myPow(x, n / 2);
    double mod = myPow(x, n % 2);
    return half * half * mod;
}
//优化方法
public double myPow(double x, int n) {
    //basecase
    if(n == 0) return 1;
    //-oo的情况,和-n情况区分，因为会有溢出问题
    if(n == Integer.MIN_VALUE){
        return myPow(1 / x, Integer.MAX_VALUE) / x;
    }
    //-n的情况
    if(n < 0) return myPow(1 / x, -n);
    //普通情况   
    if(n % 2 ==0){//偶数
        x = Math.abs(x);
        double sub = myPow(x, n / 2);
        return sub * sub;
    }
    return x * myPow(x, n - 1);//奇数
}
//暴力方法
class Solution {
    public double myPow(double x, int n) {
        if(Math.abs(x) == 1){
            if(x < 0 && n % 2 != 0) return -1;
            return 1;
        }
        if(n == Integer.MIN_VALUE) return (double)0;
        if(n < 0){
            x = 1 / x;
            n = Math.abs(n);
        }
        double ret = 1;
        for(int i = 0; i < n; i++){
            ret *= x;
        }
        return ret;
    }
}
```

解题思路:

best：

把n^ k-->n^(k/2) * n^(k/2) * n^(k%2);

这个时候都不用管溢出的k情况了，正负情况也可以

优化方法：

首先处理好basecase+n^k的k溢出的特殊情况，然后把k为负数的情况统一转化成k为正数的情况

然后对于O（k)的迭代可以在k为偶数时做优化

```java
if(n % 2 ==0){//偶数
    x = Math.abs(x);
    double sub = myPow(x, n / 2);
    return sub * sub;
}
```

暴力解法：

对basecase做处理，以及溢出的情况(面向用例编程xs)

然后累计乘



#### [剑指 Offer 18. 删除链表的节点](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/)



给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

**注意：**此题对比原题有改动

**示例 1:**

```
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```

**示例 2:**

```
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```

 

**说明：**

- 题目保证链表中节点的值互不相同

- 若使用 C 或 C++ 语言，你不需要 `free` 或 `delete` 被删除的节点[剑指 Offer 18. 删除链表的节点](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

  [思路](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/#)

  难度简单244

  给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

  返回删除后的链表的头节点。

  **注意：**此题对比原题有改动

  **示例 1:**

  ```
  输入: head = [4,5,1,9], val = 5
  输出: [4,1,9]
  解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
  ```

  **示例 2:**

  ```
  输入: head = [4,5,1,9], val = 1
  输出: [4,5,9]
  解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
  ```

   

  **说明：**

  - 题目保证链表中节点的值互不相同
  - 若使用 C 或 C++ 语言，你不需要 `free` 或 `delete` 被删除的节点

我的代码

```java
//方法一：递归，代码很好看
public ListNode deleteNode(ListNode head, int val) {
    if(head.val == val) return head.next;
    head.next = deleteNode(head.next, val);
    return head;
}
//方法二：虚拟头结点，不用单独处理head情况
public ListNode deleteNode(ListNode head, int val) {
    //建立虚节点
    ListNode dummy = new ListNode(-1);
    dummy.next = head;
    ListNode curr = dummy, next = head;
    while(next.val != val){
        curr = curr.next;
        next = next.next;
    }
    curr.next = next.next;
    return dummy.next;
}
//方法三:头结点和body节点分开处理
public ListNode deleteNode(ListNode head, int val) {
    if(head.val == val) return head.next;
    ListNode curr = head, next = head.next;
    while(next.val != val){
        curr = curr.next;
        next = next.next;
    }
    curr.next = next.next;
    return head;
}
```



解题思路

这里的核心信息是：在链表中一定存在那么一个val，因此我们一定能在链表中找到，不会出现遍历到null的情况(除了递归)



#### [剑指 Offer 19. 正则表达式匹配](https://leetcode.cn/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)

请实现一个函数用来匹配包含`'. '`和`'*'`的正则表达式。模式中的字符`'.'`表示任意一个字符，而`'*'`表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串`"aaa"`与模式`"a.a"`和`"ab*ac*a"`匹配，但与`"aa.a"`和`"ab*a"`均不匹配。

**示例 1:**

```
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。
```

**示例 2:**

```
输入:
s = "aa"
p = "a*"
输出: true
解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。
```

**示例 3:**

```
输入:
s = "ab"
p = ".*"
输出: true
解释: ".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。
```

**示例 4:**

```
输入:
s = "aab"
p = "c*a*b"
输出: true
解释: 因为 '*' 表示零个或多个，这里 'c' 为 0 个, 'a' 被重复一次。因此可以匹配字符串 "aab"。
```

**示例 5:**

```
输入:
s = "mississippi"
p = "mis*is*p*."
输出: false
```

- `s` 可能为空，且只包含从 `a-z` 的小写字母。
- `p` 可能为空，且只包含从 `a-z` 的小写字母以及字符 `.` 和 `*`，无连续的 `'*'`。

注意：本题与主站 10 题相同：https://leetcode-cn.com/problems/regular-expression-matching/

我的代码

```java
public boolean isMatch(String s, String p) {
    int m = s.length(), n = p.length();
    boolean[][] memo = new boolean[m + 1][n + 1];
    for(int i = 0; i <= m; i++){
        for(int j = 0; j <= n; j++){
            if(j == 0){//正则表达式为空
                memo[i][j] = (i == 0);
                continue;
            }
            //正则表达式非空
            if(p.charAt(j - 1)=='*'){
                //0 time
                if(j >= 2)
                    memo[i][j] |= memo[i][j - 2];
                //multiple time
                if(i >= 1 && j >= 2 && Match(s, i - 1, p, j - 2))
                    memo[i][j] |= memo[i-1][j];
            }else{
                if(i >= 1 && j >= 1 && Match(s, i - 1, p, j - 1))
                    memo[i][j] = memo[i - 1][j - 1];
            }
        }
    }
    return memo[m][n];
}

public boolean Match(String s, int idx1, String p, int idx2){
    if(p.charAt(idx2) == '.' || s.charAt(idx1) == p.charAt(idx2)){
        return true;
    }
    return false;
}
```

解题思路：

从后往前看，如果A(长度为n)，B(长度为m)的最后一个字符比对的上，那就抛掉

核心思想：

B的最后一个字符有三种可能--字母/'.'/'*'

- 是字母时，看A[n - 1]和B[m - 1]是否一样，相等则看A[0~n-2], B[0~m-2]
- 是.时，可匹配任意字符，直接看A[0~n-2], B[0~m-2]
- 是*时，B[m - 2] = x 可能重复0~多次
  - 重复0次时， 这就代表B的最后两个字符废了，值看A[0~n-1], B[0~m-3]
  - 重复多次时，且A[n-1]==B[m-2]相等的条件下，A往前挪一个，B继续匹配，所以看A[0~n-2], B[0~m-1]

总结：

情况1和2是一致的，所以可以合并起来

对于*情况，需要看重复几次

basecase：

- 空A 空B     **true**
- 空A 非空B **看情况**--比如A=“” ， B=“a*”
- 非空A 空B **false**
- 非空A 非空B **看情况**

因此可以得出大结构

```
//空B{}

//非空B{

    //*{}

    //非*{}

}
```

   

   

#### [剑指 Offer 20. 表示数值的字符串](https://leetcode.cn/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/)

请实现一个函数用来判断字符串是否表示**数值**（包括整数和小数）。

**数值**（按顺序）可以分成以下几个部分：

1. 若干空格
2. 一个 **小数** 或者 **整数**
3. （可选）一个 `'e'` 或 `'E'` ，后面跟着一个 **整数**
4. 若干空格

**小数**（按顺序）可以分成以下几个部分：

1. （可选）一个符号字符（`'+'` 或 `'-'`）
2. 下述格式之一：
   1. 至少一位数字，后面跟着一个点 `'.'`
   2. 至少一位数字，后面跟着一个点 `'.'` ，后面再跟着至少一位数字
   3. 一个点 `'.'` ，后面跟着至少一位数字

**整数**（按顺序）可以分成以下几个部分：

1. （可选）一个符号字符（`'+'` 或 `'-'`）
2. 至少一位数字

部分**数值**列举如下：

- `["+100", "5e2", "-123", "3.1416", "-1E-16", "0123"]`

部分**非数值**列举如下：

- `["12e", "1a3.14", "1.2.3", "+-5", "12e+5.4"]`

 

**示例 1：**

```
输入：s = "0"
输出：true
```

**示例 2：**

```
输入：s = "e"
输出：false
```

**示例 3：**

```
输入：s = "."
输出：false
```

**示例 4：**

```
输入：s = "    .1  "
输出：true
```

 

**提示：**

- `1 <= s.length <= 20`
- `s` 仅含英文字母（大写和小写），数字（`0-9`），加号 `'+'` ，减号 `'-'` ，空格 `' '` 或者点 `'.'` 。

我的代码

```java
public boolean isNumber(String s) {
    String str = s.trim();
    //分小数和整数处理
    boolean hasE = false, haspoint = false;
    int idx;
    for(idx = 0; idx < str.length(); idx++){
        if(str.charAt(idx) == '.') haspoint = true;
        if(str.charAt(idx) == 'E' || str.charAt(idx) == 'e'){
            hasE = true;
            break;
        }
    }
    //e之前
    if(haspoint){
        if(!isDigit(str.substring(0,idx))) return false;
    }else{
        if(!isZ(str.substring(0,idx))) return false;
    }
    //e之后
    if(hasE){
        return isZ(str.substring(idx + 1));
    }
    return true;
}
public boolean isDigit(String s){
    if(s.length() == 0) return false;
    int idx = 0;
    boolean hasSign = false;
    //排除+/-
    if(s.charAt(0)=='+' || s.charAt(0) == '-'){
        idx++;
        hasSign = true;
    }
    //找到点
    while(idx < s.length()){
        if(s.charAt(idx) == '.') break;
        idx++;
    }

    if(idx == s.length() - 1){//情况1
        return isZ(s.substring(0,idx));
    }else if(idx == 0 || (idx == 1 && hasSign)){//情况2
        return isInteger(s.substring(idx + 1));
    }else{//情况3
        return isZ(s.substring(0,idx)) && isInteger(s.substring(idx+1));
    }

}
public boolean isZ(String s){
    if(s.length() == 0) return false;
    int idx = 0;
    //排除+/-
    if(s.charAt(0)=='+' || s.charAt(0) == '-' ) idx++;
    return isInteger(s.substring(idx));
}
public boolean isInteger(String s){
    if(s.length() == 0) return false;
    int idx = 0;
    while(idx < s.length()){
        char c = s.charAt(idx);
        if(c > '9' || c < '0') return false;
        idx++;
    }
    return true;
}
```

解题思路：

这道题目的难度在于corner case的判断，而不是编码

corner case有如下情况

- 不止一个小数点
- 只有符号 + - e .而没有数字
- 不止一个 +-号

对于整数：

[+/-] + [数字]

对于小数：

1.  [+/-] + [数字] + .
2.  [+/-] + . + [数字]
3.  [+/-] + [数字] + . + [数字]

整体处理：

trim空格之后，根据e/E划分成两个部分

之前的判断是否是**小数/整数**

之后的判断是否是**整数**

#### [剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)



输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数在数组的前半部分，所有偶数在数组的后半部分。

 

**示例：**

```
输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。
```

 

**提示：**

1. `0 <= nums.length <= 50000`
2. `0 <= nums[i] <= 10000`

我的代码

```java
public int[] exchange(int[] nums) {
    //快排
    int l = 0, r = nums.length - 1;
    while(l < r){
        while(l < r && nums[l] % 2 == 1) l++;
        while(l < r && nums[r] % 2 == 0) r--;
        //做swap
        swap(nums, l, r);
    }
    return nums;
}
public void swap(int[] nums, int l, int r){
    int tmp = nums[l];
    nums[l] = nums[r];
    nums[r] = tmp;
}
```

解题思路

其实就是双指针的一次快排



#### [剑指 Offer 22. 链表中倒数第k个节点](https://leetcode.cn/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 `6` 个节点，从头节点开始，它们的值依次是 `1、2、3、4、5、6`。这个链表的倒数第 `3` 个节点是值为 `4` 的节点。

 

**示例：**

```java
给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.
```

我的代码

```java
public ListNode getKthFromEnd(ListNode head, int k) {
    //双指针法
    ListNode curr = head, nextnode = head;
    for(int i = 1; i < k; i++){
        nextnode = nextnode.next;
    }

    while(nextnode.next != null){
        curr = curr.next;
        nextnode = nextnode.next;
    }
    return curr;
}
```

解题思路

[无效的图片地址](C:%5CUsers%5Cl50023467%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220729173755373.png)

如上，双指针，当右边的指针的next为null时，就代表右边的指针到了最后一个node

因此如果想要返回倒数两个节点，就让左指针指向head，右指针向后遍历到(算上头结点)的第二个节点

然后返回左指针即可 

#### [剑指 Offer 24. 反转链表](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/)

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

 

**示例:**

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

 

**限制：**

```
0 <= 节点个数 <= 5000
```

 

**注意**：本题与主站 206 题相同：https://leetcode-cn.com/problems/reverse-linked-list/



我的代码

```java
public ListNode reverseList(ListNode head) {
    if(head == null || head.next == null){
        return head;
    }
    ListNode ret = reverseList(head.next);
    ListNode tmp = head.next;
    tmp.next = head;
    head.next = null;
    return ret;
}
```



解题思路：

1 -> 2 -> 3 -> 4 -> 5

1 -> 2 -> 3

5 -> 4 -> 3

当currnode 为2时， currnode的next是3，

用tmp来标记currnode.next，然后让3指向2,

2指向null

即可

迭代法如下

```java
 public ListNode reverseList(ListNode head) {
     ListNode pre = null, cur = head, next = null;
     while(cur != null) {
         next = cur.next;
         cur.next = pre;
         pre = cur;
         cur = next;
     }
     return pre;
 }
```



#### [剑指 Offer 25. 合并两个排序的链表](https://leetcode.cn/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

**示例1：**

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

**限制：**

```
0 <= 链表长度 <= 1000
```

注意：本题与主站 21 题相同：https://leetcode-cn.com/problems/merge-two-sorted-lists/

我的代码

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(-1); //dummy head
    ListNode curr = dummy;
    while(l1 != null && l2 != null){
        if(l1.val < l2.val){
            curr.next = l1;
            l1 = l1.next;
        }else{
            curr.next = l2;
            l2 = l2.next;
        }
        curr = curr.next;
    }
    if(l1 != null){
        curr.next = l1;
    }
    if(l2 != null){
        curr.next = l2;
    }
    return dummy.next;
}
```

解题思路：

核心思路：dummyHead + 归并排序思路





#### [剑指 Offer 27. 二叉树的镜像](https://leetcode.cn/problems/er-cha-shu-de-jing-xiang-lcof/)

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

```
   4
  /  \
 2   7
 / \  / \
1  3 6  9
```

镜像输出：

```
   4
  /  \
 7   2
 / \  / \
9  6 3  1
```



**示例 1：**

```
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

 

我的代码

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode mirrorTree(TreeNode root) {
        if(root == null) return root;
        //镜像左右子树
        root.left = mirrorTree(root.left);
        root.right = mirrorTree(root.right);
        //交换左右子树
        TreeNode tmp = root.left;
        root.left = root.right;
        root.right = tmp;
        
        return root;
    }
}
```



解题思路：

如代码，镜像就是左右子树也要镜像，然后左右子树交换位置即可

因此，步骤如下

1.左右子树分别镜像

2.交换左右子树位置



#### [剑指 Offer 28. 对称的二叉树](https://leetcode.cn/problems/dui-cheng-de-er-cha-shu-lcof/)

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```



但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

```
    1
   / \
  2   2
   \   \
   3    3
```



**示例 1：**

```
输入：root = [1,2,2,3,4,4,3]
输出：true
```

**示例 2：**

```
输入：root = [1,2,2,null,3,null,3]
输出：false
```

 

**限制：**

```
0 <= 节点个数 <= 1000
```

注意：本题与主站 101 题相同：https://leetcode-cn.com/problems/symmetric-tree/

我的代码

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if(root == null) return true;
        return checkSym(root.left, root.right);
    }
    public boolean checkSym(TreeNode l, TreeNode r){
        if(l == null && r == null) return true;
        if(l == null || r == null) return false;

        if(l.val != r.val) return false;
        return checkSym(l.left, r.right) && checkSym(l.right, r.left);
    }
}
```



解题思路：

对比的时候，会比对左子树和右子树，需要注意，这里对称的定义是l.left == r.right && l.right == r.left

以及对代码精简的建议，上面的代码判断两个TreeNode是否有一个是null的情况

可以使用`if(l == null || r == null)`



#### [剑指 Offer 29. 顺时针打印矩阵](https://leetcode.cn/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

 

**示例 1：**

```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```

**示例 2：**

```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

 

**限制：**

- `0 <= matrix.length <= 100`
- `0 <= matrix[i].length <= 100`

注意：本题与主站 54 题相同：https://leetcode-cn.com/problems/spiral-matrix/

我的代码

```java
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        if(matrix.length == 0) return new int[0];
        int[] ret = new int[matrix.length * matrix[0].length];
        int idx = 0;
        int upperbound = 0, lowerbound = matrix.length - 1, leftbound = 0, rightbound = matrix[0].length - 1;
        while(idx < ret.length){
            //上面 →
            for(int i = leftbound; i <= rightbound && idx < ret.length; i++){
                ret[idx++] = matrix[upperbound][i];
            }
            upperbound++;

            //右边 ↓
            for(int i = upperbound; i <= lowerbound && idx < ret.length; i++){
                ret[idx++] = matrix[i][rightbound];
            }
            rightbound--;

            //下面 ←
            for(int i = rightbound; i >= leftbound && idx < ret.length; i--){
                ret[idx++] = matrix[lowerbound][i];
            }
            lowerbound--;

            //左边 ↑
            for(int i = lowerbound; i >= upperbound && idx < ret.length; i--){
                ret[idx++] = matrix[i][leftbound];
            }
            leftbound++;
            
        }
        return ret;
    }
}
```

解题思路

利用四个boundary来不断压缩

需要注意的是，对于n*n的矩阵，不会出现idx超界的情况

对于 m*n的情况，必须要每次上下左右都对boundary是否有效做判断，或者在for循环中直接加入`idx < ret.length`的比较，达到不会超界的效果



#### [剑指 Offer 30. 包含min函数的栈](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/)

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

 

**示例:**

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

 

**提示：**

1. 各函数的调用总次数不超过 20000 次

 我的代码

```java
class MinStack {
    Stack<Integer> stack;
    Stack<Integer> minsta;
    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack<Integer>();
        minsta = new Stack<Integer>();
    }
    
    public void push(int x) {
        stack.push(x);
        int cnt = 0;
        int min = x;
        if(minsta.isEmpty()){
            minsta.push(x);
            return;
        }
        minsta.push(Math.min(x, minsta.peek()));
    }
    
    public void pop() {
        stack.pop();
        minsta.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int min() {
        return minsta.peek();
    }
}
```

解题思路：

<img src="C:\Users\l50023467\Documents\笔记\pic\155.jpeg" style="zoom:50%;" />

使用两个stack

左右同高，一个是普通stack，另一个是minstack用于记录当前高度的min值

如上图

因此每次push的时候，普通stack直接入栈，minstack需要判断以下两种情况

a minstack为空--直接入栈

b minstack不为空--对比当前值和minstack.peek()，更小的那个为当前高度的min值，入栈

**优化**

```java
class MinStack {
    Stack<Integer> stack;
    Stack<Integer> minsta;
    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack<Integer>();
        minsta = new Stack<Integer>();
    }
    
    public void push(int x) {
        stack.push(x);
        int min = x;
        if(minsta.isEmpty() || minsta.peek() >= x){
            minsta.push(x);
        }
    }
    
    public void pop() {
        int val = stack.pop();
        if(minsta.peek().equals(val))
            minsta.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int min() {
        return minsta.peek();
    }
}
```

这里就是不让minstack和stack等高，只有当当前值<=minstack.peek()才会入栈

pop的时候可以比对一下minstack.peek和stack的pop值是否一致，一致就pop

注意：这里用的是`<=minstack.peek()`而不是`<`，这是因为以防stack会入栈一样的值比如1,2,1，这样pop的时候让minstack为空了抛出异常，因此需要等号



#### [剑指 Offer 31. 栈的压入、弹出序列](https://leetcode.cn/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/)

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。

 

**示例 1：**

```
输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
输出：true
解释：我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

**示例 2：**

```
输入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
输出：false
解释：1 不能在 2 之前弹出。
```

 

**提示：**

1. `0 <= pushed.length == popped.length <= 1000`
2. `0 <= pushed[i], popped[i] < 1000`
3. `pushed` 是 `popped` 的排列。

注意：本题与主站 946 题相同：https://leetcode-cn.com/problems/validate-stack-sequences/

我的代码

```java
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        if(pushed.length == 0) return true;
        Stack<Integer> sta = new Stack<>();
        int in = 0, out = 0;
        //模拟栈
        for(;in < pushed.length; in++){
            sta.push(pushed[in]);
            //比对元素是否一致
            while(!sta.isEmpty() && out < popped.length && sta.peek() == popped[out]){
                sta.pop();
                out++;
            }
        }
        
        return out == popped.length;
    }
}
```

解题思路：

模拟一下就知道了

把压栈的元素按顺序压入

**当栈顶元素和出栈的第一个元素相同，则将该元素弹出**

出栈列表指针后移并继续判断

最后判断出栈列表指针是否指向出栈列表的末尾即可





#### [剑指 Offer 32 - I. 从上到下打印二叉树](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

 

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回：

```
[3,9,20,15,7]
```

 

**提示：**

```
节点总数 <= 1000
```

我的代码

```java
class Solution {
    public int[] levelOrder(TreeNode root) {
        //层序遍历
        List<Integer> list = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while(!queue.isEmpty()){
            TreeNode curr = queue.poll();
            if(curr==null) continue;
            list.add(curr.val);
            //把子节点加入队列中
            queue.add(curr.left);
            queue.add(curr.right);
        }
        return list.stream().mapToInt(Integer::intValue).toArray();
    }
}
```

解题思路：

考点就是层序遍历二叉树



#### [剑指 Offer 32 - II. 从上到下打印二叉树 II](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

 

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
```

 

**提示：**

1. `节点总数 <= 1000`

我的代码

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while(!queue.isEmpty()){
            List<Integer> list = new ArrayList<>();
            int size = queue.size();
            for(int i=0;i<size;i++){
                TreeNode curr = queue.poll();
                if(curr==null) continue;
                list.add(curr.val);
                //把邻接点加入
                queue.add(curr.left);
                queue.add(curr.right);
            }
            if(list.size()>0)
                res.add(list);
        } 
        return res;
    }
}
```

解题思路

分层之后可以通过在while中添加for循环达到目的



#### [剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从**左到右**的顺序打印，第二层按照**从右到左**的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

 

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [20,9],
  [15,7]
]
```

 

**提示：**

1. `节点总数 <= 1000`

我的代码

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        //记录layer
        int layer = 1;
        queue.add(root);
        while(!queue.isEmpty()){
            Stack<TreeNode> sta = new Stack<>();
            List<Integer> list = new ArrayList<>();
            int size = queue.size();
            boolean iseven = (layer%2==0)?true:false;
            for(int i=0;i<size;i++){
                TreeNode curr = queue.poll();
                if(curr==null) continue;
                //处理层数对应的入队方法
                if(iseven) sta.add(curr);
                else list.add(curr.val);
                //邻接点入队
                queue.add(curr.left);
                queue.add(curr.right);
            }
            while(!sta.isEmpty()){
                list.add(sta.pop().val);
            }
            if(list.size()>0)
                res.add(list);
            layer++;
        }
        return res;
    }
}
```

解题思路

记录层数

对奇数层 ：左到右，使用一个list

对偶数层 ：右到左，使用一个stack

然后跳出层数后统一打印即可



#### [剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode.cn/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

 

参考以下这颗二叉搜索树：

```
     5
    / \
   2   6
  / \
 1   3
```

**示例 1：**

```
输入: [1,6,3,2,5]
输出: false
```

**示例 2：**

```
输入: [1,3,2,6,5]
输出: true
```

 

**提示：**

1. `数组长度 <= 1000`



我的代码

```java
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        return checkPostorder(postorder, 0, postorder.length - 1);
    }
    public boolean checkPostorder(int[] tree, int s, int e){
        if(s >= e) return true; 
        int mid = tree[e];
        int idx = e - 1;
        while(idx >= s && tree[idx] > mid){//右子树
            idx--;
        }
        int boundary = idx;//记录左右子树的分界处
        while(idx >= s && tree[idx] < mid){//左子树
            idx--;
        }
        if(idx < s){
            //该层的左右子树正常
            return checkPostorder(tree, s, boundary) && checkPostorder(tree, boundary + 1, e - 1);
        }
        return false;
    }
}
```

解题思路

方法一：递归

```
[1,3,2,6,5]
```

这是一binary search tree的后序遍历，顺序是left->right->root

因此可以发现 从后往前，5是root，然后[6]比5大，因此是右子树，剩下的[1,3,2]比5小因此是左子树

然后按道理来说应该分完了，如果这个时候还有漏掉的数字，那么就说明它违背了后序遍历的原则

接着对[6]和[1,3,2]递归check即可

方法二：单调栈

```java
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        // 单调栈使用，单调递增的单调栈
        Deque<Integer> stack = new LinkedList<>();
        int pervElem = Integer.MAX_VALUE;
        // 逆向遍历，就是翻转的先序遍历
        for (int i = postorder.length - 1;i>=0;i--){
            // 左子树元素必须要小于递增栈被peek访问的元素，否则就不是二叉搜索树
            if (postorder[i] > pervElem){
                return false;
            }
            while (!stack.isEmpty() && postorder[i] < stack.peek()){
                // 数组元素小于单调栈的元素了，表示往左子树走了，记录下上个根节点
                // 找到这个左子树对应的根节点，之前右子树全部弹出，不再记录，因为不可能在往根节点的右子树走了
                pervElem = stack.pop();
            }
            // 这个新元素入栈
            stack.push(postorder[i]);
        }
        return true;
    }
}
```

可以再研究一下



我的代码

```java
class Solution {
    boolean isSub = false;
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        if(B == null) return false;
        checkStructure(A, B);
        return isSub;
    }
    public void checkStructure(TreeNode A, TreeNode B){
        if(isSub) return; //已经找到了
        if(A == null) return; //A树到底了
        if(A.val == B.val){
            isSub = compare(A, B);
        }
        checkStructure(A.left, B);
        checkStructure(A.right, B);
    }
    public boolean compare(TreeNode A, TreeNode B){
        if(B == null) return true;
        if(A == null) return false; //没比完就到底了
        if(A.val != B.val) return false;
        
        return compare(A.left, B.left) && compare(A.right, B.right);
    }
}
```

解题思路：

先找到B在A中对应的点，然后开始对比是不是对的

这里用到了一个全局变量isSub，实际上可以不用的，如下即可

```java
class Solution {
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        if(B == null) return false;
        return checkStructure(A, B);
    }
    public boolean checkStructure(TreeNode A, TreeNode B){
        if(A == null) return false; //A树到底了
        if(A.val == B.val && compare(A, B)){
            return true;
        }
        return checkStructure(A.left, B) || checkStructure(A.right, B);
    }
    public boolean compare(TreeNode A, TreeNode B){
        if(B == null) return true;
        if(A == null) return false; //没比完就到底了
        if(A.val != B.val) return false;
        
        return compare(A.left, B.left) && compare(A.right, B.right);
    }
}
```

再简化一下就是如下

```java
class Solution {
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        if(A == null || B == null) return false;
        return compare(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
    }
    public boolean compare(TreeNode A, TreeNode B){
        if(B == null) return true;
        if(A == null) return false; //没比完就到底了        
        return A.val == B.val && compare(A.left, B.left) && compare(A.right, B.right);
    }
}
```

但是我认为没必要给每个AB都进行compare，只需要找A.val == B.val的那个情况进行对比就可以了

而且现在的这个可读性不高，不如原来的



#### [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode.cn/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

给你二叉树的根节点 `root` 和一个整数目标和 `targetSum` ，找出所有 **从根节点到叶子节点** 路径总和等于给定目标和的路径。

**叶子节点** 是指没有子节点的节点。

 

**示例 1：**

![img](https://pic.leetcode.cn/1660876832-Jrbqig-pathsumii1.jpg)

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
```

**示例 2：**

![img](https://pic.leetcode.cn/1660876832-EmXsrh-pathsum2.jpg)

```
输入：root = [1,2,3], targetSum = 5
输出：[]
```

**示例 3：**

```
输入：root = [1,2], targetSum = 0
输出：[]
```

 

**提示：**

- 树中节点总数在范围 `[0, 5000]` 内
- `-1000 <= Node.val <= 1000`
- `-1000 <= targetSum <= 1000`

注意：本题与主站 113 题相同：https://leetcode-cn.com/problems/path-sum-ii/

我的代码

```java
class Solution {
    List<List<Integer>> ret = new ArrayList<>();
    LinkedList<Integer> list = new LinkedList<>();
    int target;
    int curr = 0;
    public List<List<Integer>> pathSum(TreeNode root, int target) {
        this.target = target;
        //先序遍历traverse
        preorder(root);
        return ret;
    }
    public void preorder(TreeNode root){
        if(root == null) return;

        //add
        curr += root.val;
        list.add(root.val);
        if(curr == target){
            //需要判断是否到达叶子节点
            if(root.left == null && root.right == null){
                ret.add(new LinkedList(list));
            }
        }

        preorder(root.left);
        preorder(root.right);

        //remove
        curr -= root.val;
        list.removeLast();
    }
}
```



解题思路：

需要注意：这里的条件是root--》leaf的路径，也就是说最后一个被添加的节点必须是叶子节点

以及node的值可以是负数，因此必须要全部遍历，没法剪枝

核心思想：**遍历--》先序遍历**

curr == target同时需要判断是否是叶子节点了

满足条件才能添加



#### [剑指 Offer 35. 复杂链表的复制](https://leetcode.cn/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

请实现 `copyRandomList` 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 `next` 指针指向下一个节点，还有一个 `random` 指针指向链表中的任意节点或者 `null`。

 

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e1.png)

```
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

**示例 2：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e2.png)

```
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
```

**示例 3：**

**![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e3.png)**

```
输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]
```

**示例 4：**

```
输入：head = []
输出：[]
解释：给定的链表为空（空指针），因此返回 null。
```

 我的代码

```java
public Node copyRandomList(Node head) {
    Map<Node, Node> map = new HashMap<>(); //record <old node, new node>
    Node ptr = head;
    // 1st traverse--copy node
    while(ptr != null){
        //copy node
        map.put(ptr,new Node(ptr.val));
        ptr = ptr.next;
    }
    //2cd traverse--link node
    ptr = head;
    while(ptr != null){
        map.get(ptr).next = map.get(ptr.next);
        map.get(ptr).random = map.get(ptr.random);
        ptr = ptr.next;
    }
    return map.get(head);
}
```

解题思路

利用hashmap，遍历两次，时间复杂度O(N), 空间复杂度O(N)

方法二：不采用额外的数据结构

时间复杂度O(N), 空间复杂度O(1)

```java
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null) return null;
        Node curr = head;
        //1->2->3   1->1'->2->2'->3->3'
        while(curr != null){
            Node n = new Node(curr.val);
            n.next = curr.next;
            curr.next = n;
            curr = curr.next.next;
        }
        curr = head;
        //deal with random
        while(curr != null){
            if(curr.random != null){
                curr.next.random = curr.random.next;
            }
            curr = curr.next.next;
        }
        //split
        Node newhead = head.next;
        Node ptrn = newhead, ptro = head;//ptro-->pointer to old; ptrn-->pointer to new
        while(ptro != null){
            ptro.next = ptrn.next;
            ptro = ptro.next;
            if(ptro == null) break;
            ptrn.next = ptro.next;
            ptrn = ptrn.next;
        }
        return newhead;
    }
}
```

原地修改，首先把1->2->3 变成  1->1'->2->2'->3->3'，即复制的node紧接在原node后

然后处理复制的node的random

最后由于系统会检查是否修改了原来的链表，需要把1->1'->2->2'->3->3'还原成两个链表

1->2->3和1'->2'->3'



#### [剑指 Offer 36. 二叉搜索树与双向链表](https://leetcode.cn/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。

 

为了让您更好地理解问题，以下面的二叉搜索树为例：

 

![img](https://pic.leetcode.cn/1660876832-DeEvRu-bstdlloriginalbst.png)

 

我们希望将这个二叉搜索树转化为双向循环链表。链表中的每个节点都有一个前驱和后继指针。对于双向循环链表，第一个节点的前驱是最后一个节点，最后一个节点的后继是第一个节点。

下图展示了上面的二叉搜索树转化成的链表。“head” 表示指向链表中有最小元素的节点。

 

![img](https://pic.leetcode.cn/1660876832-BnEDqR-bstdllreturndll.png)

 

特别地，我们希望可以就地完成转换操作。当转化完成以后，树中节点的左指针需要指向前驱，树中节点的右指针需要指向后继。还需要返回链表中的第一个节点的指针。

 

**注意：**本题与主站 426 题相同：https://leetcode-cn.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/

我的代码

```java
class Solution {
    Node pre, head;
    public Node treeToDoublyList(Node root) {
        if(root == null) return root;
        inorder(root);
        head.left = pre;
        pre.right = head;
        return head;
    }
    public void inorder(Node curr){
        if(curr == null) return;
        inorder(curr.left);
        //做操作
        if(pre == null){
            head = curr;
        }else{
            pre.right = curr;
        }
        curr.left = pre;
        pre = curr;
        inorder(curr.right);
    }
}
```

解题思路

中序遍历就是想要的结果

只要我们找到head，以及每次找到prev就能做到连接起来

中序遍历的地方定义 curr和prev连接起来就可以了

当第一次遇到pre==null时说明找到了最左的节点，此时定义head



#### [剑指 Offer 37. 序列化二叉树](https://leetcode.cn/problems/xu-lie-hua-er-cha-shu-lcof/)

请实现两个函数，分别用来序列化和反序列化二叉树。

你需要设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

**提示：**输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 [LeetCode 序列化二叉树的格式](https://support.leetcode-cn.com/hc/kb/article/1567641/)。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。

 

**示例：**

![img](https://pic.leetcode.cn/1660876832-UFIzPa-serdeser.jpg)

```
输入：root = [1,2,3,null,null,4,5]
输出：[1,2,3,null,null,4,5]
```

 

注意：本题与主站 297 题相同：https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/

我的代码

```java
// Encodes a tree to a single string.
public String serialize(TreeNode root) {
    StringBuffer sb = new StringBuffer();
    //层序遍历得到
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    while(!queue.isEmpty()){
        TreeNode curr = queue.poll();

        if(curr != root) sb.append(",");
        if(curr == null){
            sb.append("#");
            continue;
        }
        else sb.append(String.valueOf(curr.val));
        //左右子树
        queue.add(curr.left);
        queue.add(curr.right);
    }
    return sb.toString();
}

// Decodes your encoded data to tree.
public TreeNode deserialize(String data) {
    Queue<TreeNode> queue = new LinkedList<>();
    String[] nodes = data.split(",");

    //处理头结点
    int idx = 0;
    TreeNode root = buildNode(idx, nodes);
    idx++;
    if(root == null) return null;

    queue.add(root);

    while(!queue.isEmpty()){
        TreeNode curr = queue.poll();
        if(curr == null) continue;
        //构建左右子树
        TreeNode left,right;
        left = buildNode(idx, nodes);
        idx++;
        right = buildNode(idx, nodes);
        idx++;
        //连接curr和左右子树
        curr.left = left;
        curr.right = right;
        queue.add(left);
        queue.add(right);
    }
    return root;
}
public TreeNode buildNode(int idx, String[] nodes){
    if(nodes.length == 0 || idx >= nodes.length) return null;
    if(nodes[idx].equals("#")) return null;
    else return new TreeNode(Integer.valueOf(nodes[idx]));

}
```

解题思路：

层序遍历，遇到null就用“#”代替，然后deserialize的时候还是层序遍历反过来就可以了

注意处理字符串的时候，可能会出现下标越界的情况，这种情况按照null来返回就可以了




#### [剑指 Offer 38. 字符串的排列](https://leetcode.cn/problems/zi-fu-chuan-de-pai-lie-lcof/)

输入一个字符串，打印出该字符串中字符的所有排列。

 

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

 

**示例:**

```
输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
```

 

**限制：**

```
1 <= s 的长度 <= 8
```

我的代码

```java
class Solution {
    Set<String> set = new HashSet<>();
    int len;
    public String[] permutation(String s) {
        char[] str = s.toCharArray();
        boolean[] used = new boolean[s.length()];
        backtrace(str, used, "");
        return set.toArray(new String[0]);
    }
    public void backtrace(char[] str, boolean[] used, String s){
        //basecase
        if(s.length() == str.length){
            set.add(s);
            return;
        }

        for(int i = 0; i < str.length; i++){
            if(i > 0 && str[i] == str[i-1] && ！used[i - 1]) continue;
            if(used[i]) continue;
            used[i] = true;
            backtrace(str, used, s + String.valueOf(str[i]));
            used[i] = false;
        }
    }
}
```

解题思路

就是有重元素的全排列，这里注意要剪枝！

```
if(i > 0 && str[i] == str[i-1] && ！used[i - 1]) continue;
```



#### [剑指 Offer 39. 数组中出现次数超过一半的数字](https://leetcode.cn/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

 

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

 

**示例 1:**

```
输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
```

 

**限制：**

```
1 <= 数组长度 <= 50000
```



我的代码

```java
class Solution {
    public int majorityElement(int[] nums) {
        if(nums.length==1) 
            return nums[0];
        int res=nums[0];
        int cnt=1;/*我方个数*/
        for(int i=1;i<nums.length;i++) {
            cnt = (res!=nums[i])? cnt-1:cnt+1;/*遇到友军cnt++,遇到敌军cnt--*/
            if(cnt==0) {/*打乱洗牌，重新站队*/
                res=nums[i];
                cnt++;
            }
        }
        return res;
    }
}
```

解题思路：摩尔投票法：遇见不同的就同归于尽

最优解：摩尔投票法
也可以理解成混战极限一换一，不同的两者一旦遇见就同归于尽，最后活下来的值都是相同的，即要求的结果
时间**O(n)，空间O(1)**

其他解法：

方法二： 排序后取中值 时间O(nlogn)，空间O(1)

方法三：使用哈希表 时间O(n)，空间O(n/2)

#### [剑指 Offer 40. 最小的k个数](https://leetcode.cn/problems/zui-xiao-de-kge-shu-lcof/)

难度简单481收藏分享切换为英文接收动态反馈

输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

 

**示例 1：**

```
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```

**示例 2：**

```
输入：arr = [0,1,2,1], k = 1
输出：[0]
```

 

**限制：**

- `0 <= k <= arr.length <= 10000`
- `0 <= arr[i] <= 10000`

我的代码

```java
//最优解： 快速排序
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        if(arr.length == 0 || k == 0) return new int[0];
        return quicksort(arr, 0, arr.length - 1, k - 1);
    }
    public int[] quicksort(int[] arr, int l, int r, int k){
        int idx = partition(arr, l, r);
        if(idx == k) return Arrays.copyOf(arr, idx + 1);
        return (idx < k)? quicksort(arr, idx + 1, r, k) : quicksort(arr, l, idx - 1, k);
    }
    public int partition(int[] arr, int l, int r){
        int pivot = arr[l];
        int i = l, j = r + 1;
        while(true){
            while(++i < r && arr[i] < pivot);
            while(--j > l && arr[j] > pivot);
            if(i >= j) break;
            swap(arr, i, j);
        }
        swap(arr, l, j);
        return j;
    }
    public void swap(int[] arr, int i, int j){
        int tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }
}
//最大堆
public int[] getLeastNumbers(int[] arr, int k) {
    if(k == 0) return new int[0];
    //keep a 最大堆with size n
    int[] ret = new int[k];
    PriorityQueue<Integer> pq = new PriorityQueue<>((a, b)->{return b - a;});
    for(int i = 0; i < arr.length; i++){
        if(pq.size() < k){
            pq.offer(arr[i]);
        }else if(pq.peek() > arr[i]){
            pq.poll();
            pq.offer(arr[i]);
        }
    }
    //traverse
    for(int i = 0; i < k; i++){
        ret[i] = pq.poll();
    }
    return ret;
}
```

解题思路：

最优解：快排

并不需要完全排序，只需要排0~k - 1的这一段就可以了

逻辑就是partition之后得到下标，如果==k - 1那么就可以返回0~k -1这一段

如果 idx < k - 1那么还需要在 idx + 1到右边这一片继续partition

如果 idx > k - 1 那么直接在 l 到 idx - 1这一片partition

#### [剑指 Offer 41. 数据流中的中位数](https://leetcode.cn/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

- void addNum(int num) - 从数据流中添加一个整数到数据结构中。
- double findMedian() - 返回目前所有元素的中位数。

**示例 1：**

```
输入：
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]
[[],[1],[2],[],[3],[]]
输出：[null,null,null,1.50000,null,2.00000]
```

**示例 2：**

```
输入：
["MedianFinder","addNum","findMedian","addNum","findMedian"]
[[],[2],[],[3],[]]
输出：[null,null,2.00000,null,2.50000]
```

 

**限制：**

- 最多会对 `addNum、findMedian` 进行 `50000` 次调用。

注意：本题与主站 295 题相同：https://leetcode-cn.com/problems/find-median-from-data-stream/

我的代码

```java
class MedianFinder {
    PriorityQueue<Integer> small;
    PriorityQueue<Integer> big;
    /** initialize your data structure here. */
    public MedianFinder() {
        //大顶堆
        small = new PriorityQueue<>((a,b)->(b - a));
        //小顶堆
        big = new PriorityQueue<>();
    }
    
    public void addNum(int num) {
        if(small.size() >= big.size()){
            small.offer(num);
            big.offer(small.poll());
        }else{
            big.offer(num);
            small.offer(big.poll());
        }
    }
    
    public double findMedian() {
        //如果奇数--大小不一致，在大的那个里面
        if(small.size() > big.size()){
            return small.peek();
        }else if(small.size() < big.size()){
            return big.peek();
        }else{
            //如果偶数--大小一致
            return (small.peek() + big.peek()) / 2.0;
        }
    }
}
```

解题思路：

如果只是单次需要得到中位数，不如直接排序然后取中间的值，时间复杂度也是差不多的

但是如果是多次，利用两个堆可以把时间复杂度变成插入一个堆的复杂度--O(logN).

我们需要保证

<img src="https://labuladong.github.io/algo/images/%E4%B8%AD%E4%BD%8D%E6%95%B0/2.jpeg" alt="img" style="zoom:50%;" />

左边为小顶堆，右边为大顶堆

左边的最小值 》右边的最大值

因此我们取值的时候，如果左右两个堆大小一致--偶数情况，则两者的peek()的平均值

否则更大的那个堆的peek()是中位数

因此就有

```java
public double findMedian() {
    //如果奇数--大小不一致，在大的那个里面
    if(small.size() > big.size()){
        return small.peek();
    }else if(small.size() < big.size()){
        return big.peek();
    }else{
        //如果偶数--大小一致
        return (small.peek() + big.peek()) / 2.0;
    }
}
```

算法流程：
设元素总数为 `N = m + n`，其中 m 和 n 分别为 A 和 B 中的元素个数。

addNum(num) 函数：

当 `m = n`（即 N 为 偶数）：需向 A 添加一个元素。实现方法：将新元素 num 插入至 B ，再将 B 堆顶元素插入至 A ；
当 `m !=n`（即 N 为 奇数）：需向 B 添加一个元素。实现方法：将新元素 num 插入至 A ，再将 A 堆顶元素插入至 B ；



#### [剑指 Offer 42. 连续子数组的最大和](https://leetcode.cn/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

 

**示例1:**

```
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

 

**提示：**

- `1 <= arr.length <= 10^5`
- `-100 <= arr[i] <= 100`

注意：本题与主站 53 题相同：https://leetcode-cn.com/problems/maximum-subarray/

我的代码

```java
public int maxSubArray(int[] nums) {
    int max = Integer.MIN_VALUE, curr = 0;
    for(int i = 0; i < nums.length; i++){
        if(curr < 0) curr = 0;
        curr += nums[i];
        max = Math.max(curr, max);
    }
    return max;
}
```

解题思路：

只需要知道我们不断往前移动，如果之前的累计是负数，那么就应该清零了，不然加上当前值会让当前值变得更小

因此

```java
if(curr < 0) curr = 0;
```



#### [剑指 Offer 43. 1～n 整数中 1 出现的次数](https://leetcode.cn/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)

难度困难367收藏分享切换为英文接收动态反馈

输入一个整数 `n` ，求1～n这n个整数的十进制表示中1出现的次数。

例如，输入12，1～12这些整数中包含1 的数字有1、10、11和12，1一共出现了5次。

 

**示例 1：**

```
输入：n = 12
输出：5
```

**示例 2：**

```
输入：n = 13
输出：6
```

 

**限制：**

- `1 <= n < 2^31`

注意：本题与主站 233 题相同：https://leetcode-cn.com/problems/number-of-digit-one/

我的代码

```java
class Solution {
    public int countDigitOne(int n) {
        // idx :=记录当前是个位十位百位， standard记录 标准情况下有几个1
        // right :=记录 当前位右边有几个1 rest记录当前位右边的值
        int idx = 1, standard = 0;
        int right = 0, rest = 0;
        while(n > 0){
            int curr = n % 10;
            if(curr > 1){
                right += curr * standard + idx;
            }else if(curr == 1){
                right += curr * standard + rest + 1;
            }
            rest += idx * curr;
            standard = 10 * standard + idx;
            idx *= 10;
            n /= 10;
        }
        return right;
    }
}
```

解题思路：

```ABAP
5 | 1 | 2
```

其中 1 的个数 = 5 * 【0~ 99会有的1的个数】 + 【12中1的个数】+100

这是因为512超过了100，那么一定会经历100~199，这时百位数的1会出现100次

```java
3 | 1 | 5 | 8
```

其中1的个数 = 3 * 【0 ~999会有的1的个数】 + 【158中1的个数】 + 1000

这是因为3158 > 1000, 1000~1999中千位的1出现了1000次

```
1 | 5 | 3
```

其中1的个数 = 1 * 【0 ~99会有的1的个数】 + 【53中1的个数】 + 53

这是因为153 > 100，但是并没有>199，所以并不会让1出现100次，只会出现53次

核心思路：

得到【standard情况下1的个数】+ 【右边1的个数】 + 当前位数/ 右边的值

即对于153的情况，当我们从后往前遍历到1时

【standard】代表右边位数为理想情况，即全9，会有几个1，这里右边只有两位，因此standard代表的是0 ~ 99会有几个1

【右边1的个数】即1的右边是53，指 0 ~ 53会有几个1

【当前位数】 当前位是百位，即100

【右边的值】1的右边是53

因此我们就可以得出来153有几个1了，不断从后往前遍历

```java
public int countDigiOne(int n){
    int standard = 0, idx = 1;
    int right = 0, rest = 0;
    //153
    while(n > 0){
        //get # at this idx
        int curr = n % 10;
        if(curr > 1){
            right += curr * standard + idx;
        }else if(curr == 1){
            right += curr * standard + rest + 1;//加1是因为eg. 12-->rest为2，但是这样就skip了10，因此计数应该从0开始计
        }
        //refresh value
        n /= 10;
        standard = 10 * standard + idx;
        idx *= 10;
    }
}
```

这里需要注意一下standard的变化规则

0~9 1

0~99 = 10 * 1[last] + 10[idx] = 20

0~999 = 10 * 20[last] + 100[100] 

#### [剑指 Offer 44. 数字序列中某一位的数字](https://leetcode.cn/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

 

**示例 1：**

```
输入：n = 3
输出：3
```

**示例 2：**

```
输入：n = 11
输出：0
```

 

**限制：**

- `0 <= n < 2^31`

注意：本题与主站 400 题相同：https://leetcode-cn.com/problems/nth-digit/

我的代码

```java
public int findNthDigit(int n) {
    long l = 0, r = 9;
    long lastMax = -1, currMax = 9;
    int len = 1;
    while(n > currMax){
        l = r + 1;
        r = l * 10 - 1;
        len++;
        lastMax = currMax;
        currMax = lastMax + (r - l + 1) * len;
    }
    lastMax++;
    //find val
    long val = l + (n - lastMax) / len;
    //find idx
    int idx = (int)((n - lastMax) % len);
    String str = String.valueOf(val);
    return str.charAt(idx) - '0';

}
```

解题思路：

```pseudocode
位数  对应数字范围  实际数字范围      占用数字
1位    0 ~ 9       0 ~ 9          10
2位    10 ~ 99     10 ~ 189       180
3位    100 ~ 999   190 ~ 2880     2700
```

所以我们需要 l r记录当前对应数字范围

以及lastMax currMax记录上个范围对应的实际数字范围最大值，和当前范围对应的实际数字范围最大值

```java
//l r的更新
l = r + 1;
r = l * 10 - 1;
//对应lastMax CurrMax的更新
lastMax = currMax;
currMax = lastMax + (r - l + 1) * len;
```

对于任意一个数字，比如2200

我们发现在三位数字的实际数字范围内，在代码上的表现就是，当lastMax = 189时会进入while循环

然后更新为3位数，lr也更新为[100, 999]

然后出来后让lastMax+1为了方便运算

然后就知道实际数字190对应100，那么就让l + (2200 - lastMax) / 3就知道2200对应的是哪个数字

再通过 (2200 - lastMax) % 3 就知道对应该数字的第几位



#### [剑指 Offer 45. 把数组排成最小的数](https://leetcode.cn/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

 

**示例 1:**

```
输入: [10,2]
输出: "102"
```

**示例 2:**

```
输入: [3,30,34,5,9]
输出: "3033459"
```

 

**提示:**

- `0 < nums.length <= 100`

**说明:**

- 输出结果可能非常大，所以你需要返回一个字符串而不是整数
- 拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0

我的代码

```java
public String minNumber(int[] nums) {
    String[] str = new String[nums.length];
    int idx = 0;
    for(int num : nums){
        str[idx++] = String.valueOf(num);
    }
    //核心排序
    Arrays.sort(str, new Comparator<String>(){
        @Override
        public int compare(String str1, String str2) {
            return (str1 + str2).compareTo(str2 + str1);
        }
    });
    StringBuffer sb = new StringBuffer();
    for(String s : str){
        sb.append(s);
    }
    return sb.toString();
}
```

解题思路

把num都转成string后进行排序，我们希望的顺序是拼后的值更小，即3 和 30

330 >  303

因此sort需要使用

```java
@Override
public int compare(String str1, String str2) {
    return (str1 + str2).compareTo(str2 + str1);
}
```



#### [剑指 Offer 46. 把数字翻译成字符串](https://leetcode.cn/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 

**示例 1:**

```
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

 

**提示：**

- `0 <= num < 231`

我的代码

```java
class Solution {
    int cnt = 0;
    public int translateNum(int num) {
        String str = String.valueOf(num);
        char[] strc = str.toCharArray();
        backtrace(strc, 0);
        return cnt;
    }
    public void backtrace(char[] str, int idx){
        if(idx >= str.length){
            cnt++;
            return;
        }
        //一位数
        backtrace(str, idx + 1);
        //两位数
        if( (idx + 1 < str.length ) && (str[idx] == '1' || (str[idx] == '2' && str[idx + 1] <= '5')) ){
            backtrace(str, idx + 2);
        }
    }
}
```

解题思路：

方法一：回溯，有 0~ 25 这几个数字，因此对每位数字的选择时，有两种状态 

a 对应一位数

b 对应两位数

方法二：dp青蛙跳台阶进阶版(两个台阶时需要做判断是否是小于26)

```java
public int translateNum(int num) {
    //dp[i] = dp[i - 1] + dp[i - 2]
    char[] str =  String.valueOf(num).toCharArray();
    int[] dp = new int[str.length + 1];
    //初始化
    if(num < 10) return 1;
    dp[0] = 1;
    dp[1] = 1;
    for(int i = 2; i < dp.length; i++){
        dp[i] += dp[i - 1];
        if(str[i - 2] == '1' || (str[i - 2] == '2' && str[i - 1] < '6')){
            dp[i] += dp[i - 2];
        }
    }
    return dp[str.length];
}
```

核心思路`dp[i] = dp[i - 1] + dp[i - 2]`

即如下

```java
dp[i] += dp[i - 1];
if(str[i - 2] == '1' || (str[i - 2] == '2' && str[i - 1] < '6')){
    dp[i] += dp[i - 2];
}
```

dp[i]代表0~ i-1的可能的翻译方法的合

因此需要dp[]长度为str.length + 1

然后dp[0]和dp[1]都是1种翻译方法， Tip：dp[0]是为了能让长度为2时eg 33--》dp[2]能得1的结果



#### [剑指 Offer 47. 礼物的最大价值](https://leetcode.cn/problems/li-wu-de-zui-da-jie-zhi-lcof/)

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

 

**示例 1:**

```
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```

 

提示：

- `0 < grid.length <= 200`
- `0 < grid[0].length <= 200`

我的代码

```java
public int maxValue(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[][] val = new int[m + 1][n + 1];
    findmaxValue(val, grid, m, n);
    return val[m][n];
}
public int findmaxValue(int[][] val, int[][] grid, int x, int y){
    if(x < 1 || y < 1) return 0;
    if(val[x][y] != 0) return val[x][y];

    int up = findmaxValue(val, grid, x - 1, y);
    int left = findmaxValue(val, grid, x, y - 1);
    val[x][y] = Math.max(left, up) + grid[x - 1][y - 1];
    return val[x][y];
}
===================================================
//非递归
 public int maxValue(int[][] grid) {
    int m=grid.length,n=grid[0].length;
    int[][] dp=new int[m][n];
    dp[0][0]=grid[0][0];
    //初始化边缘
    for(int i=1;i<m;++i)
        dp[i][0]=dp[i-1][0]+grid[i][0];
    for(int i=1;i<n;++i)
        dp[0][i]=dp[0][i-1]+grid[0][i];
    //核心代码
    for(int i=1;i<m;++i)
        for(int j=1;j<n;++j){
            dp[i][j]=Math.max(dp[i-1][j],dp[i][j-1])+grid[i][j];
        }
    return dp[m-1][n-1];
}
===============================
//优化：滚动数组
public int maxValue(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[] dp = new int[n + 1];
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            dp[j] = Math.max(dp[j], dp[j - 1]) + grid[i - 1][j - 1];
        } 
    }

    return dp[n];
}
```

解题思路：

对于位置[m] [n]来说，[0] [0]到达它最大的值是[m-1] [n] 或者[m] [n-1]的较大值加上[m] [n]位置上的值

为了方便处理边缘值如 第一列和第一行，让dp `int[][] val = new int[m + 1][n + 1];`

其实这一题也是可以用非递归的dp做出来

如上

tip：滚动数组核心思路

```java
f(i, j) = max{f(i - 1, j), f(i, j - 1)} + grid[i][j]
```



#### [剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode.cn/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

 

**示例 1:**

```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

 

提示：

- `s.length <= 40000`

注意：本题与主站 3 题相同：https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/

我的代码

```java
public int lengthOfLongestSubstring(String s) {
    //滑动窗口--记录该元素第一次出现的下标
    Set<Character> set = new HashSet<>();

    int max = 0;
    for(int l = 0, r = 0; r < s.length(); r++){
        char c = s.charAt(r);
        //移动窗口左边界
        while(set.contains(c)){
            set.remove(s.charAt(l++));
        }
        set.add(c);
        max = Math.max(max, r - l + 1);
    }
    return max;
}
```

解题思路：

维护一个滑动窗口，由于可能出现的不止是小写字母，使用set来记录

右边界不断往前移动

等到遇到一样的值之后，左边界开始收缩



#### [剑指 Offer 49. 丑数](https://leetcode.cn/problems/chou-shu-lcof/)

我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

 

**示例:**

```
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
```

**说明:** 

1. `1` 是丑数。
2. `n` **不超过**1690。

注意：本题与主站 264 题相同：https://leetcode-cn.com/problems/ugly-number-ii/

我的代码

```java
 public int nthUglyNumber(int n) {
     //初始化丑数链表
     int[] ugly = new int[n];
     int p = 0;//丑数链表指针

     int p2 = 1, p3 = 1, p5 = 1;
     int i2 = 0, i3 = 0, i5 = 0;
     while(p < n){
         int min = getMin(p2, p3, p5);
         ugly[p++] = min;
         if(min == p2){
             p2 = 2 * ugly[i2++];
         }
         if(min == p3){
             p3 = 3 * ugly[i3++];
         }
         if(min == p5){
             p5 = 5 * ugly[i5++];
         } 
     }
     return ugly[n - 1];

 }
public int getMin(int a, int b, int c){
    int min = Math.min(a, b);
    min = Math.min(min, c);
    return min;
}
```

解题思路

核心思路：

如果 x 是丑数，那么 x * 2/3/5也是丑数

因此我们可以这么思考

```java
//x链表
1->2->3->4->5->6->8->9
//2链表
1 * 2->2 * 2->3 * 2->4 * 2->5 * 2->6 * 2->8 * 2->9 * 2
//3链表
1 * 3->2 * 3->3 * 3->4 * 3->5 * 3->6 * 3->8 * 3->9 * 3    
//5链表
1 * 5->2 * 5->3 * 5->4 * 5->5 * 5->6 * 5->8 * 5->9 * 5     
```

因此我们只是在合并三个链表而已

tip：这三个链表有重复的元素，因此判断的时候不能用if else，而是要用单独的if，这样能够避免最后合成的链表没有重复的元素

使用三个整形代表三个链表对应的当前节点(为了统一，让三个链表的头结点都为1)

同时还需要三个指针分别对应已合成的丑数链表的idx，这个也很好理解，我们希望不论是哪个链表，都是从最小的丑数往大的遍历，因此三个下标都在ugly[]上



#### [剑指 Offer 50. 第一个只出现一次的字符](https://leetcode.cn/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

**示例 1:**

```
输入：s = "abaccdeff"
输出：'b'
```

**示例 2:**

```
输入：s = "" 
输出：' '
```

 

**限制：**

```
0 <= s 的长度 <= 50000
```

我的代码

```java
public char firstUniqChar(String s) {
    char[] str = s.toCharArray();
    int[] alpha = new int[26];
    for(char c : str){
        alpha[c - 'a']++;
    }
    for(char c : str){
        if(alpha[c - 'a'] == 1) return c;
    }
    return ' ';
}
```

解题思路：

两次遍历：

第一次--记录每个字母出现次数

第二次--遍历看只出现过一次的字母--遇到的第一个就返回

如果没有返回的，就代表没有只出现过一次的字母，直接返回空字符' '

#### [剑指 Offer 51. 数组中的逆序对](https://leetcode.cn/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

难度困难840收藏分享切换为英文接收动态反馈

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

 

**示例 1:**

```
输入: [7,5,6,4]
输出: 5
```

 

**限制：**

```
0 <= 数组长度 <= 50000
```

我的代码

```java
class Solution {
    public int reversePairs(int[] nums) {
        return mergeSort(nums, 0, nums.length - 1);
    }
    public int mergeSort(int[] nums, int l, int r){
        if(l >= r) return 0;
        int mid = (l + r) / 2;
        int cnt = mergeSort(nums, l, mid) + mergeSort(nums, mid + 1, r);
        int left = l, right = mid + 1; // as the start idx of right part
        int idx = 0;
        int[] tmp = new int[r - l + 1]; // to put sorted numbers
        while(left <= mid && right <= r){
            if(nums[left] <= nums[right]){
                tmp[idx++] = nums[left++];
            }else{
                tmp[idx++] = nums[right++];
                cnt += mid - left + 1;
            }
        }

        while(left <= mid){
            tmp[idx++] = nums[left++];
        }
        while(right <= r){
            tmp[idx++] = nums[right++];
        }
        for(int i = 0; i < r - l + 1; i++){
            nums[l + i] = tmp[i];
        }

        return cnt;
    }
}
```

解题思路：

逆序对 和 归并 紧密相关

比如要归并这两个数组 [1,4,6] 和 [3,5]

第一步是[1]

第二步是[1,3], 说明 3和左边数组的剩下值都是构成逆序对，因此逆序对等于左边剩下的数个数

第三步是[1,3,4]...以此类推

因此逆序对个数 = 左边数组排序前的逆序对# + 右边# + 归并时的逆序对

因此，只需要在归并框架的基础上记录当前归并的逆序对个数并返回即可

#### [剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode.cn/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

统计一个数字在排序数组中出现的次数。

 

**示例 1:**

```
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
```

**示例 2:**

```
输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
```

 

**提示：**

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
- `nums` 是一个非递减数组
- `-109 <= target <= 109`

 

**注意：**本题与主站 34 题相同（仅返回值不同）：https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/



我的代码

```java
public int search(int[] nums, int target) {
    int l = 0, r = nums.length - 1, mid = l;
    int cnt = 0;
    while(l <= r){
        mid = (l + r) / 2;
        if(nums[mid] > target){
            r = mid - 1;
        }else if(nums[mid] < target){
            l = mid + 1;
        }else if(nums[mid] == target){//找到了
            r = mid - 1;
        }
    }
    while(l < nums.length && nums[l] == target){
        cnt++;
        l++;
    }
    return cnt;
}
```



解题思路：

就是二分查找， 上面是找到了左边界的情况，找右边界也是一样的

但是二分查找的细节很多，比如：查找到某个值，左边界，右边界这样的三种情况

就需要注意到底哪里需要等号，哪里不需要



对于普通的查找某个值，用如下代码

```java
int binarySearch(int[] nums, int target) {
    int left = 0; 
    int right = nums.length - 1; // 注意

    while(left <= right) {
        int mid = left + (right - left) / 2;
        if(nums[mid] == target)
            return mid; 
        else if (nums[mid] < target)
            left = mid + 1; // 注意
        else if (nums[mid] > target)
            right = mid - 1; // 注意
    }
    return -1;
}
```

查找左边界

```java
int left_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    // 搜索区间为 [left, right]
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            // 搜索区间变为 [mid+1, right]
            left = mid + 1;
        } else if (nums[mid] > target) {
            // 搜索区间变为 [left, mid-1]
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 收缩右侧边界
            right = mid - 1;
        }
    }
    // 判断 target 是否存在于 nums 中
    // 此时 target 比所有数都大，返回 -1
    if (left == nums.length) return -1;
    // 判断一下 nums[left] 是不是 target
    return nums[left] == target ? left : -1;
}
===============
int left_bound(int[] nums, int target) {
    int left = 0;
    int right = nums.length; // 注意
    
    while (left < right) { // 注意
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            right = mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid; // 注意
        }
    }
    return left;
}   
```

这里要注意

- 这里的重点就是收缩右侧边界

  `right = mid - 1;`没有直接的break出去，而是不断地收缩右边界



#### [剑指 Offer 53 - II. 0～n-1中缺失的数字](https://leetcode.cn/problems/que-shi-de-shu-zi-lcof/)

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

 

**示例 1:**

```
输入: [0,1,3]
输出: 2
```

**示例 2:**

```
输入: [0,1,2,3,4,5,6,7,9]
输出: 8
```

 

**限制：**

```
1 <= 数组长度 <= 10000
```

我的代码

```java
public int missingNumber(int[] nums) {
    int l = 0, r = nums.length, mid = l;
    while(l < r){
        mid = (l + r) / 2;
        if(nums[mid] == mid){
            l = mid + 1;
        }else{
            r = mid;
        }
    }
    return l;
}
```

解题思路



其实就是找到左边界，可以把这个问题理解成[0,0,0,1,1,1,1],我们需要找到1的左边界

套框架就是

```java
int left_bound(int[] nums, int target) {
    int left = 0;
    int right = nums.length; // 注意
    
    while (left < right) { // 注意
        int mid = left + (right - left) / 2;
        if (nums[mid] - mid == 1) {
            right = mid;
        } else if (nums[mid] - mid < 1) {
            left = mid + 1;
        }
    }
    return left;
}
```

简化一下就是如上的代码

#### [剑指 Offer 54. 二叉搜索树的第k大节点](https://leetcode.cn/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

给定一棵二叉搜索树，请找出其中第 `k` 大的节点的值。

 

**示例 1:**

```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
```

**示例 2:**

```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
```

 

**限制：**

- 1 ≤ k ≤ 二叉搜索树元素个数

我的代码

```java
class Solution {
    int cnt = 0;
    int target, val;
    public int kthLargest(TreeNode root, int k) {
        this.target = k;
        reverserInOrder(root);
        return val;
    }
    public void reverserInOrder(TreeNode root){
        //curr
        if(root == null || cnt == target) return;        
        reverserInOrder(root.right);
        cnt++;
        if(cnt == target){
            val = root.val;
            return;
        }
        reverserInOrder(root.left);
    }
}
```

解题思路：

就是反过来的先序遍历，就得可以得到从大到小的值了

#### [剑指 Offer 55 - I. 二叉树的深度](https://leetcode.cn/problems/er-cha-shu-de-shen-du-lcof/)

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

例如：

给定二叉树 `[3,9,20,null,null,15,7]`，

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

 

**提示：**

1. `节点总数 <= 10000`

注意：本题与主站 104 题相同：https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/w

我的代码

```java
public int maxDepth(TreeNode root) {
    if(root==null) return 0;
    int left=maxDepth(root.left);
    int right=maxDepth(root.right);
    return Math.max(left,right)+1;
}
```

解题思路：

递归得出



#### [剑指 Offer 55 - II. 平衡二叉树](https://leetcode.cn/problems/ping-heng-er-cha-shu-lcof/)

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

 

**示例 1:**

给定二叉树 `[3,9,20,null,null,15,7]`

```
    3
   / \
  9  20
    /  \
   15   7
```

返回 `true` 。

**示例 2:**

给定二叉树 `[1,2,2,3,3,null,null,4,4]`

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

返回 `false` 。

 

**限制：**

- `0 <= 树的结点个数 <= 10000`

注意：本题与主站 110 题相同：https://leetcode-cn.com/problems/balanced-binary-tree/

我的代码

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root == null) return true;
        int diff = Math.abs(maxDepth(root.left) - maxDepth(root.right));
        return diff<=1 && isBalanced(root.left) && isBalanced(root.right);
    }
     public int maxDepth(TreeNode root) {
        if(root==null) return 0;
        int left=maxDepth(root.left);
        int right=maxDepth(root.right);
        return Math.max(left,right)+1;
    }
}
```

解题思路：

核心逻辑：对于该节点，它左右子树都平衡，且左右子树高度差不超过1，就说明这个root是平衡的



#### [剑指 Offer 56 - II. 数组中数字出现的次数 II](https://leetcode.cn/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

在一个数组 `nums` 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

 

**示例 1：**

```
输入：nums = [3,4,3,3]
输出：4
```

**示例 2：**

```
输入：nums = [9,1,7,9,7,9,7]
输出：1
```

 

**限制：**

- `1 <= nums.length <= 10000`
- `1 <= nums[i] < 2^31`

我的代码

```java
public int singleNumber(int[] nums) {
    int[] bitmap = new int[32];
    for(int num : nums){
        for(int i = 0; i < bitmap.length; i++){
            bitmap[i] += num & 1;
            num >>>= 1;
        }
    }
    //recover
    int ret = 0;
    for(int i = bitmap.length - 1; i >= 0; i--){
        ret <<= 1;
        ret |= bitmap[i] % 3;
    }
    return ret;
}
```

解题思路：

核心思路：把数字x转化为二进制来看待，记录每一个位置[0,32)出现的1的个数

如果这个数字出现了3次，那么该数位一定能被3整除

否则，该数位不能被3整除

比如

```java
[3,3,3,1]
3 [0 1 1]
3 [0 1 1]
3 [0 1 1]
1 [0 0 1]
得出
[0 3 4]
```

对`[0 3 4]`求余后`[0 0 1]`就可以还原只出现了一次的数字了!



#### [剑指 Offer 57. 和为s的两个数字](https://leetcode.cn/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

 

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]
```

**示例 2：**

```
输入：nums = [10,26,30,31,47,60], target = 40
输出：[10,30] 或者 [30,10]
```

 

**限制：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^6`



我的代码

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int r = nums.length - 1, l = 0;
        while(l < r){
            int sum = nums[l] + nums[r];
            if(sum > target) r--;
            else if(sum < target) l++;
            else break;
        }
        return new int[]{nums[l], nums[r]};
    }
}
```

解题思路：

每次只做一次移动，初始化双指针分别指向数组头尾

如果此时sum>target，那么需要减小sum，只能左移动r

如果sum<target，那么需要增加sum，应该右移l

如果等于，直接break出来返回即可



#### [剑指 Offer 57 - II. 和为s的连续正数序列](https://leetcode.cn/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

输入一个正整数 `target` ，输出所有和为 `target` 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

 

**示例 1：**

```
输入：target = 9
输出：[[2,3,4],[4,5]]
```

**示例 2：**

```
输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]
```

 

**限制：**

- `1 <= target <= 10^5`



我的代码

```java
public int[][] findContinuousSequence(int target) {
    List<int[]> list = new ArrayList<>();
    int diff = 1;
    while(target > 0){
        target -= diff++;
        if(target > 0 && target % diff == 0){
            int start = target / diff;
            int[] tmp = new int[diff];
            for(int i = 0; i < diff; i++){
                tmp[i] = start + i;
            }
            list.add(0, tmp);
        }
    }
    return list.toArray(new int[list.size()][]);
}
```

解题思路：

如果这个数能由2个数值拼凑那么必须满足条件(target-1) % 2 == 0, 且开始的数值必定为 (target - 1) / 2

如果这个数值能由3个数值拼凑，那么必须满足条件(target - 1 -2) % 3 == 0, 且开始的数值必定为 (target - 1 - 2) / 3

```java
//以此类推，因此我们可以每轮让target减去一个递增值
target -= diff++;
//同时递增后的数值就是被除数
if(target % diff == 0){//满足条件，开始构建序列
    int start = target / diff;
    //遍历
}
```

#### [剑指 Offer 58 - I. 翻转单词顺序](https://leetcode.cn/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

 

**示例 1：**

```
输入: "the sky is blue"
输出: "blue is sky the"
```

**示例 2：**

```
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```

**示例 3：**

```
输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

 

**说明：**

- 无空格字符构成一个单词。
- 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
- 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。

**注意：**本题与主站 151 题相同：https://leetcode-cn.com/problems/reverse-words-in-a-string/

**注意：**此题对比原题有改动

我的代码

```java
public String reverseWords(String s) {
    String[] str = s.split(" ");
    StringBuffer sb = new StringBuffer();
    int cnt = 0;
    for(int i = str.length - 1; i >= 0; i--){
        if(str[i] == "") continue;
        if(cnt != 0) sb.append(" ");
        sb.append(str[i]);
        cnt++;
    }
    return sb.toString();
}
```

解题思路

利用api，先split(" "),这样数组中的值要么是单词，如果本来是连续的空格那么对应的值就是“”空值



#### [剑指 Offer 58 - II. 左旋转字符串](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

 

**示例 1：**

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

**示例 2：**

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

 

**限制：**

- `1 <= k < s.length <= 10000`

我的代码

```java
public String reverseLeftWords(String s, int n) {
    return s.substring(n) + s.substring(0,n);
}
```

解题思路：

为了让本题更有意义，提升一下本题难度：不能申请额外空间，只能在本串上操作

方法：

1.先反转整个字符串--这样前后顺序可以得到调换

2.翻转后n个值

3.翻转前面的值

tip：先做2/3再做1也是可以的



#### [剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode.cn/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

**示例:**

```
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

 

**提示：**

你可以假设 *k* 总是有效的，在输入数组 **不为空** 的情况下，`1 ≤ k ≤ nums.length`。

注意：本题与主站 239 题相同：https://leetcode-cn.com/problems/sliding-window-maximum/

我的代码

```java
public int[] maxSlidingWindow(int[] nums, int k) {
    int[] ret = new int[nums.length - k + 1];
    Deque<Integer> dq = new LinkedList<>();
    for(int i = 1 - k, j = 0; j < nums.length; i++, j++){
        //手动删除--最左边的值是最大值的情况
        if(i > 0 && dq.getFirst() == nums[i - 1]){
            dq.removeFirst();
        }
        //挤走前面比它小的值
        while(!dq.isEmpty() && dq.getLast() < nums[j]){
            dq.removeLast();
        }
        dq.addLast(nums[j]);
        if(i >= 0){
            ret[i] = dq.getFirst();
        }
    }
    return ret;
}
```

解题思路：

方法一：直接用priorityqueue做，但是会超时

方法二：仿照minstack的思想，但是stack是FILO，我们需要的是FIFO，所以需要一个队列，因此我们需要构建一个minqueue

对于这个queue，我们希望它unrestricted 减小排列，即最左边是最大的，但是允许等大存在

如果进来的值是max，那么它可以挤走所有其他的值，让queue中只剩下他--即进来的val左边只能存在>=val的

每次往前移动需要注意最左边的值的删除

有两种可能：

a 最左边的值就是max，那么需要手动删除

b 不是max，那么会自然被挤走

Tip：这里val左边只能存在>=val的，而不是>val的，这是因为对于这种情况[2,2,2,2]长度=3的滑动窗口，如果挤走了之后会让queue为空，没有值了



#### [剑指 Offer 59 - II. 队列的最大值](https://leetcode.cn/problems/dui-lie-de-zui-da-zhi-lcof/)

难度中等406收藏分享切换为英文接收动态反馈

请定义一个队列并实现函数 `max_value` 得到队列里的最大值，要求函数`max_value`、`push_back` 和 `pop_front` 的**均摊**时间复杂度都是O(1)。

若队列为空，`pop_front` 和 `max_value` 需要返回 -1

**示例 1：**

```
输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]
```

**示例 2：**

```
输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]
```

 

**限制：**

- `1 <= push_back,pop_front,max_value的总操作数 <= 10000`
- `1 <= value <= 10^5`

我的代码

```java
class MaxQueue {
    Deque<Integer> dq;
    Queue<Integer> queue;
    public MaxQueue() {
        dq = new LinkedList<>();
        queue = new LinkedList<>();
    }
    
    public int max_value() {
        if(dq.isEmpty()) return -1;
        return dq.getFirst();
    }
    
    public void push_back(int value) {
        queue.add(value);
        while(!dq.isEmpty() && dq.getLast() < value){
            dq.removeLast();
        }
        dq.addLast(value);
    }
    
    public int pop_front() {
        if(queue.isEmpty()) return -1;
        int val = queue.poll();
        if(dq.getFirst() == val){
            dq.removeFirst();
        }
        return val;
    }

}
```

解题思路：

就是maxqueue，参照上一题

核心思路：

1.确认最左边的值是否是最大值，如果是的话需要手动移除

2.unrestricted递减序列--进来的val可以挤走前面比它小的值



#### [剑指 Offer 60. n个骰子的点数](https://leetcode.cn/problems/nge-tou-zi-de-dian-shu-lcof/)

把n个骰子扔在地上，所有骰子朝上一面的点数之和为s。输入n，打印出s的所有可能的值出现的概率。

 

你需要用一个浮点数数组返回答案，其中第 i 个元素代表这 n 个骰子所能掷出的点数集合中第 i 小的那个的概率。

 

**示例 1:**

```
输入: 1
输出: [0.16667,0.16667,0.16667,0.16667,0.16667,0.16667]
```

**示例 2:**

```
输入: 2
输出: [0.02778,0.05556,0.08333,0.11111,0.13889,0.16667,0.13889,0.11111,0.08333,0.05556,0.02778]
```

 

**限制：**

```
1 <= n <= 11
```

我的代码

```java
public double[] dicesProbability(int n){
    //cnt[curr][n toses] = cnt[curr - 1][n - 1] + ...+ cnt[curr - 6][n - 1]
    int total = (int)Math.pow(6, n);
    int[][] cnt = new int[6 * n + 1][n + 1]; //包含所有的可能
    double[] ret = new double[5 * n + 1];
    //初始化
    for(int i = 1; i <= 6; i++){
        cnt[i][1] = 1;
    }
    for(int i = 1; i <= n; i++){
        for(int j = i; j <= 6 * i; j++){
            for(int k = 1; k <= 6; k++){
                cnt[j][i] += (j >= k) ? cnt[j - k][i - 1] : 0;
            }
            if(i == n)
                ret[j - n] += (double) cnt[j][i] / total;
        }
    }
    return ret;
}
```

解题思路：

核心思路--n个骰子合为s出现的次数 = 

(n-1)个骰子合为(s-1)出现的次数+

(n-1)个骰子合为(s-2)出现的次数+

(n-1)个骰子合为(s-3)出现的次数+

(n-1)个骰子合为(s-4)出现的次数+

(n-1)个骰子合为(s-5)出现的次数+

(n-1)个骰子合为(s-6)出现的次数

因此可以推出dp的公式了

定义一个cnt\[s][n]来计数n个骰子合为s出现的次数

那么s的长度最大为 6 * n + 1(这里+1是为了直接让val对应下标)

因此可以套框架

```java
for(n){
	for(n个骰子对应的值范围){
		for(dp的-1 到 -6--j){
            //可能会出现s比j小的情况，这种情况取0即可
            cnt[s][n] += cnt[s - j][n - 1];
        }
        //如果已经是最后一个骰子了
        //可以直接输出ret
	}
}
```

优化版一维情况





#### [剑指 Offer 61. 扑克牌中的顺子](https://leetcode.cn/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

难度简单266收藏分享切换为英文接收动态反馈

从**若干副扑克牌**中随机抽 `5` 张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

 

**示例 1:**

```
输入: [1,2,3,4,5]
输出: True
```

 

**示例 2:**

```
输入: [0,0,1,2,5]
输出: True
```

 

**限制：**

数组长度为 5 

数组的数取值为 [0, 13] .

我的代码

```java
public boolean isStraight(int[] nums) {
    Arrays.sort(nums);
    //count 0
    int zeros = 0;
    int diff = 0;
    for(int i = 0; i < nums.length; i++){
        if(nums[i] == 0){
            zeros++;
            continue;
        }
        if(i + 1 < nums.length){
            if(nums[i] == nums[i + 1]) return false;
            diff += nums[i + 1] - nums[i] - 1;
        }
    }
    return diff <= zeros;
}
```

解题思路：

tip: JQKA2不算顺子，也就是说不需要考虑循环数组的情况

只需要给数组排序，计算中间的缺的数是否能够被万能数0补上即可，同时需要注意，sort之后必须是严格increase



#### [剑指 Offer 62. 圆圈中最后剩下的数字](https://leetcode.cn/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

难度简单671收藏分享切换为英文接收动态反馈

0,1,···,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字（删除后从下一个数字开始计数）。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。

 

**示例 1：**

```
输入: n = 5, m = 3
输出: 3
```

**示例 2：**

```
输入: n = 10, m = 17
输出: 2
```

 

**限制：**

- `1 <= n <= 10^5`
- `1 <= m <= 10^6`

我的代码

```java
//递归
class Solution {
    public int lastRemaining(int n, int m) {
        return f(n, m);
    }
    public int f(int n, int m){
        if(n == 1) return 0;
        return (f(n - 1, m) + m) % n;
    }
}
//模拟法
class Solution {
    public int lastRemaining(int n, int m) {
        List<Integer> list = new ArrayList<>();
        for(int i = 0; i < n; i++){
            list.add(i);
        }
        int idx = 0;
        int size = list.size();
        while(size > 1){
            idx = (idx + m - 1) % size;
            list.remove(idx);
            size--;
        }
        return list.get(0);
    }
}
```

解题思路：

方法1：递归

令f(n, m)代表有n个数时删掉第m个数，最后的下标是f(n, m)

那么我们就可以的出来f(n, m)执行完第一步后，即删除了位置为m - 1的数后，会进入到f(n - 1, m)情况

此时我们需要知道，每一次删除其实就是将这个环形数组往前移动m个数

```java
//m = 2
1 2 3 4 5 6
3 4 5 6 1 
5 6 1 3 
```

如上，因此如果f(n - 1, m)最后的删除下标为f(n - 1, m)的话，那么f(n, m)就相当于逆过程一次，即向后移动m个数

因此可以得出核心公式

`f(n, m) = [f(n - 1, m) + m] % n` 

方法2：模拟

通过直接用一个ArrayList来模拟删除数据的情况

为了保证循环数组，`idx = (idx + m - 1) % size;`

#### [剑指 Offer 63. 股票的最大利润](https://leetcode.cn/problems/gu-piao-de-zui-da-li-run-lcof/)

难度中等281收藏分享切换为英文接收动态反馈

假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

 

**示例 1:**

```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```

**示例 2:**

```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

 

**限制：**

```
0 <= 数组长度 <= 10^5
```

 

**注意：**本题与主站 121 题相同：https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/



我的代码

```java
public int maxProfit(int[] prices) {
    int min = Integer.MAX_VALUE;
    int max = 0;
    for(int i = 0; i < prices.length; i++){
        min = Math.min(prices[i], min);
        max = Math.max(prices[i] - min, max);
    }
    return max;
}
```

解题思路：

只需要知道当下标为i的情况，i之前的min 和 max即可求出来之间的差值，这里是直接求差值了



#### [剑指 Offer 64. 求1+2+…+n](https://leetcode.cn/problems/qiu-12n-lcof/)

难度中等530收藏分享切换为英文接收动态反馈

求 `1+2+...+n` ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

 

**示例 1：**

```
输入: n = 3
输出: 6
```

**示例 2：**

```
输入: n = 9
输出: 45
```

 

**限制：**

- `1 <= n <= 10000`

我的代码

```java
class Solution {
    int ret = 0;
    public int sumNums(int n) {
        boolean flag = (n > 1) && (sumNums(n - 1) > 0);
        ret += n;
        return ret;
    }
}
```

解题思路：

利用一个全局变量来记录

由于不能使用*/，不能套公式

由于不能for while if，普通的暴力方法也不可以，递归也不行

此时可以通过短路法来达到if的效果

```java
if(A && B) //如果A false就不会执行B
if(A || B) //如果A true就不会执行B
```

因此可以通过这个方法来做一个短路，当n == 1时 就不会继续递归了

```java
boolean flag = (n > 1) && (sumNums(n - 1) > 0);
```



#### [剑指 Offer 65. 不用加减乘除做加法](https://leetcode.cn/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

难度简单345收藏分享切换为英文接收动态反馈

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

 

**示例:**

```
输入: a = 1, b = 1
输出: 2
```

 

**提示：**

- `a`, `b` 均可能是负数或 0
- 结果不会溢出 32 位整数



我的代码

```java
public int add(int a, int b) {
    int tmp = 1;
    while(tmp != 0){
        int xor = a ^ b;
        tmp = (a & b) << 1;
        a = xor;
        b = tmp;
    }
    return a;
}
```

解题思路：

可以把这题理解成这样

11 + 19做计算的时候，我们是分别对个位数做计算，然后再算是否需要进位

对二进制也是这样的 a + b

101 + 110 对每个数字做xor就是个位数字不考虑进位的值

不考虑进位 `n = a ^ b`

```assembly
 101
^110
-------
 011
```

对每个数字做 & 就是是否需要进位，同时因为进位是对左边的数字有影响，因此计算完之后需要左移

`c = (a & b) << 1`

然后 a + b 就演变成了 n + c

直到c = 0，即没有需要进位的情况



#### [剑指 Offer 67. 把字符串转换成整数](https://leetcode.cn/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/)

难度中等187收藏分享切换为英文接收动态反馈

写一个函数 StrToInt，实现把字符串转换成整数这个功能。不能使用 atoi 或者其他类似的库函数。

 

首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。

当我们寻找到的第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字组合起来，作为该整数的正负号；假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

该字符串除了有效的整数部分之后也可能会存在多余的字符，这些字符可以被忽略，它们对于函数不应该造成影响。

注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换。

在任何情况下，若函数不能进行有效的转换时，请返回 0。

**说明：**

假设我们的环境只能存储 32 位大小的有符号整数，那么其数值范围为 [−231, 231 − 1]。如果数值超过这个范围，请返回  INT_MAX (231 − 1) 或 INT_MIN (−231) 。

**示例 1:**

```
输入: "42"
输出: 42
```

**示例 2:**

```
输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。
```

**示例 3:**

```
输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。
```

**示例 4:**

```
输入: "words and 987"
输出: 0
解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
     因此无法执行有效的转换。
```

**示例 5:**

```
输入: "-91283472332"
输出: -2147483648
解释: 数字 "-91283472332" 超过 32 位有符号整数范围。 
     因此返回 INT_MIN (−231) 。
```

 

注意：本题与主站 8 题相同：https://leetcode-cn.com/problems/string-to-integer-atoi/

我的代码

```java
class Solution {
    public int strToInt(String str) {
        if(str == null) return 0;
        int val = 0;
        boolean neg = false;
        int idx = 0;
        while(idx < str.length() && str.charAt(idx) == ' '){
            idx++;
        }
        
        if(idx == str.length()) return val;
        if(str.charAt(idx) == '-' || str.charAt(idx) == '+' ){
            if(str.charAt(idx) == '-') neg = true;
            idx++;
        }
        int bdry = Integer.MAX_VALUE / 10;
        while(idx < str.length() && Character.isDigit(str.charAt(idx))){
            if(val > bdry || (val == bdry && str.charAt(idx) > '7')){
                return neg ? Integer.MIN_VALUE : Integer.MAX_VALUE;
            }
            int add = str.charAt(idx) - '0';
            val = val * 10 + add;
            idx++;
        }
        
        
        return neg? -val : val;

    }
}
```

解题思路：

核心思想：遍历字符串，进行累加

难点：整形边界判断

方法：有两种情况，val 此时已经大于边界/10了， 或者等于边界/10(此时需要判断是否越界)

```java
if(val > bdry || (val == bdry && str.charAt(idx) > '7')){
    return neg ? Integer.MIN_VALUE : Integer.MAX_VALUE;
}
```

#### [剑指 Offer 66. 构建乘积数组](https://leetcode.cn/problems/gou-jian-cheng-ji-shu-zu-lcof/)

难度中等267收藏分享切换为英文接收动态反馈

给定一个数组 `A[0,1,…,n-1]`，请构建一个数组 `B[0,1,…,n-1]`，其中 `B[i]` 的值是数组 `A` 中除了下标 `i` 以外的元素的积, 即 `B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]`。不能使用除法。

 

**示例:**

```
输入: [1,2,3,4,5]
输出: [120,60,40,30,24]
```

 

**提示：**

- 所有元素乘积之和不会溢出 32 位整数
- `a.length <= 100000`

我的代码

```java
public int[] constructArr(int[] a) {
    int[] ret = new int[a.length];
    //left to right
    for(int i = 0, product = 1; i < a.length;product *= a[i], i++){
        ret[i] = product;
    }
    //right to left
    for(int i = a.length - 1, product = 1; i >= 0; product *= a[i], i--){
        ret[i] *= product;
    }
    return ret;
}
```

解题思路

[1,2,3,4,5]

result ret[i] = a[左边累乘] * a[右边累乘]

所以可以通过用两个数组来达到

或者可以通过直接for左到右，再右到左达到省O(N)空间的效果
