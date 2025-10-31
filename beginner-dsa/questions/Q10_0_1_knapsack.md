# Q10: 0/1 Knapsack

def knapsack(weights, values, W):
    n = len(values)
    # dp[i][w] will store the max value for i items and capacity w
    dp = [[0 for _ in range(W + 1)] for _ in range(n + 1)]

    # Build table dp[][] in bottom-up manner
    for i in range(1, n + 1):
        for w in range(1, W + 1):
            if weights[i - 1] <= w:
                # Include item i-1
                dp[i][w] = max(values[i - 1] + dp[i - 1][w - weights[i - 1]],
                               dp[i - 1][w])
            else:
                # Cannot include item i-1
                dp[i][w] = dp[i - 1][w]

    return dp[n][W]

# Example usage:
weights = [2, 3, 4, 5]
values = [3, 4, 5, 6]
W = 5

print("Maximum value in Knapsack =", knapsack(weights, values, W))
