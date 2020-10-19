---
layout: post
title:  "Sorting Algorithm"
categories: [Class, Algorithm]
---

## Sorting Algorithm (정렬 알고리즘)
### 종류
- Bubble Sort
- Selection Sort
- Insertion Sort
- Merge Sort
- Quick Sort

### Bubble Sort
- 인접한 두 개의 데이터를 비교하면서 정렬한다. 해당 원소를 맨 끝까지 비교하면서 가장 큰 원소를 맨 끝에, 가장 작은 원소를 맨 앞에 위치한다.
- 시간복잡도 : O(n^2)

### Selection Sort
- 비교하고자 하는 index를 기준으로 모든 원소와 비교 후 위치를 정하여 정렬한다. 매번 데이터를 바꾸지 않고, 위치가 확정되면 바꾼다.
- 시간복잡도 : O(n^2)

### Insertion Sort
- i번째 원소를 정렬해야 할 차례인 경우, 자신의 뒤의 원소와 비교하여 자신이 더 크면 해당 원소와 자리를 바꾼다. 이 과정을 배열의 크기만큼 반복한다.
- 시간복잡도 : O(n^2)

### Merge Sort
- `Divide and Connquer`를 이용한 정렬방식이다.
- 배열을 원소 하나가 될 때까지 1/2씩 분할한다. 원소하나가 되면 이를 return하고, return된 것을 합칠 때 순서에 맞게 정렬하여 합친다.
- 시간복잡도 : O(nlogn)

### Quick Sort
- 정렬 기법중 가장 빠르다고해서 붙여진 이름이지만 최악의 경우에는 O(n^2)의 효율을 보인다.
- `Divide and Conquer`를 이용한 정렬방식이다.
- 임의의 기준인 Pivot을 기준으로 왼쪽에 작은 수, 오른쪽에 큰 수를 배치하고 이들을 다시 분할한다. 원소가 하나가 되면 이들을 return하며 이를 합치면 정렬된 데이터를 얻게 된다.
- 이때 pivot은 다음 분할에 포함시키지 않아야한다.
- Worst Case : pivot이 가장 크거나 작은 값으로 모든 분할 과정에서 최악의 횟수로 비교를 할 때 최악의 경우이다.
  * Ex) 오름차순 정렬이 필요할 때 내림차순으로 정렬된 데이터.
  * Pivot을 랜덤으로 지정한다면 악의적인 Worst Case를 막을 수 있다.
- Best Case : 데이터가 반씩 분할이 이루어지는 경우
- 시간복잡도 : O(nlogn)