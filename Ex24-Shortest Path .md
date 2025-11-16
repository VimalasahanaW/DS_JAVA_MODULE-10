# Ex24 Shortest Path and Reachability in a Heritage Town using BFS
## DATE: 17-11-25
## AIM:
To design and implement a java program that, given a map of attractions in a heritage town connected by walking paths, recommends:
The shortest number of paths (minimum hops) from a starting attraction to a target attraction.
The number of reachable attractions from the same starting point using Breadth-First Search (BFS)


## Algorithm
1.Read the map: Number of attractions and walking paths; build an adjacency list.

2.Take the starting attraction and optionally the target attraction.

3.Perform BFS from the starting point:

4.Keep track of distance (hops) for each node.

     Mark nodes as visited.

     Find shortest path to the target by using the distance array.

5.Count all reachable attractions during BFS and output both results. 


## Program:
```
/*
Program to determine Shortest Path and Reachability in a Heritage Town using BFS
Developed by: VIMALA SAHANA W
RegisterNumber: 212223040241  
*/
import java.util.*;

public class HeritageTownMap {

    public static void bfs(Map<Integer, List<Integer>> graph, int start, int target, int numAttractions) {
        boolean[] visited = new boolean[numAttractions];
        int[] distance = new int[numAttractions]; // distance in hops
        Arrays.fill(distance, -1);

        Queue<Integer> queue = new LinkedList<>();
        visited[start] = true;
        distance[start] = 0;
        queue.add(start);

        int reachableCount = 0;

        while (!queue.isEmpty()) {
            int current = queue.poll();
            reachableCount++;

            for (int neighbor : graph.getOrDefault(current, new ArrayList<>())) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    distance[neighbor] = distance[current] + 1;
                    queue.add(neighbor);
                }
            }
        }

        System.out.println("Number of reachable attractions from attraction " + start + ": " + reachableCount);
        if (distance[target] != -1) {
            System.out.println("Minimum number of paths (hops) from attraction " + start + " to " + target + ": " + distance[target]);
        } else {
            System.out.println("Target attraction " + target + " is not reachable from attraction " + start);
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of attractions: ");
        int numAttractions = sc.nextInt();

        System.out.print("Enter number of walking paths: ");
        int numPaths = sc.nextInt();

        Map<Integer, List<Integer>> graph = new HashMap<>();
        System.out.println("Enter paths (attraction1 attraction2):");
        for (int i = 0; i < numPaths; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();

            graph.computeIfAbsent(u, k -> new ArrayList<>()).add(v);
            graph.computeIfAbsent(v, k -> new ArrayList<>()).add(u);
        }

        System.out.print("Enter starting attraction: ");
        int start = sc.nextInt();

        System.out.print("Enter target attraction: ");
        int target = sc.nextInt();

        bfs(graph, start, target, numAttractions);

        sc.close();
    }
}

```

## Output:

<img width="740" height="446" alt="image" src="https://github.com/user-attachments/assets/bdd8c1a7-62fe-4f1c-8079-dc8640239b5e" />


## Result:
The program has been successfully implemented and executed.
It correctly computes:
The shortest number of paths (minimum hops) between two attractions.
The total number of reachable attractions from a given starting point using BFS traversal.
