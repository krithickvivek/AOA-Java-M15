
# EX 5E Minimum Spanning Tree - Boruvka's Algorithm
## Date:
## Aim:
To implement Borůvka’s algorithm to compute the Minimum Spanning Tree (MST) of a connected, weighted, undirected graph by repeatedly selecting the cheapest edge for each component until only one component remains.

## Problem statement:
To write a Java program to for given constraints. Find the MST using Boruvka's Algorithm for a weighted undirected graph.

<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm
1. Initialize each vertex as its own component using a parent array for Union–Find.
2. Repeat until only one component remains:  
   a. Create an array `cheapest[]` to store the cheapest outgoing edge for each component.  
   b. Traverse all edges and update the cheapest outgoing edge for each component.  
   c. For each component, add its cheapest edge to the MST if it connects two different components.  
   d. Union the components and update MST weight.
3. Print each edge added to the MST.
4. After all components merge, return the total MST weight.

## Program:
```
Program to implement boruvka's algorithm

Developed by: Krithick Vivekananda
Register Number: 212223240075

import java.util.*;

public class BoruvkaMST {
    static int[] parent;

    static int find(int i) {
        if (parent[i] != i)
            parent[i] = find(parent[i]);
        return parent[i];
    }

    static void union(int x, int y) {
        parent[find(x)] = find(y);
    }

    
    static int boruvkaMST(int V, List<Edge> edges) {
        parent = new int[V];
        for (int i = 0; i < V; i++) parent[i] = i;

        int components = V;
        int mstWeight = 0;

        while (components > 1) {
            Edge[] cheapest = new Edge[V];

            // Find cheapest edge for each component
            for (Edge e : edges) {
                int set1 = find(e.src), set2 = find(e.dest);
                if (set1 == set2) continue;

                if (cheapest[set1] == null || cheapest[set1].weight > e.weight)
                    cheapest[set1] = e;

                if (cheapest[set2] == null || cheapest[set2].weight > e.weight)
                    cheapest[set2] = e;
            }

            // Add cheapest edges to MST and union the components
            for (int i = 0; i < V; i++) {
                Edge e = cheapest[i];
                if (e != null && find(e.src) != find(e.dest)) {
                    mstWeight += e.weight;
                    union(e.src, e.dest);
                    components--;
                    System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);
                }
            }
        }
        return mstWeight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();
        for (int i = 0; i < E; i++) {
            edges.add(new Edge(sc.nextInt(), sc.nextInt(), sc.nextInt()));
        }

        int totalWeight = boruvkaMST(V, edges);
        System.out.println("Total Weight of MST: " + totalWeight);

        sc.close();
    }
}

class Edge {
    int src, dest, weight;
    Edge(int s, int d, int w) {
        src = s; dest = d; weight = w;
    }
}
```

## Output:
<img width="700" height="488" alt="image" src="https://github.com/user-attachments/assets/06daca0e-50cc-4e7b-bd44-3fcd04e2160a" />

## Result:
The program was successfully implemented and the expected output is verified.
