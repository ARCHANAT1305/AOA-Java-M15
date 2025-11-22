
# EX 5A 0/1 Knapsack Problem - Branch&Bound 
## AIM:
To Write a Java program to solve 0/1 Knapsack problem using Branch and Bound Approach.
You are heading a college entrepreneurship cell that can invest in up to N student‑startups.

For each startup i you know: cost[i]  — the amount (in ₹ lakh) required to join the showcase profit[i] — the estimated profit (in ₹ lakh) you’ll gain if it succeeds You have a total budget of B ₹ lakh. Pick a subset of startups so that the sum of costs ≤ B and the sum of profits is maximised.

Because N can be as large as 50, a plain exhaustive search (2^N) is too slow.

The recommended approach is Branch & Bound with a fractional‑knapsack upper bound (but any algorithm that meets the constraints is accepted). 

Input Format

N

B

cost[1] cost[2] … cost[N]

profit[1] profit[2] … profit[N]

1 ≤ N ≤ 50

1 ≤ B ≤ 1 000 000

1 ≤ cost[i], profit[i] ≤ 10 000 

Output Format

maxProfit

For example:




## Algorithm
1.Start and read the number of startups N, total budget B, and arrays for cost[] and profit[]. 
2.For each startup, calculate ratio = profit / cost and sort all startups in descending order of this ratio.
3.Initialize a queue with a root node (level = –1, profit = 0, cost = 0) and set maxProfit = 0.
4. For each node, generate two branches — one including the current item and one excluding it — compute their bounds, and enqueue them if their bound exceeds maxProfit. 
5.Continue exploring nodes until the queue is empty, updating maxProfit whenever a better profit is found, then print the final maxProfit and stop.

## Program:
#### Developed by: ARCHANA T
#### Register Number: 212223240013
```
import java.util.*;

public class StartupInvestment 
{
    static class Item 
    {
        int cost, profit;
        double ratio;
        Item(int c, int p) 
        {
            cost = c;
            profit = p;
            ratio = (double) p / c;
        }
    }

    static class Node 
    {
        int level, profit, cost;
        double bound;
        Node(int level, int profit, int cost, double bound)
        {
            this.level = level;
            this.profit = profit;
            this.cost = cost;
            this.bound = bound;
        }
    }

    static double bound(Node u, int N, int B, Item[] items)
    {
        if (u.cost >= B) return 0;
        double profitBound = u.profit;
        int j = u.level + 1;
        int totalCost = u.cost;

        while (j < N && totalCost + items[j].cost <= B) 
        {
            totalCost += items[j].cost;
            profitBound += items[j].profit;
            j++;
        }

        if (j < N)
            profitBound += (B - totalCost) * items[j].ratio;

        return profitBound;
    }

    static int knapsack(int N, int B, Item[] items) 
    {
        Arrays.sort(items, (a, b) -> Double.compare(b.ratio, a.ratio));

        Queue<Node> q = new LinkedList<>();
        Node u, v;
        v = new Node(-1, 0, 0, 0);
        q.add(v);

        int maxProfit = 0;

        while (!q.isEmpty())
        {
            v = q.poll();

            if (v.level == N - 1) continue;

            u = new Node(v.level + 1, v.profit, v.cost, 0);

            // Include current item
            u.cost = v.cost + items[u.level].cost;
            u.profit = v.profit + items[u.level].profit;

            if (u.cost <= B && u.profit > maxProfit)
                maxProfit = u.profit;

            u.bound = bound(u, N, B, items);
            if (u.bound > maxProfit)
                q.add(u);

            // Exclude current item
            u = new Node(v.level + 1, v.profit, v.cost, 0);
            u.bound = bound(u, N, B, items);
            if (u.bound > maxProfit)
                q.add(u);
        }
        return maxProfit;
    }

    public static void main(String[] args) 
    {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int B = sc.nextInt();
        int[] cost = new int[N];
        int[] profit = new int[N];
        for (int i = 0; i < N; i++) cost[i] = sc.nextInt();
        for (int i = 0; i < N; i++) profit[i] = sc.nextInt();

        Item[] items = new Item[N];
        for (int i = 0; i < N; i++)
            items[i] = new Item(cost[i], profit[i]);

        System.out.println(knapsack(N, B, items));
        sc.close();
    }
}

```

## Output:

<img width="466" height="206" alt="image" src="https://github.com/user-attachments/assets/e4853fab-19e5-42b5-8dd8-4849b0f6d7e2" />


## Result:
The program successfully solved 0/1 Knapsack problem using branch & bound and output is verified. 
