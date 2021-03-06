# 学习总结

## 一、分治、回溯
1. **递归思想**
    - **最近重复性**
	根据其递归的形式、复杂度有多种多样的表现，比如分治、回溯。
    - **最优重复性**
	代表算法：动态规划。
2. **分治**
    - **分治的理解**
	把一个普通的递归分成几段不同的的drill down（可以想到相同的drill down逻辑也可以根据数值区间交给线程池执行）。
	- **分治算法的代码模板**
	基于递归方式的代码模板，但是递归模板的第三步drill down会根据问题的不同而出现多次，然后将这些drill down的结果（即子问题的结果）合并成为一个最终的结果。
	后续继续接递归模板的第四步。
3. **回溯**
    - **回溯的理解**
	每一次的递归都是一种试错，对了就返回，错了就换一个参数继续递归进行试错（即不继续往下走了，到这发现错了就回家再换个新参数），直至找到答案或者尝试了所有的可能性（最糟糕的情况会花费指数级别的时间复杂度）。
	比如：八皇后问题、数独问题等。
	- 哈希表太小

## 二、深度优先搜索（DFS）和广度优先搜索（BFS）
1. **DFS**
    - **DFS的理解**
	既然叫做深度优先，那么就是从树的根节点开始，先选中一个方向挖到底为止才会换方向，遇到子方向也有分支时依然选择先挖选定的方向（比如左边），当这个子方向挖到底返回后再去挖它的右方向，发现它的右方向也有分支，那么依然选择先挖左边的，以此类推。
	- **DFS的递归写法**
	多叉树为例，
	方式一：**肌肉记忆：递归写法**：
	```
	visited = set()
	def dfs(node, visited):
	  # 终止条件：已处理过
	  if node in visited:
	    return;
	  # 给当前节点添加处理标记（即进入已处理的集合中）
	  visited.add(node)
	  # 执行当前节点的处理逻辑
	  ...
	  # 当前节点处理完后遍历它的子节点
	  for next_nodein node.children():
	    # 如果子节点没有被处理过（二次判断，严谨起见）
	    if not next_node in visited:
		  # 递归自己进行处理
		  dfs(next_node, visited)
	```
	方式二：**肌肉记忆：用栈模拟递归**
	自行实现。
2. **BFS**
    - **BFS的理解**
	遍历一棵树时，从上往下分层，每走一步都要把这一层的所有节点“看”一遍，然后才进入下一层，直至最底层。
	- **肌肉记忆：BFS的实现**
    BFS不再使用递归或者栈循环去做了，而是使用队列来实现。
	```
	def BFS(graph, start, end):
	  queue = []
	  queue.append([start])
	  visited.add(start)
	  while queue:
	    node = queue.pop()
		visited.add(node)
		process(node)
		# 扩散出当前节点的周围节点，并依次加到队列里面
		nodes = generate_related_nodes(node)
		queue.push(nodes)
	```

## 三、贪心算法
1. **贪心算法的理解**
贪心算法是一种在每一步的选择中都选择最有利的选择，从而希望这样最终得到的结果就是全局最优结果的算法（**每一步都是鼠目寸光的选择**）。
它**和动态规划的不同在于**它对每个子问题的解决方案都做出选择，不能回退后悔。而动态规划则会保存以前的运算结果，并根据以前的结果对当前可选项进行选择，可以回退后悔。
可以发现由于贪心算法的鼠目寸光式选择导致其本身是具备很大局限性的，所以一般在使用的时候会选择“**全局搜索递归/动态规划+某一步使用贪心**”的组合。
**做个对比**：
（1）**贪心**：当下做局部最优判断
（2）**回溯**：能够回退
（3）**动态规划**：最优判断+回退
2. **贪心算法的一些应用场景**
    - **场景分析**
	问题能够分解成子问题，并且子问题的最优解能够递推到最终问题的最优解。这种子问题最优解成为**最优子结构**。
    - **举例**
    求图中的最小生成树、求哈夫曼编码
    （**贪心法一般不适用于在工程和生活中的问题**）
    然而**一旦一个问题可以通过贪心法求解，那么贪心法一般就是这个问题的最好解决方法**了。
    而由于其高效性和效果，其**也可以用做其他算法的辅助算法或者直接解决一些要求结果不特别精确的问题**。
3. **贪心算法的选取难点**
要怎么证明这个问题是可以使用贪心法的（比如做预处理、从后往前贪心等）。

## 四、二分查找
1. **肌肉记忆：二分查找的前提条件**
（1）目标函数单调性（单调递增或单调递减）
（2）存在上下界（bounded）
（3）能够通过索引访问（index accessible），即能够通过下标去访问
2. **肌肉记忆：二分查找的代码模板（这里是升序）**
```
left = 0, right = array.length - 1
while (left <= right):
  middle = (left + right) / 2
  if (array[middle] == target):
    # 说明目标找到了
	break 或者 return result
  else if (array[middle] < target):
    left = middle + 1
  else:
    right = middle - 1
```
3. **经验分享**
在实际的情况中，**二分查找法**用的**优先级**会**明显低于 牛顿迭代法**。

## 五、检讨
这周由于一些外在原因导致只看了少量题目，并且还是处于五毒神掌的第二层甚至第一层，部分题解代码没有完全掌握。第11课的课后作业没有列出所有情况，是一个半残代码，等于没有做出来。