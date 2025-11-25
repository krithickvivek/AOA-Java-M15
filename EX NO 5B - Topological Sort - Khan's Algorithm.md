
# EX 5B Topological Sort - Khan's Algorithm
## Date:
## Aim:
To determine a valid order of executing tasks based on given dependency constraints using **Kahn’s Algorithm (Topological Sorting)**. If a cycle exists, scheduling is impossible.

## Problem Statement:
To write a Java program to for given constraints. A software development team is preparing for a product release. The release consists of multiple tasks, each dependent on other tasks being completed first. You are to determine a valid order in which all tasks can be completed. If it's not possible due to cyclic dependencies, output that the release cannot be scheduled. Each task is labeled from 0 to n-1. The dependencies are provided in the form of pairs [a, b] which means task a depends on task b. Implement a program to find a valid task execution order using topological sort.

**Input Format:**

An integer n — number of tasks.

An integer m — number of dependencies.

m lines follow with two integers a and b — representing a depends on b.

**Output Format:**

If a valid order exists, print the task numbers in a possible execution order (space-separated).

If not, print "Release cannot be scheduled".

<img width="341" height="363" alt="image" src="https://github.com/user-attachments/assets/f0355541-4f66-49da-bcd3-171a799a7c1f" />

## Algorithm
1.Initialize adjacency list `graph` and `indegree` array for all tasks.  
2.Fill the graph based on dependencies: for each `b → a` increase indegree of `a`.  
3.Add all tasks with `indegree = 0` to a queue (tasks that can run first).  
4.While queue not empty: remove a task, add it to order list, decrease indegree of all its neighbors, and push neighbors with indegree 0 into queue.  
5.If all tasks are processed return order, else return null indicating scheduling is not possible. 

## Program:
```
Program to implement topological sort

Developed by: Krithick Vivekananda 
Register Number: 212223240075

import java.util.*;

public class prog{

    public static List<Integer> findTaskOrder(int n, int[][] dependencies) {
        List<Integer> order = new ArrayList<>();
        List<List<Integer>> graph = new ArrayList<>();
        int[] indegree = new int[n];

        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int[] dep : dependencies) {
            graph.get(dep[1]).add(dep[0]);
            indegree[dep[0]]++;
        }

        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) q.offer(i);
        }

        while (!q.isEmpty()) {
            int curr = q.poll();
            order.add(curr);
            for (int neighbor : graph.get(curr)) {
                indegree[neighbor]--;
                if (indegree[neighbor] == 0) q.offer(neighbor);
            }
        }

        if (order.size() != n) return null;
        return order;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(); // number of tasks
        int m = sc.nextInt(); // number of dependencies

        int[][] dependencies = new int[m][2];
        for (int i = 0; i < m; i++) {
            dependencies[i][0] = sc.nextInt(); // a
            dependencies[i][1] = sc.nextInt(); // b
        }

        List<Integer> result = findTaskOrder(n, dependencies);

        if (result == null) {
            System.out.println("Release cannot be scheduled");
        } else {
            for (int task : result) {
                System.out.print(task + " ");
            }
        }
    }
}
```

## Output:
<img width="818" height="525" alt="image" src="https://github.com/user-attachments/assets/97257a44-3247-4b3f-8b36-efe9776023e4" />

## Result:
The program was successfully implemented and the expected output is verified.
