### 그리디

### DFS&BFS

### 정렬

선택정렬

삽입정렬

퀵정렬

계수정렬

- 비교

거품정렬

병합정렬

힙정렬

### 이진탐색

### 다이나믹프로그래밍?

### 최단경로

다익스트라

플로이드 워셜

### 기타(그래프)

신장 트리

크루스칼

위상정렬

### 기타

에라토스테네스의 체

투포인터

부록. 힙 자료구조

## **그리디**

그리디 알고리즘(탐욕법)은 현재 상황에서 지금 당자 좋은 것만 고르는 방법 이다.→ 현재의 선택이 나중에 미칠 영향에 대해서는 고려하지 않음

### **그리디 알고리즘의 정당성**

대부분의 그리디 알고리즘 문제에서는 문제풀이를 위한 최소한의 아이디어를 떠올리고 정당한지 검토할 수 있어야 한다.[팁] 기준에 다라 좋은것을 선택하는 알고리즘으로 문제에서 알게 모르게 기준을 제시할 수 도 있음.

DFS와 BFS는 대표적인 그래프 탐색 알고리즘이다. 여기서 탐색이란 원하는 데이터를 찾는 과정을 말한다.

## **DFS (Depth-First Search)**

### **[정의]**

- DFS는 **깊이 우선 탐색**이라고도 부르며 그래프에서 **깊은 부분을 우선적**으로 탐색하는 알고리즘이다.
- DFS는 **스택** 자료구조(혹은 **재귀** 함수)를 이용하며, 구체적인 동작 과정은 다음과 같다.
1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다
2. 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리한다
3. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다 더 이상 2번의 과정을 수행할 수 없을 때까지 반복한다 모든 경로 방문시 적합
- 시간 복잡도
    - 인접 행렬: O(v^2)
    - 인접 리스트: O(V+E)

### **[예제]**

`# DFS 함수 정의
def dfs(graph, v, visited):
    # 현재 노드를 방문 처리
    visited[v] = True
    print(v, end=' ')
    # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)

# 각 노드가 연결된 정보를 리스트 자료형으로 표현(2차원 리스트)
graph = [
  [],
  [2, 3, 8],
  [1, 7],
  [1, 4, 5],
  [3, 5],
  [3, 4],
  [7],
  [2, 6, 8],
  [1, 7]
]

# 각 노드가 방문된 정보를 리스트 자료형으로 표현(1차원 리스트)
visited = [False] * 9

# 정의된 DFS 함수 호출
dfs(graph, 1, visited)`

### **[결과]**

`1 2 7 6 8 3 4 5`

## **BFS (Breadth-First Search)**

### **[정의]**

- BFS는 **너비 우선 탐색**이라고도 부르며, 그래프에서 **가까운 노드부터 우선적**으로 탐색하는 알고리즘이다.
- BFS는 **큐** 자료구조를 이용하며, 구체적인 동작 과정은 다음과 같다.
1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 합니다
2. 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리한다 더 이상 2번의 과정을 수행할 수 없을 때까지 반복한다 +최소비용에 적합하다.
- 시간 복잡도
    - 인접 행렬: O(V^2)
    - 인접 리스트 O(V+E)

### **[예제]**

`from collections import deque

# BFS 함수 정의
def bfs(graph, start, visited):
    # 큐(Queue) 구현을 위해 deque 라이브러리 사용
    queue = deque([start])
    # 현재 노드를 방문 처리
    visited[start] = True
    # 큐가 빌 때까지 반복
    while queue:
        # 큐에서 하나의 원소를 뽑아 출력
        v = queue.popleft()
        print(v, end=' ')
        # 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i] = True

# 각 노드가 연결된 정보를 리스트 자료형으로 표현(2차원 리스트)
graph = [
  [],
  [2, 3, 8],
  [1, 7],
  [1, 4, 5],
  [3, 5],
  [3, 4],
  [7],
  [2, 6, 8],
  [1, 7]
]

# 각 노드가 방문된 정보를 리스트 자료형으로 표현(1차원 리스트)
visited = [False] * 9

# 정의된 BFS 함수 호출
bfs(graph, 1, visited)`

### **[결과]**

`1 2 3 8 7 4 5 6`

### **참고 서적**

이것이 취업을 위한 코딩 테스트다

## 정렬

- **정렬**이란 순업없이 배열된 자료를 오름차순이나 내림차순으로 재배열하는것이다.
- 종류: 선택 정렬, 삽입 정렬, 버블 정렬, 퀵 정렬, 힙 정렬, 기수 정렬

---

## **선택 정렬(Selection Sort)**

### **[정의]**

- 처리되지 않은 데이터 중에서 **가장 작은 데이터를 선택해 맨 앞에 있는 데이터와 바꾸는 것을 반족**한다.
- 현재 위치에 저장될 값의 크기가 작냐, 크냐에 따라서 최소 선택 정렬(오름차순 정렬)과 최대 선택 정렬(내림차순 정렬)로 나뉜다.

### **[예제]**

`array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(len(array)):
    min_index = i # 가장 작은 원소의 인덱스
    for j in range(i + 1, len(array)):
        if array[min_index] > array[j]:
            min_index = j
    array[i], array[min_index] = array[min_index], array[i] # 스와프

print(array)`

