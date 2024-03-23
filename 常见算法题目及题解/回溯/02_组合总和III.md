题目链接：[216. 组合总和 III](https://leetcode.cn/problems/combination-sum-iii/)

题目描述：找出所有相加之和为 n 的 k 个数的组合，且满足下列条件：

* 只使用数字1到9
* 每个数字 最多使用一次 
返回 所有可能的有效组合的列表 。该列表不能包含相同的组合两次，组合可以以任何顺序返回。

解题思路：使用回溯算法，从 1-9 开始尝试加入每个数字，比如从 1 开始尝试，那么下一层就是尝试加入 2-9。每次加完之后进行递归然后回溯。终止条件，如果路径总和已经大于n，直接返回终止；如果路径数组的长度大于k，直接返回终止；如果总和等于n并且路径数组等于k就直接收集结果。否则进行递归搜索，从startIndex开始尝试到9，路径加入i，sum加i，然后递归搜索下一层，然后回溯。

参考代码：

```java
class Solution {
    public List<List<Integer>> result = new ArrayList<>();
    public List<Integer> path = new ArrayList<>();
    public List<List<Integer>> combinationSum3(int k, int n) {
        backtracking(k, n, 0, 1);
        return result;
    }
    public void backtracking(int k, int n, int sum, int startIndex) {
        // 终止条件
        if(sum > n) {
            return;
        }
        if(path.size() > k) {
            return;
        }
        if(sum == n && path.size() == k) {
            // 收集结果
            result.add(new ArrayList<>(path));
            return;
        }
        // 递归搜索
        for(int i = startIndex; i <= 9; i++) {
            path.add(i);
            sum += i;
            backtracking(k, n, sum, i + 1);
            sum -= i;
            path.removeLast();
        }
    }
}
```


