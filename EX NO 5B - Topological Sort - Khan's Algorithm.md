
# EX 5B Topological Sort - Khan's Algorithm
## AIM:
To write a Java program to for given constraints.
Problem Description:
A software development team is preparing for a product release. The release consists of multiple tasks, each dependent on other tasks being completed first. You are to determine a valid order in which all tasks can be completed. If it's not possible due to cyclic dependencies, output that the release cannot be scheduled.

Each task is labeled from 0 to n-1. The dependencies are provided in the form of pairs [a, b] which means task a depends on task b.

Implement a program to find a valid task execution order using topological sort.

Input Format:

An integer n — number of tasks.

An integer m — number of dependencies.

m lines follow with two integers a and b — representing a depends on b.

Output Format:

If a valid order exists, print the task numbers in a possible execution order (space-separated).

If not, print "Release cannot be scheduled".

<img width="341" height="363" alt="image" src="https://github.com/user-attachments/assets/f0355541-4f66-49da-bcd3-171a799a7c1f" />

## Algorithm
1. Start and read the number of tasks n and the number of dependencies m, then input all dependency pairs.
2. Build a directed graph using an adjacency list, and compute the indegree (number of prerequisites) for each task.
3. Add all tasks with indegree 0 (no dependencies) to a queue, as they can be done first.
4.  Perform topological sorting — repeatedly remove a task from the queue, add it to the result list, and decrease the indegree of its dependent tasks, adding them to the queue when their indegree becomes 0.
5. If all tasks are scheduled (result size = n), print the order; otherwise, print “Release cannot be scheduled” and stop.

## Program:
#### Developed by: ARCHANA T
#### Register Number: 212223240013
```
import java.util.*;

public class prog{

    public static List<Integer> findTaskOrder(int n, int[][] dependencies) {
       //Write your code
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());
        int[] indegree = new int[n];

        for (int[] dep : dependencies) {
            int a = dep[0], b = dep[1];
            graph.get(b).add(a);
            indegree[a]++;
        }

        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0)
                q.add(i);
        }

        List<Integer> order = new ArrayList<>();
        while (!q.isEmpty()) {
            int curr = q.poll();
            order.add(curr);
            for (int next : graph.get(curr)) {
                indegree[next]--;
                if (indegree[next] == 0)
                    q.add(next);
            }
        }

        if (order.size() != n)
            return null;
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
<img width="587" height="364" alt="image" src="https://github.com/user-attachments/assets/3e374221-f72b-416d-9c7d-9557bf4889ea" />



## Result:
The program successfully implemented and the expected output is verified.