### **[결과]**

`[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]`

### **[시간복잡도]**

O(N^2) 이융 : 선택 정렬은 N번 만큼 가장 작은 수를 찾아서 맨 앞으로 보내야 한다. -> N + (N-1) + (N-2) + ... + 2 => (𝑁² + 𝑁 - 2) / 2

### **[장점]**

- 알고리즘이 단순하다.
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다.

### **[단점]**

- 시간 복잡도가 O(N^2)이므로 비효율적이다.
- 불안정 정렬(Unstable Sort)이다. *불안정 정렬이란?* 정렬 후에 원래의 순서가 유지된다는 보장을 할 수 없는 정렬

## **삽입정렬(Insertion Sort)**

### **[정의]**

- 처리되지 않은 데이터를 하나씩 골라 적절한 위치에 삽입한다.
- 선택 정렬에 비해 구현 난이도가 높은 편이지만, 일반적으로 더 효율적으로 동작한다.

### **[로직]**

[Step 0] 첫 번째 데이터는 그 자체로 정렬이 되어 있다고 판단하고, 두 번째 데이터가 어떤 위치로 들어갈지 판단한다. 첫번째의 왼쪽으로 들어가거나 오른쪽으로 들어가거나 두 경우만 존재한다. [Step 1] 세 번째 데이터가 어떤 위치(1번째의 앞 혹은 뒤 2번째의 뒤)로 들어갈지 판단한다. 위 과정을 반복한다.

### **[예제]**

`array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(1, len(array)):
    for j in range(i, 0, -1): # 인덱스 i부터 1까지 1씩 감소하며 반복하는 문법
        if array[j] < array[j - 1]: # 한 칸씩 왼쪽으로 이동
            array[j], array[j - 1] = array[j - 1], array[j]
        else: # 자기보다 작은 데이터를 만나면 그 위치에서 멈춤
            break

print(array)`

### **[결과]**

`[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]`

### **[시간복잡도]**

O(N²)

- 현재 리스트의 데이터가 거의 정렬되어 있는 상태라면 매우 빠르게 동작한다.
- 최선의 경우 O(N)의 시간 복잡도를 가진다.
- 모두 정렬되어 있을 경우에는 한번씩만 비교하기에 O(N)

### **[공간복잡도]**

O(N)

- 주어진 배열안에서 교환해 정렬하기 때문에

### **[장점]**

- 알고리즘이 단순하다.
- 대부분의 원소가 이미 정렬되어 있는 경우, 매우 효율적일 수 있다.
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다.
- 선택 정렬이나 버블 정렬에 비하여 상대적으로 빠르다.

### **[단점]**

- 비교할 수가 많고 크기가 클 경우에 적합하지 않다.(배열의 길이가 길어질수록 비효율적)
- 평균과 최악의 시간 복잡도가 O(N^2)이므로 비효율적이다.

## **Quick Sort**

### **[정의]**

- 퀵 정렬은 분할 정복 방법을 통해 주어진 배열을 정렬한다. -- 분할 정복이란 문제를 작은 2개의 문제로 분리하고 각각 해결한 다음에 결과를 모아 원래의 문제를 해결하는 전략이다.
- 불안정 정렬에 속하며, 다른 원소와의 비교만으로 정렬을 수행하는 비교 정렬에 속한다. 또한, Merge Sort와 달리 Quick Sort는 배열을 비균등하게 분할한다.
- 일반적인 상황에서 가장 많이 사용되는 정렬 알고리즘 중 하나이며 병합 정렬과 더불어 대부분의 프로그래밍 언어의 정렬 라이브러리의 근간이 되는 알고리즘이다
- 가장 기본적인 퀵 정렬은 **첫 번째** 데이터를 **기준 데이터(Pivot)**로 설정한다

### **[로직]**

1. 배열 가운데서 하나의 원소를 고른다. 이렇게 고른 원소는 피벗(pivot)이라고 한다.
2. 피벗 앞에는 피벗보다 값이 작은 모든 원소들이 오고, 피벗 뒤에는 피벗보다 값이 큰 모든 원소들이 오도록 피벗을 기준으로 배열을 둘로 나눈다. 이렇게 배열을 둘로 나누는 것을 분할(Divide)이라고 한다. 분할을 마친 뒤에 피벗은 더 이상 움직이지 않는다.
3. 분할 된 두 개의 작은 배열에 대해 재귀적으로 이 과정을 반복한다.

### **[예제]**

`array = [5, 7, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array):
    # 리스트가 하나 이하의 원소만을 담고 있다면 종료
    if len(array) <= 1:
        return array

    pivot = array[0] # 피벗은 첫 번째 원소
    tail = array[1:] # 피벗을 제외한 리스트

    left_side = [x for x in tail if x <= pivot] # 분할된 왼쪽 부분
    right_side = [x for x in tail if x > pivot] # 분할된 오른쪽 부분

    # 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬을 수행하고, 전체 리스트를 반환
    return quick_sort(left_side) + [pivot] + quick_sort(right_side)

print(quick_sort(array))`

### **[결과]**

`[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]`

### **[시간복잡도]**

평균: O(NlogN) 최악: O(N²)

### **[공간복잡도]**

O(N)

### **[장점]**

