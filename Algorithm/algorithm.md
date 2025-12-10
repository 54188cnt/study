# 一、栈
定义：栈是一种后进先出(FILO/LIFO)的数据结构。

数据结构：
- `Deque<Object> stack = new ArrayDeque<>();`  
- `Deque<Object> stack = new LinkedList<>();`
- `Stack<Object> stack = new Stack<>()`

方法：`E peek(), push(e), E pop()`

<font color="lightblue">提示</font>：栈中的元素可以是值，也可以是指向这个值的索引。

## 1.1 单调栈
### 1.1。1 单调递减栈
定义：栈中存放的是<font color="red">单调递减的元素</font>，栈顶的元素比栈内元素都大。  

代码模板(以int为例)：
```  java
// 数组 int[] nums
int[] nums = new int[] {0,1,0,2,1,0,1,3,2,1,2,1};
Deque<Integer> stack = new ArrayDeque<>();
for (int i = 0; i < nums.length; i++) {
    int x = nums[i];
    while (!stack.isEmpty() && x >= nums[stack.peek()]) {
        int y = stack.pop();
        // 其他内部处理
    }
    stack.push(i);
}
```

题目：
- [T42.接雨水](https://leetcode.cn/problems/trapping-rain-water/description/)

### 1.1.2 单调递增栈
定义：栈中存放的是<font color="red">单调递增的元素</font>，栈顶的元素比栈内元素都小。

代码模板：
```java

```

题目：

# 二、双指针
定义：用两个指针指向数组元素，移动指针，寻找满足条件的元素。

## 2.1 快慢指针
快慢指针：快指针每次移动两步，慢指针每次移动一步，当快慢指针相遇时，慢指针所在位置就是结果。  
场景：常用于寻找链表环的入口或者判断链表有没有环。

代码模板：
```java

```

题目：

## 2.2 同向双指针
定义：两个指针同时移动，一个指针比另一个指针先移动，寻找满足条件结果。  

代码模板：
```java

```

题目：

## 2.3 相向双指针
定义：两个指针分别指向数组的头和尾，通过移动指针，寻找满足条件结果。

代码模板(以T42为例)：
```java
/**
 * T42.接雨水
 * @param height 柱子高度
 * @return 可以接的雨水量
 */
public int trap(int[] height) {
        int n = height.length, res = 0;
        int l = 0, r = n - 1;
        int preMax = 0, sufMax = 0;
        while(l < r) {
            int hL = height[l], hR = height[r];
            preMax = Math.max(preMax, hL);
            sufMax = Math.max(sufMax, hR);
            // 谁小谁先移动
            if(preMax  < sufMax){
                res += preMax - hL;
                l++;
            }else{
                res += sufMax - hR;
                r--;
            }
        }
        return res;
    }
```

题目：
- [T42.接雨水](https://leetcode.cn/problems/trapping-rain-water/description/)


# 三、回溯
定义：使用递归，配合剪枝并恢复现场得到所有结果。

代码模板(以括号生成为例):
```java
private void dfs(int left, int right, StringBuilder sb, int n){
    // 剪枝
    if(left > n || right > n) return;
    // 满足条件
    if(left + right == 2 * n) {
        // res定义为全局即可
        res.add(sb.toString());
    }
    if(left < n){
        sb.append("(");
        // 递归
        dfs(left + 1, right, sb, n);
        // 恢复现场
        sb.deleteCharAt(sb.length() - 1);
    }
    if(right < left){
        sb.append(")");
        // 递归
        dfs(left, right + 1, sb, n);
        // 恢复现场
        sb.deleteCharAt(sb.length() - 1);
    }
}
```

题目:  
- [T22.括号生成](https://leetcode.cn/problems/generate-parentheses/description/)

# 四、动态规划
定义：通过递推公式，将问题转化为子问题，得到结果。

## 4.1 一维DP
定义：一维DP数组，`dp[i]`表示组成i所需要的最小硬币数。

代码模板(以T322.零钱兑换为例):
```java
public int coinChange(int[] coins, int amount) {
    int[] dp = new int[amount + 1];
    Arrays.fill(dp, amount + 1);
    int n = coins.length;
    dp[0] = 0;
    for(int i = 1;i <= amount;++i) {
        for(int c: coins){
            if(i - c < 0) continue;
            // 递推公式
            dp[i] = Math.min(dp[i], dp[i - c] + 1);
        }
    }
    return dp[amount] < amount + 1 ? dp[amount] : -1; 
}
```

题目:
- [T322.零钱兑换](https://leetcode.cn/problems/coin-change/description/)

# 五、图
定义：图是一组节点和边组成的数据结构。

两种表示形式：
- 邻接矩阵 `int[][]`
- 邻接表 `List<Integer>[]`

两种遍历方式：
- DFS: 深度优先搜索
- BFS: 广度优先搜索

## 5.1 DFS
代码模板(以T200.岛屿数量为例):  
```java
private int m, n;
    private static final int[][] DIRS = {{-1, 0}, {0, 1}, {1, 0}, {0, -1}};
    public int numIslands(char[][] grid) {
        int m = grid.length, n = grid[0].length;
        this.m = m;
        this.n = n;
        int res = 0;
        for(int i = 0;i < m;++i){
            for(int j = 0;j < n;++j){
                if(grid[i][j] == '1') {
                    res++;
                    // 深度优先搜索
                    dfs(grid, i, j);
                }
            }
        }
        return res;
    }

    private void dfs(char[][] g, int i, int j){
        if(i < 0 || i >= m || j < 0 || j >= n) return ;
        if(g[i][j] != '1') return ;
        g[i][j] = '2';
        for(int[] d: DIRS){
            int x = i + d[0], y = j + d[1];
            // 递归
            dfs(g, x, y);
        }
    }
```

# 六、二分查找
定义：二分查找，通过不断缩小范围，找到目标元素。

基本代码模板(开区间写法)：
```java
// nums[idx] >= target
// 学会转化为查找第一个大于等于target的idx
private int binarySearch(int[] nums, int target) {
    int l = -1, r = nums.length;
    while(l + 1 < r) {
        int m = l + (r - l) >> 1;
        // 根据红蓝染色可以知道[r, nums.length)区间的值一定大于等于target
        if(nums[m] >= target) r = m;
        else l = m;
    }
    return r;
}
```

## 6.1 基础二分查找
定义：给定一个数组，查找一个数，返回索引。  

代码模板见基本代码模板。

## 6.2 数值二分查找
定义：通过直接在数值区间进行二分。  



# 七、树
定义：树是一类无向图，其中任意两个顶点之间至多存在一条路径。  

二叉树四种遍历方式：
- 先序遍历
- 中序遍历
- 后序遍历
- 层序遍历

## 7.1 四种遍历方式模板



## 7.2 前缀树/字典树
基本模板：
```java
public class Trie {
    // 这个是一般用于a-z的英文字母字典树
    private static class Node {
        Node[] child = new Node[26];
        boolean isEnd = false;
        // 还可以加一些其他属性, 例如cnt(字符出现组数)
    }
    // 根节点
    private final Node root = new Node();

    public Trie() {}

    public void insert(String word) {
        Node cur = root;
        for(char c: word.toCharArray()){
            int idx = c - 'a';
            if(cur.child[idx] == null) cur.child[idx] = new Node();
            cur = cur.child[idx];
        }
        cur.isEnd = true;
    }
    
    // cur.isEnd = true;
    // 搜索单词
    public boolean search(String word) {
        return find(word) == 2;
    }
    
    // cur.isEnd 无关
    // 搜索前缀
    public boolean startsWith(String prefix) {
        return find(prefix) != 0;
    }

    private int find(String word) {
        Node cur = root;
        for(char c: word.toCharArray()){
            int idx = c - 'a';
            if(cur.child[idx] == null) return 0;
            cur = cur.child[idx];
        }
        return cur.isEnd ? 2 : 1;
    }
}
```

可扩展节点模板：
```java
class Trie {
    private String word;
    private Map<Character, Trie> children;
    private boolean isWord;
    public Trie() {
        word = "";
        children = new HashMap<>();
    }
    public void insert(String word) {
        Trie cur = this;
        for(char c: word.toCharArray()) {
            if(!cur.children.containsKey(c)) {
                cur.children.put(c, new Trie());
            }
            cur = cur.children.get(c);
        }
        cur.word = word;
    }
}
```

# 八、哈希表
定义：哈希表是一种数据结构，用于存储键值对。

常见的Map结构：Map(不可以new), HashMap


# 九、字符串
定义：字符串是一组字符的集合。字符串一旦创建不可修改。

常用方法：
- `int indexOf(String str)`

## 9.1 字符串匹配(KMP)



# 十、队列
定义：队列是一种数据结构，FIFO(先进先出)。

数据结构：
- `Deque<Obejct> queue = new LinkedList<>();`
- `Deque<Object> queue = new ArrayDeque<>();`
- `Queue<Object> queue = new LinkedList<>();`

方法：`boolean offer(e), E poll(), E peek()`

## 10.1 优先队列
定义：优先队列其实就是堆，一般默认都是小顶堆。  

数据结构：`PriorityQueue<Obejct> queue = new PriorityQueue<>();`

方法：`boolean offer(e), E poll(), E peek()`

代码模板(以T23.合并k个升序链表为例):
```java
public ListNode mergeKLists(ListNode[] lists) {
        if(lists == null || lists.length == 0) return null;
        int n = lists.length;
        if(n == 1) return lists[0];
        // 创建小根堆
        PriorityQueue<ListNode> queue = new PriorityQueue<>(n, (a, b) -> a.val - b.val);
        for(ListNode node: lists) {
            if(node != null) {
                queue.offer(node);
            }
        }
        ListNode dummy = new ListNode(), pre = dummy;
    while(!queue.isEmpty()) {
        ListNode node = queue.poll();
        if(node.next != null) queue.offer(node.next);
        pre.next = node;
        pre = node;
    }
        return dummy.next;
    }
```