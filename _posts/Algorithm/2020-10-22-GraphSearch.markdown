---
layout: post
title:  "그래프 탐색 알고리즘"
categories: [Class, Algorithm]
---

## 그래프 탐색 알고리즘
### 다익스트라 알고리즘
- 기존에 알고 있던 최단거리를 갱신하는 방법으로 최단거리를 계산한다.
- 두 정점 사이의 최단 거리를 구하는 알고리즘이다.
- 만약 len의 값이 MAX_VALUE이면 접근할 수 없는 노드이다.
- 우선순위 큐를 활용해 구현하며 가중치가 낮은 것이 우선순위가 되도록 한다. `Comparable<node> 구현`
- 출발지 노드를 queue에 넣는다. `queue.add(new node(1, 0))`
- 해당 노드에서 갈 수 있고, 기존 거리보다 단축시킬 수 있는 경우 거리를 갱신하고 queue에 삽입한다.
- 가중치에 음수가 있는 경우 사용할 수 없다.
  + 다익스트라 알고리즘의 핵심은 정점을 지날 수록 가중치가 증가하는 것이다.
  + 하지만 음수가 있다면 이후의 가중치가 더 작을 수 있고, 이는 위의 핵심에 위배되는 사항이다.
- 시간복잡도 O(ElogV)(우선순위큐와 리스트 사용할 경우)
```java
if(len[temp.num] + next.weight < len[next.num]){
       // 최단 경로를 갱신하고 next노드를 탐색 대상에 추가한다.
       len[next.num] = len[temp.num] + next.weight;
       queue.add(new node(next.num , len[next.num]));
}
```
- 이전에 queue에 넣었던 최단거리가 아닌 것이 실행되는 것을 방지하기 위해 조건문을 형성한다.
```java
if(temp.weight != len[temp.num])
       continue;
```
- 위 과정을 반복하며 모든 노드를 파악하고, 최단거리를 찾는다.
- 목적지까지의 최단 거리는 len배열에 저장되어 있다.
```java
public class 다익스트라 {
    static class node implements Comparable<node>{
        int num;
        int weight;
        public node(int num, int weight) {
            this.num = num;
            this.weight = weight;
        }
        @Override
        public int compareTo(node o) {
            return this.weight-o.weight;
        }
    }

    public static void main(String[] args) {
        // u->v 가중치 w, 1번노드에서 시작
        // 정점의 수=5
        int num = 5;
        String[] data = {"5 1 1",
                "1 2 2",
                "1 3 3",
                "2 3 4",
                "2 4 5",
                "3 4 6"};
        // list를 통해 간선을 표시한다.
        ArrayList<ArrayList<node>> arr= new ArrayList<>();
        for(int i=0; i<=num; i++){
            arr.add(new ArrayList<>());
        }
        // list.get(u)에 v와 w를 추가하며 연결관계를 만든다.
        for(int i=0; i<data.length; i++){
            String[] temp = data[i].split(" ");
            int u = Integer.parseInt(temp[0]);
            int v = Integer.parseInt(temp[1]);
            int w = Integer.parseInt(temp[2]);
            arr.get(u).add(new node(v,w));
        }
        // 우선순위 큐를 사용하며 1번부터 탐색을 시작한다.
        // 우선순위 큐를 통해 현재 갈 수 있는 노드 중 가중치가 가장 작은 노드를 먼저 탐색한다.
        PriorityQueue<node> queue = new PriorityQueue<>();
        queue.add(new node(1,0));
        // 전체 거리를 큰 수로 초기화 해준다.
        int[] len = new int[data.length];
        for (int i = 0; i < len.length; i++) {
            len[i] = Integer.MAX_VALUE;
        }
        len[1] = 0;
        while(!queue.isEmpty()){
            node temp = queue.poll();
            // len에 있는 최단거리와 현재의 가중치가 다른 경우
            // 다른 경로를 통해 최단거리가 업데이트 되었으므로 쓸모 없는 경로다.
            if(temp.weight != len[temp.num])
                continue;
            for(node next : arr.get(temp.num)){
                // 현재까지 temp에 도달하는 거리보다 갱신된 거리가 더 짧은 경우
                if(len[temp.num] + next.weight < len[next.num]){
                    // 최단 경로를 갱신하고 next노드를 탐색 대상에 추가한다.
                    len[next.num] = len[temp.num] + next.weight;
                    queue.add(new node(next.num , len[next.num]));
                }
            }
        }
        System.out.println(Arrays.toString(len));
    }
}
```

