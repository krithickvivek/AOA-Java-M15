
# EX 5C Graph coloring
## Date:
## Aim:
To write a Java program that checks whether it is possible to assign at most **m** different channels (colors) to **n** wireless towers such that no two directly connected towers share the same channel, using backtracking-based graph coloring.

## Problem Description:
To write a Java program to for given constraints. In a hilly region, several radio towers are installed to provide communication services. However, due to signal interference, two adjacent towers (i.e., in communication range of each other) must not use the same frequency channel. You are given N radio towers and their communication ranges represented as an undirected graph. Your task is to assign channels (colors) to these towers using at most M channels such that no two adjacent towers use the same channel. Write a program to determine if such an assignment is possible or not.

**Input Format:**

First line contains two integers: N (number of towers), and M (number of available frequency channels).

Next line contains an integer E — number of edges representing the communication range.

Next E lines contain two integers u and v — representing that tower u and tower v are within range (0-based index).

**Output Format:**

Print "YES" if it's possible to assign frequencies to towers such that no two adjacent towers have the same frequency.

Otherwise, print "NO".

<img width="182" height="440" alt="image" src="https://github.com/user-attachments/assets/b32078a2-c79d-4a25-88c4-e51144b5456f" />

## Algorithm
1. Read `n` (number of towers), `m` (number of channels), and `e` (number of connections) from input.  
2. Initialize an adjacency list `graph` of size `n` and read `e` edges; for each connection `(u, v)` add `v` to `graph[u]` and `u` to `graph[v]`.  
3. Create an integer array `color[n]` initialized with 0 to represent uncolored towers.  
4. Call `isColorable(graph, color, 0, m, n)` which tries to assign a valid color (1..m) to each tower using recursion:  
   - For the current tower `node`, try each color `c` from 1 to `m`.  
   - For each `c`, call `isSafe(graph, color, node, c)` to check that no neighbor of `node` already has color `c`.  
   - If safe, assign `color[node] = c` and recursively color the next node `node + 1`; if at any point `node == n`, return `true`.  
   - If no color works for a node, backtrack by resetting `color[node]` to 0 and return `false`.  
5. After the call returns, if `isColorable` is `true`, print `"YES"`; otherwise print `"NO"`.  

## Program:
```
Program to implement graph coloring

Developed by: Krithick Vivekananda 
Register Number: 212223240075

import java.util.*;

public class prog {

    public static boolean isColorable(List<List<Integer>> graph, int[] color, int node, int m, int n) {
        if (node == n) return true;

        for (int c = 1; c <= m; c++) {
            if (isSafe(graph, color, node, c)) {
                color[node] = c;
                if (isColorable(graph, color, node + 1, m, n))
                    return true;
                color[node] = 0;
            }
        }
        return false;
    }

    public static boolean isSafe(List<List<Integer>> graph, int[] color, int node, int c) {
        for (int neighbor : graph.get(node)) {
            if (color[neighbor] == c)
                return false;
        }
        return true;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(); // number of towers
        int m = sc.nextInt(); // number of channels
        int e = sc.nextInt(); // number of connections

        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++)
            graph.add(new ArrayList<>());

        for (int i = 0; i < e; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int[] color = new int[n];

        if (isColorable(graph, color, 0, m, n))
            System.out.println("YES");
        else
            System.out.println("NO");

        sc.close();
    }
}
```

## Output:
<img width="337" height="476" alt="image" src="https://github.com/user-attachments/assets/37986b37-fd3c-4bc7-8c6b-8e107db7b721" />

## Result:
The program was successfully implemented and the expected output is verified.
