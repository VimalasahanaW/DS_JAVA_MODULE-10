# Ex23 Breadth-First Search (BFS) Traversal of a City Junction Map
## DATE: 17-11-25
## AIM:
To design and implement a java program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph, and find all reachable locations from a given source junction.
## Algorithm
1.Read the number of junctions and roads, and build the graph using an adjacency list.

2.Take the source junction from which to start BFS.

3.Initialize a queue and a visited array; mark the source as visited and enqueue it.

4.While the queue is not empty, dequeue a junction, process it, and enqueue all unvisited neighbors.

5.Output all junctions visited during BFS as the reachable locations from the source. 
  

## Program:
```
/*
Program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph
Developed by: VIMALA SAHANA W
RegisterNumber: 212223040241  
*/
import java.util.*;

public class CityBFS {

    // Function to perform BFS from source
    public static void bfs(Map<Integer, List<Integer>> graph, int source, int numJunctions) {
        boolean[] visited = new boolean[numJunctions];
        Queue<Integer> queue = new LinkedList<>();

        visited[source] = true;
        queue.add(source);

        System.out.println("Reachable junctions from junction " + source + " in BFS order:");

        while (!queue.isEmpty()) {
            int current = queue.poll();
            System.out.print(current + " ");

            for (int neighbor : graph.getOrDefault(current, new ArrayList<>())) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of junctions: ");
        int numJunctions = sc.nextInt();

        System.out.print("Enter number of roads: ");
        int numRoads = sc.nextInt();

        // Graph represented as adjacency list
        Map<Integer, List<Integer>> graph = new HashMap<>();

        System.out.println("Enter roads (junction1 junction2):");
        for (int i = 0; i < numRoads; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();

            // Undirected graph (bidirectional roads)
            graph.computeIfAbsent(u, k -> new ArrayList<>()).add(v);
            graph.computeIfAbsent(v, k -> new ArrayList<>()).add(u);
        }

        System.out.print("Enter source junction: ");
        int source = sc.nextInt();

        bfs(graph, source, numJunctions);

        sc.close();
    }
}

```

## Output:

<img width="670" height="405" alt="image" src="https://github.com/user-attachments/assets/010c889c-8b40-4cda-a695-1a57948affdb" />



## Result:
The program has been successfully implemented and executed.
It performs Breadth-First Search (BFS) traversal on a city junction map and correctly lists all reachable locations from the given source node.
