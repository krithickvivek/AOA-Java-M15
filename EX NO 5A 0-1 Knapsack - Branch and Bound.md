
# EX 5A 0/1 Knapsack Problem - Branch & Bound 
## Date:
## Aim:
To maximize total profit by selecting startups whose combined cost does not exceed the available budget using the Branch & Bound technique with fractional upper bound estimation.

## Problem statement:
To Write a Java program to solve 0/1 Knapsack problem using Branch and Bound Approach. You are heading a college entrepreneurship cell that can invest in up to N student‑startups. For each startup i you know: cost[i]  — the amount (in ₹ lakh) required to join the showcase profit[i] — the estimated profit (in ₹ lakh) you’ll gain if it succeeds You have a total budget of B ₹ lakh. Pick a subset of startups so that the sum of costs ≤ B and the sum of profits is maximised. Because N can be as large as 50, a plain exhaustive search (2^N) is too slow. The recommended approach is Branch & Bound with a fractional‑knapsack upper bound (but any algorithm that meets the constraints is accepted). 

**Input Format:**

N

B

cost[1] cost[2] … cost[N]

profit[1] profit[2] … profit[N]

1 ≤ N ≤ 50

1 ≤ B ≤ 1 000 000

1 ≤ cost[i], profit[i] ≤ 10 000 

**Output Format:**

maxProfit

## Algorithm
1.Read N(startups count) and B(budget), then read cost and profit arrays.  
2.Sort startups in descending order of profit-to-cost ratio to tighten upper bound efficiency.  
3.Use DFS to explore inclusion/exclusion of each startup while tracking current cost(cw) and current value(cv).  
4.Compute an upper bound using fractional knapsack logic; if bound ≤ best profit found so far, prune that branch.  
5.Update global best profit whenever a leaf node (idx==N) is reached with a higher accumulated profit.  

## Program:
```
Program to implement knapsack problem

Developed by: Krithick Vivekananda 
Register Number: 212223240075

import java.util.*;

public class StartupShowcaseOptimizer {

    // ---------- Global data ----------
    static int N, B;
    static int[] c, p;          // cost, profit after sorting by ratio
    static int best = 0;        // incumbent best profit

    // ---------- Fractional upper bound ----------
    static double bound(int idx, int cw, int cv) {
        if (cw >= B) return cv;                 // bag full or overweight
        double val = cv;
        int rem = B - cw;

        while (idx < N && c[idx] <= rem) {      // add full items
            rem -= c[idx];
            val += p[idx];
            idx++;
        }
        if (idx < N) val += p[idx] * (rem / (double) c[idx]); // fractional part
        return val;
    }

    // ---------- DFS Branch & Bound ----------
    static void dfs(int idx, int cw, int cv) {
        if (idx == N) {                 // leaf
            best = Math.max(best, cv);
            return;
        }
        if (bound(idx, cw, cv) <= best) return; // prune

        // 1. include current startup if it fits
        if (cw + c[idx] <= B)
            dfs(idx + 1, cw + c[idx], cv + p[idx]);

        // 2. exclude current startup
        dfs(idx + 1, cw, cv);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        B = sc.nextInt();
        int[] cost = new int[N];
        int[] prof = new int[N];
        for (int i = 0; i < N; i++) cost[i] = sc.nextInt();
        for (int i = 0; i < N; i++) prof[i] = sc.nextInt();
        sc.close();

        // Sort by profit/cost ratio descending → tighter bounds
        Integer[] idx = new Integer[N];
        Arrays.setAll(idx, i -> i);
        Arrays.sort(idx, Comparator.comparingDouble(i -> -(double) prof[i] / cost[i]));

        c = new int[N];
        p = new int[N];
        for (int i = 0; i < N; i++) {
            c[i] = cost[idx[i]];
            p[i] = prof[idx[i]];
        }

        dfs(0, 0, 0);
        System.out.println(best);
    }
}
```

## Output:
<img width="408" height="215" alt="image" src="https://github.com/user-attachments/assets/3d4404c9-7b3a-4f00-9e12-e5c61d133c7a" />

## Result:
The program was successfully solved 0/1 Knapsack problem using branch & bound and output is verified. 
