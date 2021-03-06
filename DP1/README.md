题：一个机器人位于一个 m*n 网格的最左上角 （起始点在下图中标记为 “Start” ）。机器人每次只能向下或者向右移动一步。机器人试图达到网格的最右下角（在下图中标记为 “Finish” ）。
问总共有多少条不同的路径？  
例1： 输入：m = 3, n = 7  
	  输出：28  
	    
例2： 输入：m = 3, n = 2  
	  输出：3  

机器人从(0 , 0) 位置出发，到(m - 1, n - 1)终点。  
  
  
分析:  
  
按照动规五部曲来分析：  
  
1. 确定dp数组(dp table)以及下标的含义  
dp[i][j] ：表示从(0 ，0)出发，到(i, j) 有dp[i][j]条不同的路径。  
  
2. 确定递推公式  
想要求dp[i][j]，只能有两个方向来推导出来，即dp[i - 1][j] 和 dp[i][j - 1]。  
dp[i - 1][j]表示从(0, 0)的位置到(i - 1, j)有几条路径，dp[i][j - 1]同理。  
所以，dp[i][j] =  dp[i - 1][j] + dp[i][j - 1]  
  
3. dp数组的初始化    
首先dp[i][0]一定都为1，因为从(0, 0)的位置到(i, 0)的路径只有一条，那么dp[0][j]也同理。  
所以初始化代码： for (int i = 0; i < m; i++) dp[i][0] = 1;  
				 for (int j = 0; j < n; j++) dp[0][j] = 1;  
  
4. 确定遍历顺序  
这里要看一下递归公式dp[i][j] =  dp[i - 1][j] + dp[i][j - 1]，dp[i][j]都是从其上方和左方推导而来，那么从左到右一层一层遍历就可以了。  
这样就可以保证推导dp[i][j]的时候，dp[i - 1][j] 和 dp[i][j - 1]一定是有数值的。  
  
5. 推导dp数组  
  