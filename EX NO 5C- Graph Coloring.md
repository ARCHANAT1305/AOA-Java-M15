
# EX 5C Graph coloring
## AIM:
To write a Java program to for given constraints.
Problem Description:
In a hilly region, several radio towers are installed to provide communication services. However, due to signal interference, two adjacent towers (i.e., in communication range of each other) must not use the same frequency channel.

You are given N radio towers and their communication ranges represented as an undirected graph. Your task is to assign channels (colors) to these towers using at most M channels such that no two adjacent towers use the same channel.

Write a program to determine if such an assignment is possible or not.

Input Format:
First line contains two integers: N (number of towers), and M (number of available frequency channels).

Next line contains an integer E — number of edges representing the communication range.

Next E lines contain two integers u and v — representing that tower u and tower v are within range (0-based index).

Output Format:
Print "YES" if it's possible to assign frequencies to towers such that no two adjacent towers have the same frequency.

Otherwise, print "NO".

<img width="182" height="440" alt="image" src="https://github.com/user-attachments/assets/b32078a2-c79d-4a25-88c4-e51144b5456f" />


## Algorithm
1. Start and read the number of towers n, available channels m, and the number of connections e, then build the adjacency list graph.
2. Initialize a color[] array of size n to store the assigned channel for each tower, starting with all zeros (unassigned).
3. Use backtracking — for each tower (node), try assigning one of the m channels such that no adjacent tower uses the same channel.
4.If a valid channel is found for the current tower, recursively assign channels to the next tower; if no valid option exists, backtrack and try a different channel.  
5. If all towers are successfully assigned channels, print "YES"; otherwise, print "NO" and stop.  

## Program:
#### Developed by:ARCHANA T 
#### Register Number: 212223240013
```
import java.util.*;

public class RadioTowerChannelAssignment {

    public static boolean isColorable(List<List<Integer>> graph, int[] color, int node, int m, int n) {
        //Write your code
        if (node == n) return true;

        for (int c = 1; c <= m; c++) {
            boolean canUse = true;
            for (int neighbor : graph.get(node)) {
                if (color[neighbor] == c) {
                    canUse = false;
                    break;
                }
            }

            if (canUse) {
                color[node] = c;
                if (isColorable(graph, color, node + 1, m, n))
                    return true;
                color[node] = 0; // backtrack
            }
        }
        return false;
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

<img width="319" height="320" alt="image" src="https://github.com/user-attachments/assets/0d952b93-ca99-4a1d-a58c-3885c6a36f82" />


## Result:
The program successfully implemented and the expected output is verified.
