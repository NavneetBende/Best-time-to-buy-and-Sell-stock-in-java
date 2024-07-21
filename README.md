Best time to buy and Sell stock in Java
Here, in this page we will discuss the program to find the best time to buy and sell stock in C  We are given with an array represents the cost of a stock on each day is given in an array, find the max profit that you can make by buying and selling in those days.

Example :

Input: Prices[ ] = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5. Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

 
Best time to buy and sell in C
Algorithm :
Take the size of the array from the user and store it in variable say n.
Now, declare an array of size n and takes n integer value from the user and store them in array.
Create an array named max_sp of size equals size of price array and a variable max and initialize it as the minimum value.
Start from the last index in price array.
If prices[i] is greater than max
Update max as prices[i] and make max_sp[i] as minimum value
Else if price[i] is not greater than max
Update max_sp[i] = max.
After the pre computation, we follow the naive approach and replace the inner nested loop by using the max_sp array that we just created.
Print value of max.
Code in Java
Run
public class Main {
    static int findMaximumProfit(int[] prices, int i, int k, int buy, int[][] v) {
        // If no stock can be chosen
        if (i >= prices.length || k <= 0) return 0;
        if (v[i][buy] != -1) return v[i][buy];
        int nbuy;
        if (buy == 1)
            nbuy = 0;
        else
            nbuy = 1;
        if (buy == 1) {
            return v[i][buy] = Math.max(-prices[i] + findMaximumProfit(prices, i + 1, k, nbuy, v),
                                        findMaximumProfit(prices, i + 1, k, (int)(buy), v));
        }
        // Otherwise
        else {
            // Buy now
            if (buy == 1)
                nbuy = 0;
            else
                nbuy = 1;
            return v[i][buy] =
                       Math.max(prices[i] + findMaximumProfit(prices, i + 1, k - 1, nbuy, v),
                                findMaximumProfit(prices, i + 1, k, buy, v));
        }
    }
    static int maxProfit(int[] prices) {
        int n = prices.length;
        int[][] v = new int[n][2];
        for (int i = 0; i < v.length; i++) {
            v[i][0] = -1;
            v[i][1] = -1;
        }
        return findMaximumProfit(prices, 0, 1, 1, v);
    }
    // Driver Code
    public
    static void main(String[] args) {
        // Given prices
        int[] prices = {7, 1, 5, 3, 6, 4};
        int ans = maxProfit(prices);
        // Print answer
        System.out.println("Best time to buy and Sell stock = "+ans);
    }
}
Output
5
