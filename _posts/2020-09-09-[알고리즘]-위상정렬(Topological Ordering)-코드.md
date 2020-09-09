---
title: "[알고리즘] 위상정렬(Topological Ordering) 참고 코드"
date: 2020-09-09T15:34:30-04:00
classes: wide
categories:
  - Algorithm Theory
tags:
  - 위상정렬
---

위상정렬은 **싸이클이 없는 방향그래프(DAG)** 에서 그래프를 순회하는 방법 중 하나이다. 어떤 일을 먼저 해야 다른 일을 할 수 있는 (전후관계가 있는) 일들의 수행 순서와 같은 것들을 계산할 수 있다. **BFS** 와 상당히 유사한 방법으로 구현할 수 있다.

https://www.acmicpc.net/problem/2252

```java
package 위상정렬.줄세우기;
// https://www.acmicpc.net/problem/2252
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] strs = br.readLine().split(" ");
        int n = Integer.parseInt(strs[0]);
        int m = Integer.parseInt(strs[1]);
        
        ArrayList<Integer>[] arr = (ArrayList<Integer>[]) new ArrayList[n + 1];
        for (int i = 1; i < arr.length; i++) {
            arr[i] = new ArrayList<Integer>();
        }
        int[] indegree = new int[n + 1];
        
        for (int i = 0; i < m; i++) {
            String[] nums = br.readLine().split(" ");
            int a = Integer.parseInt(nums[0]);
            int b = Integer.parseInt(nums[1]);
            
            indegree[b]++;
            arr[a].add(b);
        }
        
        Queue<Integer> q = new LinkedList<Integer>();
        for (int i= 1; i <= n; i++) {
            if (indegree[i] == 0) {
                q.offer(i);
            }
        }
        
        
        while(!q.isEmpty()) {
            int cur = q.poll();
            System.out.printf("%d ", cur);
            
            for (int i = 0; i < arr[cur].size(); i++) {
                int next = arr[cur].get(i);
                if (--indegree[next] == 0) {
                    q.offer(next);
                }
            }
        }
    }
}
```

indegree가 0인 여러 노드가 있을 때 어느 것부터 출력해야 하는지에 대한 순서가 정해져 있다면 일반적인 **Queue** 대신에 **PriorityQueue** 를 사용해야 한다. `java.util` 패키지에 정의되어 있는 **PriorityQueue** 클래스는 **minHeap** 으로 구현되어 있다.

https://www.acmicpc.net/problem/1766

```java
package 위상정렬.문제집;
// https://www.acmicpc.net/problem/1766
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.PriorityQueue;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] strs = br.readLine().split(" ");
        
        int n = Integer.parseInt(strs[0]);
        int m = Integer.parseInt(strs[1]);
        
        ArrayList<Integer>[] arr = (ArrayList<Integer>[])new ArrayList[n + 1];
        for (int i = 1; i <= n; i++) {
            arr[i] = new ArrayList<Integer>();
        }
        int[] indegree = new int[n + 1];
        
        for (int i = 0; i < m; ++i) {
            String[] nodes = br.readLine().split(" ");
            int prev = Integer.parseInt(nodes[0]);
            int next = Integer.parseInt(nodes[1]);
            
            indegree[next]++;
            arr[prev].add(next);
        }
        
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int i = 1; i <= n; i++) {
            if (indegree[i] == 0) {
                pq.add(i);
            }
        }
        
        while(!pq.isEmpty()) {
            int cur = pq.poll();
            System.out.printf("%d ", cur);
            
            for (int i = 0; i < arr[cur].size(); i++) {
                int next = arr[cur].get(i);
                
                if (--indegree[next] == 0) {
                    pq.offer(next);
                }
            }
        }
    }
}
```

노드에 일하는 시간처럼 일종의 가중치가 있는 경우 위상정렬을 변형해서 해결할 수 있다.

https://www.acmicpc.net/problem/2056

```java
package 위상정렬.작업;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

public class Main {
    public static void main(String[] args) throws NumberFormatException, IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        
        int[] indegree = new int[n + 1];
        int[] workTimes = new int[n + 1];
        int[] completeTimes = new int[n + 1];
        int ans = 0;
        
        ArrayList<Integer>[] arr = (ArrayList<Integer>[]) new ArrayList[n + 1]; 
        for (int i = 1; i <= n; i++) {
            arr[i] = new ArrayList<Integer>();
        }
        
        for (int i = 1; i <= n ; i++) {
            String[] words = br.readLine().split(" ");
            workTimes[i] = Integer.parseInt(words[0]);
            indegree[i] = Integer.parseInt(words[1]);
            
            for (int j = 0; j < indegree[i]; j++) {
                int prev = Integer.parseInt(words[2 + j]);
                arr[prev].add(i);
            }
        }
        
        Queue<Integer> q = new LinkedList<>();
        
        for (int i = 1; i <= n; i++) {
            if (indegree[i] == 0) {
                completeTimes[i] = workTimes[i];
                if (ans < completeTimes[i]) ans = completeTimes[i];
                q.offer(i);
            }
        }
        
        while(!q.isEmpty()) {
            int cur = q.poll();
            
            for (int i = 0; i < arr[cur].size(); i++) {
                int next = arr[cur].get(i);
                
                if (completeTimes[next] < completeTimes[cur] + workTimes[next]) {
                    completeTimes[next] = completeTimes[cur] + workTimes[next];
                    
                }
                
                if (--indegree[next] == 0) {
                    q.offer(next);
                    if (ans < completeTimes[next]) {
                        ans = completeTimes[next];
                    }
                }
            }
        }
        
        System.out.println(ans);
    }
}
```