- 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환할 뿐만 아니라, 한번 결정된 피벗들이 추후 연산에서 제외되는 특성 때문에, 시간 복잡도가 O(N logN)을 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.
- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다.

### **[단점]**

- 불안정 정렬이다.
- 정렬된 배열에 대해서는 Quick Sort의 불균형 분할에 의해 오히려 수행 시간이 더 많이 걸린다.

<번외> 안정정렬 VS 불안정정렬

안정정렬: 중복된 값의 경우 입력 순서와 동일하게 유지해서 정렬 하는 것을 말합니다.

→ ex)삽입, 버블,병합

불안정 정렬: 중복된 값의 경우 입력 순서를 무작위로 뒤섞은 상태에서 정렬 하는 것을 말합니다.

→ ex) 선택.퀵,힙,인트로

## **Counting Sort(계수정렬)**

### **[정의]**

- 특정한 조건이 부합할 때만 사용할 수 있지만 **매우 빠르게 동작**하는 정렬 알고리즘이다
- 계수 정렬은 데이터의 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때 사용 가능하다.

### **[로직]**

**[Step 0]** 가장 작은 데이터부터 가장 큰 데이터까지의 범위가 모두 담길 수 있도록 리스트를 생성한다. **[Step 1]** 데이터를 하나씩 확인하며 데이터의 값과 동일한 인덱스의 데이터를 1씩 증가시킨다. **[Step N]** 결과적으로 최종 리스트에는 각 데이터가 몇 번씩 등장했는지 그 횟수가 기록된다.

- 결과를 확인할 때는 리스트의 첫 번째 데이터부터 하나씩 그 값만큼 반복하여 인덱스를 출력한다.

### **[예제]**

`# 모든 원소의 값이 0보다 크거나 같다고 가정
array = [7, 5, 9, 0, 3, 1, 6, 2, 9, 1, 4, 8, 0, 5, 2]
# 모든 범위를 포함하는 리스트 선언 (모든 값은 0으로 초기화)
count = [0] * (max(array) + 1)

for i in range(len(array)):
    count[array[i]] += 1 # 각 데이터에 해당하는 인덱스의 값 증가

for i in range(len(count)): # 리스트에 기록된 정렬 정보 확인
    for j in range(count[i]):
        print(i, end=' ') # 띄어쓰기를 구분으로 등장한 횟수만큼 인덱스 출력`

### **[결과]**

`0 0 1 1 2 2 3 4 5 5 6 7 8 9 9`

### **[시간복잡도]**

O(N + K)

- 데이터의 개수가 𝑁, 데이터(양수) 중 최댓값이 𝐾일 때 최악의 경우에도 수행 시간 O(N + K) 를 보장한다

### **[공간복잡도]**

O(N + K)

### **[장점]**

- 계수 정렬은 **동일한 값을 가지는 데이터가 여러개 등장**할 때 효과적으로 사용할 수 있다

### **[단점]**

- 계수 정렬은 경우에 따라 심각한 비효율성을 초래할 수 있다 EX) 데이터가 0과 999,999로 단 2개만 존재하는 경우

