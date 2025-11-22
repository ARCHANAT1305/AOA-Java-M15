
# EX 5D Flower Planting.
## AIM:
To write a Java program to for given constraints.
You are given n gardens, labelled from 1 to n.

You also have a list called paths, where each element paths[i] = [xi, yi] represents a bidirectional road connectingthe  garden xi and garden yi.

You want to plant one flower in each garden, and there are exactly 4 types of flowers labelled as 1, 2, 3, and 4.

Your goal is to plant flowers such that:

No two connected gardens (i.e., connected via a path) have the same flower type.

Return any valid flower assignment as an array where:

answer[i] is the flower type planted in the (i+1) ᵗʰ garden

It is guaranteed that:

No garden is connected to more than 3 other gardens

A valid flower assignment always exists

<img width="177" height="292" alt="image" src="https://github.com/user-attachments/assets/36aa40cb-1cdd-4746-b1a6-fc51ce6e96aa" />

## Algorithm
1. Start and read the number of gardens n and the number of paths m, then input all garden connections into a 2D array paths.
2. Build an adjacency list adj[] to represent which gardens are connected to each other.
3. Initialize an array result[] of size n to store the flower type assigned to each garden.
4. For each garden, check the flower types already used by its neighboring gardens and assign the smallest available flower type (from 1 to 4) that isn’t used
5. After assigning flower types to all gardens, print the result[] array as the final flower arrangement and stop.

 

## Program:
#### Developed by: ARCHANA T
#### Register Number: 212223240013
```
import java.util.*;

public class GardenFlowerPlanner {

    public static int[] assignFlowers(int n, int[][] paths) {
        @SuppressWarnings("unchecked")
        List<Integer>[] adj = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            adj[i] = new ArrayList<>();
        }

        // Build adjacency list
        for (int[] path : paths) {
            int u = path[0] - 1; // convert to 0-based
            int v = path[1] - 1;
            adj[u].add(v);
            adj[v].add(u);
        }

        int[] result = new int[n];

        // Assign flower types
        for (int i = 0; i < n; i++) {
            boolean[] used = new boolean[5]; // flower types 1–4
            for (int nei : adj[i]) {
                if (result[nei] != 0) {
                    used[result[nei]] = true;
                }
            }
            for (int type = 1; type <= 4; type++) {
                if (!used[type]) {
                    result[i] = type;
                    break;
                }
            }
        }

        return result;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(); 
        int m = sc.nextInt(); 

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

<img width="273" height="305" alt="image" src="https://github.com/user-attachments/assets/301e9307-d403-49fe-8120-57b270de89c9" />


## Result:
The program successfully implemented and the expected output is verified.
