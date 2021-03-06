---
layout: post
title:  "자료구조 특징"
categories: [Class, Algorithm]
---

### Array
- 연속된 index로 배열을 관리한다.
- value에 해당하는 index값을 안다면 O(1)의 시간으로 데이터를 찾을 수 있다.
- 삽입과 삭제시에는 index 뒤에 있는 데이터들을 뒤로 한칸씩 밀거나 당겨줘야하므로 O(n)의 시간이 걸린다.
- 중간 index에서의 삽입 삭제가 빈번하게 일어나지 않을 때 사용하기 좋다.
- 선언시에 설정한 배열의 크기를 넘을 수 없다. 다시 생성해서 해당 배열을 복사해야한다.

### ArrayList
- Array와 같은 특징을 갖고 있다.
- 선언시에 배열의 크기를 설정할 수 있지만, 설정하지 않고도 사용 가능하다.
- 정해진 배열의 크기를 초과한다면 알아서 현재 배열의 크기/2만큼이 늘어난 배열을 생성하고, 배열을 복사한다.


### Linked List
- 데이터 하나에는 value와 다음 데이터를 가리키는 주소값이 저장되어있다.
- index로 관리되지 않기 때문에 탐색을 위해서는 처음 데이터부터 마지막 데이터까지 순차적으로 탐색해야한다.
- 삽입시에는 이전 데이터와 자신을, 자신과 다음데이터를 연결하여 리스트를 형성한다.
- 삭제시에는 이전 데이터와 다음데이터를 연결하고 자신을 지우면서 리스트를 형성한다.

### Stack
- First In Last Out이라는 특성을 갖고 있는 자료구조이다.
- 자바에서 기본적으로 제공하는 Stack은 Vector를 활용해 구현되어있다.
- push, pop, peek등의 메소드를 통해서 데이터로 접근하며, 모든 연산은 top에서 처리된다.
- 해당 연산 모두 O(1)에 수행할 수 있지만, 가장 밑의 데이터를 확인하기 위해서는 모든 데이터를 빼야한다.

### Queue
- First In First Out이라는 특성을 갖고 있는 자료구조이다.
- 자바에서 기본적으로 제공하는 Queue는 LinkedList를 활용해 구현되어있다.
- add, poll 등의 메소드를 활용해 데이터로 접근한다.
- add는 rear, poll은 front에서 처리된다.
- Deque는 삽입과 삭제를 front, rear에서 모두 할 수 있는 자료구조이다.

### Hash Table
- key-value의 쌍으로 이루어진 데이터를 구성하는 자료구조이다.
- key값은 중복을 허용하지 않고, 이를 위해 hashcode를 사용해 indexing을 하게된다.
  - 하지만 hashcode도 같은 서로다른 데이터가 있을 경우에는 중복되는 index에 Linkded List를 사용해 데이터를 저장한다.
- 탐색을 위해서는 기본적으로 O(1)의 시간이 걸리지만, 위의 상황에 의해 예측되는 최악의 경우(모든 데이터의 key값이 같은 경우)에는 O(n)의 시간이 걸린다.

### Tree
- Root 노드로부터 시작해서 Leef 노드까지 이어지는 그래프형 자료구조이다.
- 부모와 자식이라는 특성으로 이루어지는 계층적 자료구조이다.
- 탐색하는 방법은 세 가지가 있다.
  - 전위순회: root -> left -> right
  - 중위순회: left -> root -> right
  - 후위순회: left -> right -> root
- 편향되지 않는 균등한 BST에서는 탐색에 O(logn), 편향트리에서는 O(n)이 걸린다.

### Heap
- Tree의 구조를 활용해서 만든 자료구조로 반정렬된 상태를 유지한다.
- MaxHeap과 MinHeap이 있다.
  - Maxheap: 루트노드가 가장 큰 데이터를 갖는다.
  - MinHeap: 루트노드가 가장 작은 데이터를 갖는다.
- 위의 특성을 유지하기 위해 삽입과 삭제시에 Heapify를 진행한다.
  - 삭제는 항상 루트노드에서 이루어지고, 가장 마지막에 있는 데이터를 루트노드에 옮겨와서 Heapify과정을 통해 알맞은 위치에 다시 저장된다.
  - 삽입은 가장 마지막 위치에 데이터를 넣고, 부모 노드와 비교하면서 알맞은 위치에 저장하게된다.
- 이러한 특성 때문에 최솟값, 최댓값을 찾을때 많이 사용한다.(우선순위 큐)

### Trie
- Tree의 구조를 활용해 문자열 탐색을 보다 효율적으로 하기 위해 만들어진 자료구조이다.
- 각 문자열을 이루는 한글자마다 노드를 생성하고, 뒤에 있는 글자는 앞에 있는 글자의 자식 노드가된다.
- 해당 구조를 유지하며 데이터를 넣어주게 되고, 트리의 구조로 문자열이 저장된다.