
## Article from: https://www.codechef.com/wiki/tutorial-dynamic-programming  
  
The idea of DP is to 'remember your past'. To break down problems into smaller subproblems and use the solutions to these smaller subproblems to solve a bigger problem. 
  
  
Two ways of working with subproblems is through top-down approach (memoization) or bottom-up approach (dynamic programming).  
  
DP is a bit like recursion but recursion solves all **required** subproblems and potentially solves all of these subproblems **multiple** times.  

Example DP Problem:  
Given an input number, find the fewest number of steps it would take to get the number to 1 given these functions:  
  n-1
  n/2 if n%2 = 0
  n/3 if n%3 = 0
  
Code to solve the problem translated to Java:  

```java
import java.util.Arrays;

//Top-down approach to solving example problem above
public class TopDown {

	static int[] memo;

	public static void main(String[] args) {
		int n = Integer.parseInt(args[0]);
		memo = new int[n + 1];
		Arrays.fill(memo, -1);
		System.out.println(getMinSteps(n));
	}

	public static int getMinSteps(int n) {

		if (memo[n] != -1) {
			return memo[n];
		}
		if (n == 1) {
			return 0;
		}

		int r = 1 + getMinSteps(n - 1);

		if (n % 2 == 0) {
			r = Math.min(r, 1 + getMinSteps(n / 2));
		}

		if (n % 3 == 0) {
			r = Math.min(r, 1 + getMinSteps(n / 3));
		}

		memo[n] = r;

		return r;

	}
}
```

  
  
```java
//Bottom Up approach (build table up to n)
public class BottomUp {
	public int getMinSteps(int n) {
		int dp[] = new int[n + 1];
		dp[1] = 0;
		for (int i = 2; i <= n; i++) {

			dp[i] = 1 + dp[i - 1];

			if (i % 2 == 0) {
				dp[i] = Math.min(dp[i], 1 + dp[i / 2]);
			}

			if (i % 3 == 0) {
				dp[i] = Math.min(dp[i], 1 + dp[i / 3]);
			}

		}

		return dp[n];

	}

}
```

