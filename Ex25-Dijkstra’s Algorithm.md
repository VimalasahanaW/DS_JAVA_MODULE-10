# Ex25 Finding the Fastest Route to a Charging Station using Dijkstra’s Algorithm
## DATE:
## AIM:
To design and implement a java program that helps an electric vehicle (EV) find the shortest travel time from its current block to the nearest charging station using Dijkstra’s shortest path algorithm.
## Algorithm
1.Read the graph: Take number of blocks, edges, and travel times (weighted graph) to represent the road network.

2.Read the positions of charging stations and the EV’s current block.

3.Use Dijkstra’s algorithm from the current block to compute the minimum distance (travel time) to all other blocks.

4.Find the nearest charging station by comparing distances to all charging station blocks.

5.Output the shortest travel time and the block number of the nearest charging station. 

## Program:
```
/*
Program to find the Fastest Route to a Charging Station using Dijkstra’s Algorithm
Developed by: VIMALA SAHANA W 
RegisterNumber:212223040241  
*/
import java.util.*;

public class EVChargingShortestPath {

    static class Edge {
        int target;
        int weight;
        Edge(int target, int weight) {
            this.target = target;
            this.weight = weight;
        }
    }

    public static int[] dijkstra(List<List<Edge>> graph, int source) {
        int n = graph.size();
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[source] = 0;

        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[1]));
        pq.add(new int[]{source, 0});

        boolean[] visited = new boolean[n];

        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int u = curr[0];
            if (visited[u]) continue;
            visited[u] = true;

            for (Edge edge : graph.get(u)) {
                int v = edge.target;
                int w = edge.weight;
                if (dist[u] + w < dist[v]) {
                    dist[v] = dist[u] + w;
                    pq.add(new int[]{v, dist[v]});
                }
            }
        }

        return dist;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of blocks: ");
        int n = sc.nextInt();

        System.out.print("Enter number of roads: ");
        int m = sc.nextInt();

        List<List<Edge>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        System.out.println("Enter roads (block1 block2 travel_time):");
        for (int i = 0; i < m; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            int w = sc.nextInt();
            graph.get(u).add(new Edge(v, w));
            graph.get(v).add(new Edge(u, w)); // undirected graph
        }

        System.out.print("Enter number of charging stations: ");
        int c = sc.nextInt();

        int[] chargingStations = new int[c];
        System.out.println("Enter charging station blocks:");
        for (int i = 0; i < c; i++) {
            chargingStations[i] = sc.nextInt();
        }

        System.out.print("Enter EV current block: ");
        int source = sc.nextInt();

        int[] dist = dijkstra(graph, source);

        // Find nearest charging station
        int minDist = Integer.MAX_VALUE;
        int nearestStation = -1;
        for (int station : chargingStations) {
            if (dist[station] < minDist) {
                minDist = dist[station];
                nearestStation = station;
            }
        }

        if (nearestStation != -1) {
            System.out.println("Nearest charging station: Block " + nearestStation);
            System.out.println("Shortest travel time: " + minDist);
        } else {
            System.out.println("No charging station is reachable.");
        }

        sc.close();
    }
}

```

## Output:
<img width="595" height="475" alt="image" src="https://github.com/user-attachments/assets/1132d955-5d52-40eb-8ffa-d0379dfbf21a" />



## Result:
The program has been successfully implemented and executed.
It uses Dijkstra’s algorithm to determine the shortest travel time from the EV’s current location to the nearest charging station and correctly handles cases where no station is reachable.
