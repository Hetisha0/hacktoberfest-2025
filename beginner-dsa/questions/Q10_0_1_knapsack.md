public class Knapsack {

    // Function to solve the 0/1 Knapsack problem
    public static int knapSack(int W, int[] weights, int[] values, int n) {
        // dp[i][w] will store the maximum value for first i items with capacity w
        int[][] dp = new int[n + 1][W + 1];

        // Build the dp table
        for (int i = 0; i <= n; i++) {
            for (int w = 0; w <= W; w++) {
                if (i == 0 || w == 0)
                    dp[i][w] = 0; // Base case: no items or capacity 0
                else if (weights[i - 1] <= w)
                    dp[i][w] = Math.max(
                        values[i - 1] + dp[i - 1][w - weights[i - 1]], // Include item
                        dp[i - 1][w]                                  // Exclude item
                    );
                else
                    dp[i][w] = dp[i - 1][w]; // Item too heavy to include
            }
        }

        return dp[n][W]; // Maximum value achievable with n items and capacity W
    }

    // Driver code to test the function
    public static void main(String[] args) {
        int[] values = {60, 100, 120}; // values of items
        int[] weights = {10, 20, 30};  // weights of items
        int W = 50;                    // Knapsack capacity
        int n = values.length;

        int maxValue = knapSack(W, weights, values, n);
