# EX 5D Flower Planting
## Date:
## Aim:
To assign one of four flower types to each garden such that no two adjacent gardens share the same flower type, using a greedy adjacency-checking approach.

## Problem statement:
To write a Java program to for given constraints. You are given n gardens, labelled from 1 to n. You also have a list called paths, where each element paths[i] = [xi, yi] represents a bidirectional road connectingthe  garden xi and garden yi. You want to plant one flower in each garden, and there are exactly 4 types of flowers labelled as 1, 2, 3, and 4. Your goal is to plant flowers such that:

No two connected gardens (i.e., connected via a path) have the same flower type.

Return any valid flower assignment as an array where:

answer[i] is the flower type planted in the (i+1)ᵗʰ garden

It is guaranteed that:

- No garden is connected to more than 3 other gardens

- A valid flower assignment always exists

<img width="177" height="292" alt="image" src="https://github.com/user-attachments/assets/36aa40cb-1cdd-4746-b1a6-fc51ce6e96aa" />

## Algorithm
1. Initialize an adjacency list `adj` for all gardens.
2. Read all paths and add each connection to both gardens' adjacency lists.
3. Create an array `result[]` of size `n` to store the flower type of each garden.
4. For each garden `i`:  
   a. Create a boolean array `used[1..4]` to mark flowers used by neighbors.  
   b. For every neighbor, mark its flower type as used.  
   c. Assign the first available flower type (1–4) that is not used.
5. Print the assigned flower type for each garden.

## Program:
```
Program to implement flower planting

Developed by: Krithick Vivekananda 
Register Number: 212223240075

import java.util.*;

public class GardenFlowerPlanner {

    public static int[] assignFlowers(int n, int[][] paths) {
        @SuppressWarnings("unchecked")
        List<Integer>[] adj = new ArrayList[n];

        for (int i = 0; i < n; i++) {
            adj[i] = new ArrayList<>();
        }

        for (int[] path : paths) {
            int a = path[0] - 1;
            int b = path[1] - 1;
            adj[a].add(b);
            adj[b].add(a);
        }

        int[] result = new int[n]; // answer[i] is the flower type of garden i+1

        for (int i = 0; i < n; i++) {
            boolean[] used = new boolean[5]; // flowers 1 to 4

            for (int neighbor : adj[i]) {
                int flower = result[neighbor];
                if (flower != 0) {
                    used[flower] = true;
                }
            }

            for (int flower = 1; flower <= 4; flower++) {
                if (!used[flower]) {
                    result[i] = flower;
                    break;
                }
            }
        }

        return result;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(); // number of gardens
        int m = sc.nextInt(); // number of paths

        int[][] paths = new int[m][2];
        for (int i = 0; i < m; i++) {
            paths[i][0] = sc.nextInt();
            paths[i][1] = sc.nextInt();
        }

        int[] result = assignFlowers(n, paths);

        for (int flower : result) {
            System.out.print(flower + " ");
        }
        System.out.println();
    }
}
```

## Output:
<img width="464" height="449" alt="image" src="https://github.com/user-attachments/assets/ae7214fe-2b42-4dbc-9115-5fc74ff34704" />

## Result:
The program was successfully implemented and the expected output is verified.
