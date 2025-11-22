
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.
<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm
1. Start and read the number of vertices V and edges E, then store all edges with their source, destination, and weight in a list
2. Initialize each vertex as its own parent (forming V separate components) and set all cheapest edges to -1.
3. For each iteration, find the cheapest edge connecting each component to a different component using the find() operation.
4. Add all these cheapest edges to the Minimum Spanning Tree (MST), using union() to merge connected components and update the total MST weight. 
5. Repeat until all vertices are connected into a single component (numTrees == 1), then print all selected edges and the total MST weight, and stop.



## Program:
#### Developed by: ARCHANA T
#### Register Number: 212223240013
```
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
        int[] cheapest = new int[V];
        int numTrees = V;
        int MSTweight = 0;

        for (int v = 0; v < V; v++)
            parent[v] = v;

        while (numTrees > 1) {
            Arrays.fill(cheapest, -1);

            // Find cheapest edge for each component
            for (int i = 0; i < edges.size(); i++) {
                Edge e = edges.get(i);
                int set1 = find(e.src);
                int set2 = find(e.dest);

                if (set1 == set2)
                    continue;

                if (cheapest[set1] == -1 || edges.get(cheapest[set1]).weight > e.weight)
                    cheapest[set1] = i;

                if (cheapest[set2] == -1 || edges.get(cheapest[set2]).weight > e.weight)
                    cheapest[set2] = i;
            }

            // Add the cheapest edges to MST
            for (int i = 0; i < V; i++) {
                if (cheapest[i] != -1) {
                    Edge e = edges.get(cheapest[i]);
                    int set1 = find(e.src);
                    int set2 = find(e.dest);

                    if (set1 == set2)
                        continue;

                    System.out.println("Edge: " + e.src + "-" + e.dest + " Weight: " + e.weight);
                    MSTweight += e.weight;
                    union(set1, set2);
                    numTrees--;
                }
            }
        }

        return MSTweight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt(); // number of vertices
        int E = sc.nextInt(); // number of edges

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
        src = s;
        dest = d;
        weight = w;
    }
}

```

## Output:

<img width="762" height="561" alt="image" src="https://github.com/user-attachments/assets/1f1fde11-76de-47c2-a299-7f6cbf21d166" />


## Result:
The program successfully implemented and the expected output is verified.
