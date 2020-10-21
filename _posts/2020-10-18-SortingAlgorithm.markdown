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
[Java link](https://github.com/chundh/algo/blob/master/Baekjoon/src/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EA%B5%AC%ED%98%84/Sort/BoubleSort.java)

### Selection Sort
- 비교하고자 하는 index와 범위내에 가장 작은 원소와 swap한다. 0번째 index부터 하나씩 작은 값으로 채워진다.
- 시간복잡도 : O(n^2)
- [Java link](https://github.com/chundh/algo/blob/master/Baekjoon/src/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EA%B5%AC%ED%98%84/Sort/SelectionSort.java)

### Insertion Sort
- 자신의 앞의 원소와 비교하고, 비교하고자 하는 값을 따로 저장해놓는다. `int temp = arr[i]`
- `arr[j-1] > temp`인 경우 `arr[j] = arr[j-1]`을 반복하며 데이터를 하나씩 뒤로 민다.
- 해당 조건에 만족하지 않는 index에 저장했던 temp를 넣는다. `arr[j] = temp`
- 시간복잡도 : O(n^2)
[Java link](https://github.com/chundh/algo/blob/master/Baekjoon/src/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EA%B5%AC%ED%98%84/Sort/InsertionSort.java)

### Merge Sort
- `Divide and Connquer`를 이용한 정렬방식이다.
- 배열을 원소 하나가 될 때까지 1/2씩 분할한다. 원소하나가 되면 이를 return하고, return된 것을 합칠 때 순서에 맞게 정렬하여 합친다.
- 시간복잡도 : O(nlogn)
[Java link](https://github.com/chundh/algo/blob/master/Baekjoon/src/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EA%B5%AC%ED%98%84/Sort/MergeSort.java)

### Quick Sort
- 정렬 기법중 가장 빠르다고해서 붙여진 이름이지만 최악의 경우에는 O(n^2)의 효율을 보인다.
- `Divide and Conquer`를 이용한 정렬방식이다.
- 임의의 기준인 Pivot을 기준으로 왼쪽에 작은 수, 오른쪽에 큰 수를 배치하고 이들을 다시 분할한다.
- 분할된 배열에서 Pivot을 기준으로 좌,우로 정렬을 반복한다.
- Worst Case : pivot이 가장 크거나 작은 값으로 모든 분할 과정에서 최악의 횟수로 비교를 할 때 최악의 경우이다.
  * Ex) 오름차순 정렬이 필요할 때 내림차순으로 정렬된 데이터.
  * Pivot을 랜덤으로 지정한다면 악의적인 Worst Case를 막을 수 있다.
- Best Case : 데이터가 반씩 분할이 이루어지는 경우
- 시간복잡도 : O(nlogn)
[Java link](https://github.com/chundh/algo/blob/master/Baekjoon/src/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EA%B5%AC%ED%98%84/Sort/QuickSort.java)