[정렬 알고리즘 비교](https://www.notion.so/de431e4a2902402bb4d3fc5e16cf7d7d)

## **Bubble Sort**

### **[정의]**

- 인접한 2개의 원소를 비교해 크기가 순서대로 되어 있지 않으면 서로 교환한다.

### **[로직]**

[step 0] n 번째 원소와 n+1번째 원소를 비교하여(n은 1부터 시작) 조건에 맞지 않으면 서로 교환한다. [step 1] 한 회차가 끝나면 맨 뒤의 원소(=졍렬된 원소)를 제외하고 step0을 반복한다.

### **[예제]**

`def bubble_sort(arr):
    end = len(arr) - 1
    while end > 0:
        last_swap = 0
        for i in range(end):
            if arr[i] > arr[i + 1]:
                arr[i], arr[i + 1] = arr[i + 1], arr[i]
                last_swap = i
        end = last_swap`

### **[시간복잡도]**

O(N^2) 버블 정렬은 정렬이 되어있건, 안되어있건 2개의 원소를 비교하기 때문에 최악의 경우, 최선의 경우, 평균의 경우 모두 시간 복잡도가 O(N^2)으로 동일하다.

### **[공간복잡도]**

O(N)

### **[장점]**

- 구현이 간단하고 소스코드가 직관적이다.
- 정렬하고자 하는 배열 안에서 정렬하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다.
- 안정 정렬이다.

### **[단점]**

- 시간 복잡도가 최악, 최선, 평균 모두 O(N^2)이므로 비효율적이다.
- 순서에 맞지 않은 요소를 인접한 요소와 교환한다.
- 하나의 요소가 가장 왼쪽에서 가장 오른쪽으로 이동하기 위해서는 배열에서 모든 다른 요소들과 교환되어야 한다.
- 일반적으로 자료의 교환 작업(SWAP)이 자료의 이동 작업(MOVE)보다 더 복잡하기 때문에 버블 정렬은 단순성에도 불구하고 거의 쓰이지 않는다.

## **병합 정렬(Merge Sort)**

데이터를 쪼갠 후 둘씩 크기를 비교해 정렬 후 합치는 과정을 더이상 합칠 배열이 없을때 까지 반복

! 데이터 개수가 홀수일 시 왼쪽 배열에 요소 하나를 더 포함시킴

### 특징

합병 정렬이라고도 부르며, 분할 정복 방법을 통해 구현한다.

**분할 정복 알고리즘: 큰 문제를 작은 문제 단위로 쪼개면서 해결해나가는 방식

빠른정렬로 분류 되며, 안정정렬이다.

### 예제

```
def merge_sort(list):
    if len(list) <= 1:
        return list
//쪼개기
    mid = len(list) // 2
    leftList = list[:mid]
    rightList = list[mid:]
//재귀
    leftList = merge_sort(leftList)
    rightList = merge_sort(rightList)
    return merge(leftList, rightList)

def merge(left, right):
    result = []
    while len(left) > 0 or len(right) > 0:
        if len(left) > 0 and len(right) > 0:
            if left[0] <= right[0]:
                result.append(left[0])
                left = left[1:]
            else:
                result.append(right[0])
                right = right[1:]
        elif len(left) > 0:
            result.append(left[0])
            left = left[1:]
        elif len(right) > 0:
            result.append(right[0])
            right = right[1:]
    return result
```

### **시간복잡도**

- 평균 : O(N logN)
- 최악 : O(N logN)
- 최선 : O(N logN)

### **장점**

- 데이터의 분포에 영향을 덜 받는다. 즉, 입력 데이터가 무엇이든 간에 정렬되는 시간은 동일하다. -> O(N logN)
- 크기가 큰 레코드를 정렬한 경우, LinkedList를 사용한다면 병합 정렬은 퀵 정렬을 포함한 다른 어떤 정렬 방법보다 효율적이다.
- 안정 정렬에 속한다.

### **단점**

- 레코드를 배열로 구성한다면, 임시 배열이 필요하다.
    - 메모리 낭비를 초래한다.
    - 제자리 정렬이 아니다.
- 레코드의 크기가 큰 경우에는 이동 횟수가 많으므로 매우 큰 시간적 낭비를 초래한다.

### 퀵정렬 VS 합병정렬

퀵정렬 : 우선 피벗을 통해 정렬(partition) → 영역을 쪼갬(quickSort)

합병정렬 : 영역을 쪼갤 수 있을 만큼 쪼갬(mergeSort) → 정렬(merge)

## **힙 정렬(Heap Sort)**

완전 이진 트리를 기본으로 하는 힙 자료구조를 이용하여 정렬하는 방법

리스트나 배열을 최소힙이나 최대힙으로 바꾸고 값을 하나씩 뽑아내면서 정렬(최대힙 - 오름차순, 최소힙 - 내림차순)

불안정 정렬

### **로직**

1. 최대 힙을 구성
2. 현재 힙 루트는 가장 큰 값이 존재함. 루트의 값을 마지막 요소와 바꾼 후, 힙의 사이즈 하나 줄임
3. 힙의 사이즈가 1보다 크면 위 과정 반복

[https://camo.githubusercontent.com/0104a65c5df44c342e310a24c1becd08c9596367/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f393939383936343435414434393533303233](https://camo.githubusercontent.com/0104a65c5df44c342e310a24c1becd08c9596367/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f393939383936343435414434393533303233)

루트 노드를 마지막 노드로 대체한다. (11->4) 그리고 다시 최대 힙 구성.

[https://camo.githubusercontent.com/000e4568cdab087691478961e100c8290df3af31/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f393945314144343435414434393533303135](https://camo.githubusercontent.com/000e4568cdab087691478961e100c8290df3af31/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f393945314144343435414434393533303135)

이와 같은 방식으로 최대 값을 하나씩 뽑아내면서 정렬하는 것이 Heap Sort이다.

import heapq

arr = []

heap2 = [10,20,30]

heapq.heapify(heap2)

while heap2:

arr.append(heapq.heappop(heap2))

### **시간 복잡도**

- 평균 : O(N logN)
- 최선 : O(N logN)
- 최악 : O(N logN)

### **힙 소트가 유용할 때**

- 가장 크거나 가장 작은 값을 구할 때
    
    > 최소 힙 or 최대 힙의 루트 값이기 때문에 한번의 힙 구성을 통해 구하는 것이 가능
    > 
- 최대 k 만큼 떨어진 요소들을 정렬할 때
    
    > 삽입정렬보다 더욱 개선된 결과를 얻어낼 수 있음
    > 
    

## 트리정렬

이진탐색트리를 이용하여 정렬하는 방법

정렬할 원소들을 이진탐색트리로 구성하고 운선순회방법을 사용하여 이진탐색트리의 원소들을 순회하여 꺼내면 오름차순 정렬이된다.

### 시간복잡도

O($log_2n$)

(이진탐색트리를구성하는시간으로결정됨)

## 이진탐색

정렬되어 있는 리스트에서 **탐색 범위를 절반씩 좁혀가며 데이터를 탐색**하는 방법

- 이진 탐색은 시작점, 끝점, 중간점을 이용하여 탐색 범위를 설정한다

**순차 탐색: 리스트 안에 있는 특정한 **데이터를 찾기 위해 앞에서부터 데이터를 하나씩 확인**하는 방법

### 시간복잡도

**𝑂(log𝑁)** 

- 단계마다 탐색 범위를 2로 나누는 것과 동일하므로 **연산 횟수는 log₂𝑁에 비례**한다
- 예를 들어 초기 데이터 개수가 32개일 때, 이상적으로 1단계를 거치면 16개가량의 데이터만 남는다
    - 2단계를 거치면 8개가량의 데이터만 남는다
    - 3단계를 거치면 4개가량의 데이터만 남는다
- 다시 말해 이진 탐색은 탐색 범위를 절반씩 줄이며, 시간 복잡도는 **𝑂(log𝑁)** 을 보장한다

### 예제

```

# 이진 탐색 소스코드 구현 (반복문)
def binary_search(array, target,start,end):
whilestart <=end:
mid = (start +end) // 2
        # 찾은 경우 중간점 인덱스 반환
if array[mid] == target:
returnmid# 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
        elif array[mid] > target:
end =mid - 1
        # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
else:
start =mid + 1
returnNone# n(원소의 개수)과 target(찾고자 하는 값)을 입력 받기
n, target =list(map(int,input().split()))
# 전체 원소 입력 받기
array =list(map(int,input().split()))

# 이진 탐색 수행 결과 출력
result = binary_search(array, target, 0, n - 1)
ifresult ==None:
    print("원소가 존재하지 않습니다.")
else:
    print(result + 1)
```

****파라메트릭 서치 (Parametric Search)**

**파라메트릭 서치**란 최적화 문제를 결정 문제('예' 혹은 '아니오')로 바꾸어 해결하는 기법

- 예시: 특정한 조건을 만족하는 가장 알맞은 값을 빠르게 찾는 최적화 문제

일반적으로 코딩 테스트에서 파라메트릭 서치 문제는 **이진 탐색을 이용하여 해결**할 수 있다

## 다이나믹프로그래밍(=동적계획법)

한 가지 문제에 대해, 단 한번만 풀도록 만들어주는 알고리즘(즉, 똑같은 연산 반복 X)

### 사용조건

1. **최적 부분 구조 (Optimal Substructure)**
    - 큰 문제를 작은 문제로 나눌 수 있으며 작은 문제로 나눌 수 있으며 작은 문제의 답을 모아서 큰 문제를 해결할 수 있다
2. **중복되는 부분 문제 (Overlapping Subproblem)**
    - 동일한 작은 문제를 반복적으로 해결해야 한다

### 구현방법

### - 메모이제이션 (Memoization)

- 메모이제이션은 다이나믹 프로그래밍을 구현하는 방법 중 하나이다
- 한 번 계산한 결과를 메모리 공간에 메모하는 기법이다
    - 같은 문제를 다시 호출하면 메모했던 결과를 그대로 가져온다
    - 값을 기록해 놓는다는 점에서 **캐싱(Caching)** 이라고도 한다
    

**탑다운 VS 보텀업**

- 탑다운(메모이제이션) 방식은 **하향식**이라고도 하며 보텀업 방식은 **상향식**이라고도 한다
- 다이나믹 프로그래밍의 전형적인 형태는 보텀업 방식이다
    - 결과 저장용 리스트는 **DP 테이블**이라고 부른다
- 엄밀히 말하면 메모이제이션은 이전에 계산된 결과를 일시적으로 기록해 놓는 넓은 개념을 의미한다
    - 따라서 메모이제이션은 다이나믹 프로그래밍에 국한된 개념은 아니다
    - 한 번 계산된 결과를 담아 놓기만 하고 다이나믹 프로그래밍을 위해 활용하지 않을 수도 있다

### **유클리드 호제법(Euclidean Algorithm)**

2개의 자연수를 입력 받아 최대 공약수를 구하기 위해 2부터 두 자연수 중 작은 자연수까지 모두 나누어보면서 가장 큰 공약수를 구할 수 있다. 하지만, 이 방법으로 문제를 풀면 시간 복잡도는 O(N)이 된다. 나쁜 방법은 아니지만, 보다 효율을 높일 수 있는 방법이 존재하며 **유클리드 호제법이란 알고리즘을 사용하면 시간 복잡도를 O(logN)으로 줄일 수 있다.**

> 호제법이란? 두 수가 서로 상대방 수를 나누어서 결국 원하는 수를 얻는 방법
> 

## (최단경로)

## 다익스트라

가장 짧은 경로를 찾는 알고리즘

- **특정한 노드**에서 출발하여 **다른 모든 노드**로 가는 최단 경로를 계산한다
- 다익스트라 최단 경로 알고리즘은 음의 간선이 없을 때 정상적으로 동작한다
    - 현실 세계의 도로(간선)은 음의 간선으로 표현되지 않습니다
- 다익스트라 최단 경로 알고리즘은 그리디 알고리즘으로 분류된다
    - **매 상황에서 가장 비용이 적은 노드를 선택**해 임의의 과정을 반복한다

### 로직

1. 출발 노드를 설정한다
2. 최단 거리 테이블을 초기화한다
3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택한다
4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신한다
5. 위 과정에서 3번과 4번을 반복한다

### 특징

- 그리디 알고리즘: **매 상황에서 방문하지 않은 가장 비용이 적은 노드를 선택**해 임의의 과정을 반복한다
- 단계를 거치며 **한 번 처리된 노드의 최단 거리는 고정**되어 더 이상 바뀌지 않는다
    - **한 단계당 하나의 노드에 대한 최단 거리를 확실히 찾는 것으로 이해**할 수 있다
- 다익스트라 알고리즘을 수행한 뒤에 테이블에 각 노드까지의 최단 거리 정보가 저장된다

### 구현

- 단계마다 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택하기 위해 **매 단계마다 1차원 테이블의모든 원소를 확인(순차 탐색)**한다

```

import heapq
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[]for iinrange(n + 1)]
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n + 1)

# 모든 간선 정보를 입력받기
for _inrange(m):
    a, b, c =map(int,input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[a].append((b, c))

def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 경로는 0으로 설정하여, 큐에 삽입
    heapq.heappush(q, (0,start))
    distance[start] = 0
while q: # 큐가 비어있지 않다면
        # 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
        dist,now = heapq.heappop(q)
        # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
if distance[now] < dist:
            continue
        # 현재 노드와 연결된 다른 인접한 노드들을 확인
for iin graph[now]:
cost = dist + i[1]
            # 현재 노드를 거쳐서, 다른 노드로 이동하는 거리가 더 짧은 경우
ifcost < distance[i[0]]:
                distance[i[0]] =cost
                heapq.heappush(q, (cost, i[0]))

# 다익스트라 알고리즘을 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for iinrange(1, n + 1):
    # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
if distance[i] == INF:
        print("INFINITY")
    # 도달할 수 있는 경우 거리를 출력
else:
        print(distance[i])
```

### 시간복잡도

O(V^2)

총 O(V)번에 걸쳐서 최단 거리가 가장 짧은 노드를 매번 선형 탐색해야 한다.

힙 자료구조를 이용하는 다익스트라 알고리즘의 시간 복잡도는 O(ElogV) 이다

## 플로이드 워셜

- 모든 노드에서 다른 모든 노드까지의 최단 경로를 모두 계산한다
- 플로이드 워셜(Floyd-Warshall) 알고리즘은 다익스트라 알고리즘과 마찬가지로 단계별로 **거쳐 가는 노드를기준으로 알고리즘을 수행**한다
    - 다만 매 단계마다 방문하지 않은 노드 중에 최단 거리를 갖는 노드를 찾는 과정이 필요하지 않다
- 플로이드 워셜은 2차원 테이블에 최단 거리 정보를 저장한다
- 플로이드 워셜 알고리즘은 다이나믹 프로그래밍 유형에 속한다
- 각 단계마다 **특정한 노드 𝑘를 거쳐 가는 경우를 확인**한다
    - 𝑎에서 𝑏로 가는 최단 거리보다 𝑎에서 𝑘를 거쳐 𝑏로 가는 거리가 더 짧은지 검사한다

### 예제

```

INF =int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수 및 간선의 개수를 입력받기
n =int(input())
m =int(input())
# 2차원 리스트(그래프 표현)를 만들고, 모든 값을 무한으로 초기화
graph = [[INF] * (n + 1)for _inrange(n + 1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for ainrange(1, n + 1):
for binrange(1, n + 1):
if a == b:
            graph[a][b] = 0

# 각 간선에 대한 정보를 입력 받아, 그 값으로 초기화
for _inrange(m):
    # A에서 B로 가는 비용은 C라고 설정
    a, b, c = map(int, input().split())
    graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘을 수행
for kinrange(1, n + 1):
for ainrange(1, n + 1):
for binrange(1, n + 1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행된 결과를 출력
for ainrange(1, n + 1):
for binrange(1, n + 1):
        # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
if graph[a][b] == 1e9:
            print("INFINITY", end=" ")
        # 도달할 수 있는 경우 거리를 출력
else:
            print(graph[a][b], end=" ")
    print()
```

### 시간복잡도

- 노드의 개수가 𝑁개일 때 알고리즘상으로 𝑁번의 단계를 수행한다
    - 각 단계마다 **O(N²)** 의 연산을 통해 현재 노드를 거쳐 가는 모든 경로를 고려한다
- 따라서 플로이드 워셜 알고리즘의 총 시간 복잡도는 **O(N³)** 이다

## 기타(그래프)

## 신장트리

- 그래프에서 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프를 의미한다
    - 모든 노드가 포함되어 서로 연결되면서 사이클이 존재하지 않는다는 조건은 **트리**의 조건이기도 하다

![https://blog.kakaocdn.net/dn/bSzFD7/btqKvQUKTPB/ccvE9PeolK1TWiZgJRAxR1/img.png](https://blog.kakaocdn.net/dn/bSzFD7/btqKvQUKTPB/ccvE9PeolK1TWiZgJRAxR1/img.png)

## 최소 신장 트리

- 최소한의 비용으로 구성되는 신장 트리를 찾아야 할 때 어떻게 해야 할까?
- 예를 들어 N개의 도시가 존재하는 상황에서 두 도시 사이에 도로를 놓아 **전체 도시가 서로 연결**될 수 있게도로를 설치하는 경우를 생각해 보자
    - 두 도시 A,B를 선택했을 때 A에서 B로 이동하는 경로가 반드시 존재하도록 도로를 설치한다

![https://blog.kakaocdn.net/dn/epjClI/btqKvQHcysE/DStzKyRhyJKcF9oaExCNM1/img.png](https://blog.kakaocdn.net/dn/epjClI/btqKvQHcysE/DStzKyRhyJKcF9oaExCNM1/img.png)

## 크루스칼 알고리즘

- 대표적인 **최소 신장 트리 알고리즘**이다
- 그리디 알고리즘으로 분류된다
- 구체적인 동작 과정은 다음과 같다
    1. 간선 데이터를 비용에 따라 **오름차순으로 정렬**한다
    2. 간선을 하나씩 확인하며 한다
        
        현재의 간선이 사이클을 발생시키는지 확인
        
        1. 사이클이 발생하지 않는 경우 최소 신장 트리에 포함시킨다
        2. 사이클이 발생하는 경우 최소 신장 트리에 포함시키지 않는다
    3. 모든 간선에 대하여 2번의 과정을 반복한다

### 예제

```

# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
ifparent[x] != x:
parent[x] = find_parent(parent,parent[x])
returnparent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
if a < b:
parent[b] = a
else:
parent[a] = b

# 노드의 개수와 간선(Union 연산)의 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v + 1) # 부모 테이블 초기화하기

# 모든 간선을 담을 리스트와, 최종 비용을 담을 변수
edges = []
result = 0

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(1, v + 1):
parent[i] = i

# 모든 간선에 대한 정보를 입력 받기
for _ in range(e):
    a, b, cost = map(int, input().split())
    # 비용순으로 정렬하기 위해서 튜플의 첫 번째 원소를 비용으로 설정
    edges.append((cost, a, b))

# 간선을 비용순으로 정렬
edges.sort()

# 간선을 하나씩 확인하며
for edge in edges:
    cost, a, b = edge
    # 사이클이 발생하지 않는 경우에만 집합에 포함
if find_parent(parent, a) != find_parent(parent, b):
        union_parent(parent, a, b)
        result += cost

print(result)
```

### 시간복잡도

- 크루스칼 알고리즘은 간선의 개수가 E개일 때, **O(ElogE)** 의 시간 복잡도를 가진다
- 크루스칼 알고리즘에서 가장 많은 시간을 요구하는 곳은 간선의 정렬을 수행하는 부분이다
    - 표준 라이브러리를 이용해 𝐸개의 데이터를 정렬하기 위한 시간 복잡도는  이다
        
        O(ElogE)
        

---

### ** 위상 정렬

- 사이클이 없는 방향 그래프의 모든 노드를 **방향성에 거스르지 않도록 순서대로 나열**하는 것을 의미
- **예시)** 선수과목을 고려한 학습 순서 설정

![https://blog.kakaocdn.net/dn/bQrnk6/btqKvQUKVEA/UHEgtsl5lkYnrc1CdtxkyK/img.png](https://blog.kakaocdn.net/dn/bQrnk6/btqKvQUKVEA/UHEgtsl5lkYnrc1CdtxkyK/img.png)

- 위 세 과목을 모두 듣기 위한 **적절한 학습 순서**는?
    - 자료구조 → 알고리즘 → 고급 알고리즘 (O)
    - 자료구조 → 고급 알고리즘 → 알고리즘 (X)

### ** 진입차수와 진출차수

- **진입차수(Indegree):** 특정한 노드로 들어오는 간선의 개수
- **진출차수(Outdegree):** 특정한 노드에서 나가는 간선의 개수

---

## 위상 정렬 알고리즘

- **큐**를 이용하는 **위상 정렬 알고리즘의 동작 과정**은 다음과 같다
    1. 진입차수가 0인 모든 노드를 큐에 넣는다
    2. 큐가 빌 때까지 다음의 과정을 반복한다
        1. 큐에서 원소를 꺼내 해당 노드에서 나가는 간선을 그래프에서 제거한다
        2. 새롭게 진입차수가 0이 된 노드를 큐에 넣는다

**=>** 결과 적으로 **각 노드가 큐에 들어온 순서가 위상 정렬을 수행한 결과**와 같다

### 특징

- 위상 정렬은 DAG에 대해서만 수행할 수 있다
    - **DAG (Direct Acyclic Graph):** 순환하지 않는 방향 그래프
- 위상 정렬에서는 **여러 가지 답이 존재**할 수 있다
    - 한 단계에서 큐에 새롭게 들어가는 원소가 2개 이상인 경우가 있다면 여러 가지 답이 존재한다
- **모든 원소를 방문하기 전에 큐가 빈다면 사이클이 존재**한다고 판단할 수 있다
    - 사이클에 포함된 원소 중에서 어떠한 원소도 큐에 들어가지 못한다
- 스택을 활용한 DFS를 이용해 위상 정렬을 수행할 수도 있다

### 구현

```

from collectionsimport deque

# 노드의 개수와 간선의 개수를 입력 받기
v, e = map(int, input().split())
# 모든 노드에 대한 진입차수는 0으로 초기화
indegree = [0] * (v + 1)
# 각 노드에 연결된 간선 정보를 담기 위한 연결 리스트 초기화
graph = [[]for iin range(v + 1)]

# 방향 그래프의 모든 간선 정보를 입력 받기
for _in range(e):
    a, b = map(int, input().split())
    graph[a].append(b) # 정점 A에서 B로 이동 가능
    # 진입 차수를 1 증가
    indegree[b] += 1

# 위상 정렬 함수
deftopology_sort():
    result = [] # 알고리즘 수행 결과를 담을 리스트
    q = deque() # 큐 기능을 위한 deque 라이브러리 사용

    # 처음 시작할 때는 진입차수가 0인 노드를 큐에 삽입
for iin range(1, v + 1):
if indegree[i] == 0:
            q.append(i)

    # 큐가 빌 때까지 반복
while q:
        # 큐에서 원소 꺼내기
        now = q.popleft()
        result.append(now)
        # 해당 원소와 연결된 노드들의 진입차수에서 1 빼기
for iin graph[now]:
            indegree[i] -= 1
            # 새롭게 진입차수가 0이 되는 노드를 큐에 삽입
if indegree[i] == 0:
                q.append(i)

    # 위상 정렬을 수행한 결과 출력
for iin result:
        print(i, end=' ')

topology_sort()
```

### 시간복잡도

- 위상 정렬을 위해 차례대로 모든 노드를 확인하며 각 노드에서 나가는 간선을 차레대로 제거해야 한다
    - 위상 정렬 알고리즘의 시간 복잡도는 **O(V + E)** 이다

## 기타

## 에라토스테네스의 체 알고리즘

- 다수의 자연수에 대하여 소수 여부를 판별할 때 사용하는 대표적인 알고리즘이다
- 에라토스테네스의 체는 N보다 작거나 같은 모든 소수를 찾을 때 사용할 수 있다
- 에라토스테네스의 체 알고리즘의 **구체적인 동작 과정**은 다음과 같다
    1. 2부터 𝑁까지의 모든 자연수를 나열한다
    2. 남은 수 중에서 아직 처리하지 않은 가장 작은 수 𝑖를 찾는다
    3. 남은 수 중에서 i의 배수를 모두 제거한다(𝑖는 제거하지 않는다)
    4. 더 이상 반복할 수 없을 때까지 2번과 3번의 과정을 반복한다

### 구현

```

import math

n = 1000 # 2부터 1,000까지의 모든 수에 대하여 소수 판별
array = [Truefor i in range(n + 1)] # 처음엔 모든 수가 소수(True)인 것으로 초기화

# 에라토스테네스의 체 알고리즘
for i in range(2, int(math.sqrt(n)) + 1): # 2부터 n의 제곱근까지의 모든 수를 확인하며
ifarray[i] ==True: # i가 소수인 경우 (남은 수인 경우)
        # i를 제외한 i의 모든 배수를 지우기
        j = 2
while i * j <= n:
array[i * j] =False
            j += 1

# 모든 소수 출력
for i in range(2, n + 1):
ifarray[i]:
print(i, end=' ')
```

### 시간복잡도

- 에라토스테네스의 체 알고리즘의 시간 복잡도는 사실상 선형 시간에 가까울 정도로 매우 빠르다
    - 시간 복잡도는 **O(NloglogN)** 이다

## 투 포인터 (Two Pointers)

- **투 포인터 알고리즘**은 리스트에 순차적으로 접근해야 할 때 두 개의 점의 위치를 기록하면서 처리하는알고리즘을 의미한다
- 흔히 2, 3, 4, 5, 6, 7번 학생을 지목해야 할 때 간단히 '2번부터 7번까지의 학생'이라고 부르곤 한다
- 리스트에 담긴 데이터에 순차적으로 접근해야 할 때는 **시작점**과 **끝점** 2개의 점으로 접근할 데이터의범위를 표현할 수 있다
- 시간복잡도: O(N)

## 우선순위 큐(Priority Queue)

- 우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료구조이다
- 예를 들어 여러 개의 물건 데이터를 자료구조에 넣었다가 높은 물건 데이터부터 꺼내서 확인해야하는경우에 우선순위 큐를 이용할 수 있다
- Python, C++, Java를 포함한 대부분의 프로그래밍 언어에서 **표준 라이브러리 형태로 지원**한다

[제목 없음](https://www.notion.so/cf3998c68af34e9689076a25a0bca90e)

---

## 힙(Heap)

- 우선순위 큐(Priority Queue)를 구현하기 위해 사용하는 자료구조 중 하나이다
- **최소 힙(Min Heap)** 과 **최대 힙(Max Heap)** 이 있다
- 다익스트라 최단 경로 알고리즘을 포함해 다양한 알고리즘에서 사용된다

[제목 없음](https://www.notion.so/303ae9d289924f50b284e5ffc5a6d1b6)

---

## 힙 라이브러리 사용 예제: 최소 힙

```
import heapq

# 오름차순 힙 정렬(Heap Sort)
defheapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
for valuein iterable:
        heapq.heappush(h, value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
for iin range(len(h)):
        result.append(heapq.heappop(h))
return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```

실행 결과

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---

## 힙 라이브러리 사용 예제: 최대 힙

```
import heapq

# 오름차순 힙 정렬(Heap Sort)
defheapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
for valuein iterable:
        heapq.heappush(h, -value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
for iin range(len(h)):
        result.append(-heapq.heappop(h))
return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)
```

실행 결과

```
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```