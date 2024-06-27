# Dynamic Programming

Dynamic programming is a method for solving complex problems by breaking them down into simpler subproblems. 

The main idea is to store the solutions of subproblems to avoid redundant computations, which is typically done using a table (or memoization).

## The workflow of Dynamic Programming 
- **Identifying Subproblems**:
    Break down the main problem into smaller, independent subproblems.
- **Storing Solutions**: 
    Solve each subproblem once and store the solution, typically using a table or array to avoid redundant computations.
- **Building Up Solutions**: 
    Use the stored solutions to construct the solution to the main problem, often through iterative or recursive methods.
- **Avoiding Redundancy**: 
    Ensures each subproblem is solved only once, reducing computation time compared to naive approaches.

## Example - Coin Change Problem

Given a set of coin denominations and a target amount, determine the minimum number of coins needed to make up that amount. Assume an unlimited supply of each coin denomination.

### 1. Define the Subproblem:

Let's define dp[i] as the minimum number of coins required to make up the amount i.

### 2. Base Case:

dp[0] = 0: Zero coins are needed to make up the amount 0.

### 3. Recurrence Relation:

For each coin denomination coin, if coin <= i, then dp[i] = min(dp[i], dp[i - coin] + 1).

This means to make up the amount i, consider using each coin denomination and choose the one that minimizes the number of coins.

### Implementation:
```python
def min_coins(coins, amount):
    # Initialize the dp array with a large number (infinity)
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0  # Base case: 0 coins needed to make amount 0
    
    # Fill dp array
    for i in range(1, amount + 1):
        for coin in coins:
            if coin <= i:
                dp[i] = min(dp[i], dp[i - coin] + 1)
    
    return dp[amount] if dp[amount] != float('inf') else -1

# Example usage:
coins = [1, 5, 10, 25]
amount = 30
print(f"Minimum number of coins to make {amount} is: {min_coins(coins, amount)}")
```