### 프림 알고리즘
- 최소 신장 트리(MST)를 만들때 주로 사용하는 알고리즘이다.
- 모든 정점을 연결하는 최소 비용을 계산하는 알고리즘이다.
- 모든 간선을 대상으로 싸이클이 만들어지지 않고, 가중치가 가장 작은 간선을 선택해 그래프를 형성한다.
- 우선순위 큐를 사용하며 간선의 가중치가 작은 것이 우선순위가 된다.
- 한번 방문한 노드의 거리는 0으로 바꿔주고 중복과 싸이클이 생기는 것을 막는다.
- `from`배열을 통해 i번째 노드가 어디와 연결되어있는지 판단한다.
- `len`배열을 통해 현재 접근 가능한 간선의 가중치를 파악한다. 이때 이미 접근한 노드까지의 간선은 0으로 만들어 중복 탐색을 막는다.
```java
public class 프림 {
    static class node implements Comparable<node>{
        int num;
        int weight;
        public node(int num, int weight) {
            this.num = num;
            this.weight = weight;
        }
        @Override
        public int compareTo(node o) {
            return this.weight - o.weight;
        }
    }
    public static void main(String[] args) {
        String[] data = {"5 1 1",
                "1 2 2",
                "1 3 3",
                "2 3 4",
                "2 4 5",
                "3 4 6"};
        int v = 5;
        int e = data.length;
        ArrayList<ArrayList<node>> arr = new ArrayList<>();
        for(int i=0; i<=v; i++){
            arr.add(new ArrayList<>());
        }
        for(int i=0; i<e; i++){
            String[] temp = data[i].split(" ");
            int v1 = Integer.parseInt(temp[0]);
            int v2 = Integer.parseInt(temp[1]);
            int w = Integer.parseInt(temp[2]);
            arr.get(v1).add(new node(v2, w));
            arr.get(v2).add(new node(v1, w));
        }
        // i번째 노드가 어디와 연결되는 것인지 정보 저장
        int[] from = new int[v+1];
        // 탐색할 때 가장 가중치가 작은 간선을 찾을 때 활용
        int[] dist = new int[v+1];
        for(int i=1; i<=v; i++){
            dist[i] = Integer.MAX_VALUE;
            from[i] = 0;
        }
        from[1] = 1;
        dist[1] = 0;
        PriorityQueue<node> queue = new PriorityQueue<>();
        queue.add(new node(1,0));
        while(!queue.isEmpty()){
            node temp = queue.poll();
            // temp의 weight가 dist의 값과 다르다면 최단거리 갱신 전의 데이터이므로 continue한다.
            if(temp.weight != dist[temp.num])
                continue;
            dist[temp.num] = 0;
            for(node next : arr.get(temp.num)){
                if(dist[next.num] > next.weight){
                    dist[next.num] = next.weight;
                    from[next.num] = temp.num;
                    queue.add(new node(next.num, dist[next.num]));
                }
            }
        }
        System.out.println(Arrays.toString(from));
        System.out.println(Arrays.toString(dist));
    }
}
```

### 플로이드 와샬 알고리즘
- 모든 정점에서 모든 정점까지의 거리를 알 수 있다.
- 시간 복잡도가 O(n^3)이므로 범위가 큰 문제에서는 사용할 수 없다.
- 모든 정점에서 탐색을 한다는 것이 차이점이며, 중간 간선을 통해 최단거리가 되는지 모든 경우에서 탐색한다. `map[i][j] > map[i][k] + map[j][k]`
- 정점의 수에 비해 간선의 수가 매우 많다면 다익스트라 알고리즘 보다 빠를 수 있다.
- 시간복잡도 : O(V^3)
```java
public class 플로이드 {
    public static void main(String[] args) {
        int n = 5;
        String[] data = {"5 1 1",
                "1 2 2",
                "1 3 3",
                "2 3 4",
                "2 4 5",
                "3 4 6"};
        int[][] map = new int[n+1][n+1];
        for(int i=1; i<=n; i++){
            for(int j=1; j<=n; j++){
                map[i][j] = 1000000;
            }
        }
        for(int i=0; i<data.length; i++){
            String[] temp = data[i].split(" ");
            int v1 = Integer.parseInt(temp[0]);
            int v2 = Integer.parseInt(temp[1]);
            int w = Integer.parseInt(temp[2]);
            map[v1][v2] = w;
            map[v2][v1] = w;
        }
        for(int i=1; i<=n; i++){
            for(int j=1; j<=n; j++){
                for(int k=1; k<=n; k++){
                    if(i==j)
                        continue;
                    if(map[i][j] > map[i][k] + map[j][k]){
                        map[i][j] = map[i][k] + map[j][k];
                    }
                }
            }
        }
        for(int i=1; i<=n; i++){
            for(int j=1; j<=n; j++){
                System.out.print(map[i][j] + " ");
            }
            System.out.println();
        }

    }
}
```