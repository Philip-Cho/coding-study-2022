# 보충 개념

## [리스트의 메소드]
#### 1. index(value)
- ex) 최대/최소값의 인덱스 찾기
```
a = [3,5,2,7,4]
max_a = max(a)
min_a = min(a)
print(a.index(max_a))
print(a.index(min_a))

# 더 간단한 방법으로는 numpy의 argmax 메소드가 있다
np.argmax(a)
np.argmin(b)
```

#### 2. insert(index, value)
- 리스트 특정 인덱스 위치에 새 값을 삽입한다

#### 3. count(value)
- value가 나온 횟수를 나타냄

#### 4. reverse()
- 리스트를 반전시킴
- **inplace=True**가 **default**로 적용된다

#### 5. remove(value)
- 리스트 순서상 처음으로 나오는 value 값을 제거한다 (pop은 인덱스로 접근하지만, remove는 value로 접근함)
- **inplace=True**가 **default**로 적용된다

#### 6. del
- pop과 같이 index로 삭제 가능
```
a = [1,2,3,4,5]

del a # a 리스트 자체를 제거
del a[4] # 4번째 인덱스 값인 5 제거
a.pop(4) # 4번째 인덱스 값인 5 제거
```

<br>


## [문자열 메소드]
크롤링 및 데이터 전처리 과정에서 문자열을 여러가지 방법으로 다루게 될 일들이 많다. 또한, 자바의 경우 문자열은 하나의 객체로 메모리 효율과도 관련이 있다. 효율적으로 코딩하기 위해 알아둬야 할 몇가지 메소드들을 정리해두고자 한다.

<br>

## [순열과 조합, 그리고 페어링(pairing)]
- 리스트 1개의 원소들에 대한 **순열(Permutation)**을 iteration 형태로 반환
- 리스트 1개의 원소들에 대한 **조합(Combination)**을 iteration 형태로 반환
- 리스트 2개의 원소들에 대한 **조합(Combination)**을 iteration 형태로 반환

```
from itertools import permutations, combinations, product

a = [1,2,3,4]
b = [5,6,7,8]

# 리스트1, 순열, 조합(2개 뽑아 나열)
print(list(permutations(a, 2)))   # [(1, 2), (1, 3), (1, 4), (2, 1), (2, 3), (2, 4), (3, 1), (3, 2), (3, 4), (4, 1), (4, 2), (4, 3)]
print(list(combinations(a, 2)))   # [(1, 2), (1, 3), (1, 4), (2, 3), (2, 4), (3, 4)]

# 리스트2, 모든 원소들에 대한 조합
print(list(product(a,b)))         # [(1, 5), (1, 6), (1, 7), (1, 8), (2, 5), (2, 6), (2, 7), (2, 8), (3, 5), (3, 6), (3, 7), (3, 8), (4, 5), (4, 6), (4, 7), (4, 8)]
```

<br> 

## [sort() VS sorted()]

(수정)
- sorted 람다 방식: 메뉴 리뉴얼 문제
- sorted(food_dict.items(), key=lambda item: item[1])
<br>

## [슬라이싱]
**문자열, series, dataframe** 등의 **datatype**에 관하여 특정 index의 값을 구해야하거나 특정 범위의 값을 찾는 경우가 많다. 한편, 대부분의 프로그램 언어들은 인덱스 번호가 0부터 시작이 되고 경우에 따라 마지막 범위가 포함이 되는 경우도 있고 안되는 경우도 있다. 이번 파트에서는 인덱스가 0부터 시작되는 이유에 대해 알아본 후 슬라이싱 규칙에 대해 정리해보고자 한다. 추가로, 시계열 혹은 패널 데이터의 경우에도 슬라이싱 규칙이 경우에 따라 다른데 이에 대해서는 추후에 정리하도록 한다.

<br>

## [딕셔너리의 key값]
리스트를 딕셔너리의 키 값으로 사용하게 되면 오류가 발생한다. **("TypeError: unhashable type: 'list'")**
- set 혹은 dictionary 키 값은 **해시 가능한 값**이어야 한다.
- **해시 가능**하기 위해서는 **변형이 불가능한(immutable) 값**이어야 한다.
- 리스트의 경우 추가(append), 제거(remove)가능하므로 mutable하다

따라서, **리스트 대신 튜플을 사용**하도록 한다

<br>

## 우선순위 큐(PriorityQueue)
- input으로 (우선순위, 데이터)를 삽입한다
```
import queue
data_queue = queue.PriorityQueue()

# input: (우선순위, 데이터)
data_queue.put((10, "korea"))
data_queue.put((5, 1))
data_queue.put((15, "china"))

data_queue.queue # [(5, 1), (10, 'korea'), (15, 'china')]
data_queue.qsize() # 3
data_queue.get() # (5, 1) 값을 pop
```

<br>


## [Runtime Error]
백준, 프로그래머스 문제를 풀다보면 test 데이터에 대해서 **'런타임 에러'**가 발생하는 경우가 있다. 파이썬을 직접 실행하는 경우에는 구체적으로 에러 위치를 볼 수 있을 테지만 문제는 test 데이터는 어떤 경우인지 주어지지 않는다는 점이다. **'런타임 에러'**가 발생했을 때는 다음과 같은 부분이 원인이 됬을 수 있으므로 확인해보도록 한다.

    1. 배열 인덱스 범위를 벗어났을 때 (자바 등의 경우 할당 크기를 넘었을 때 포함)
    2. 0으로 나눌 때
    3. 사용하는 라이브러리가 예외를 발생시켰을 때
    4. 재귀 호출이 너무 깊어질 때
    5. 이미 해제된 메모리를 참조할 때

경험에 따르면 주로 인덱스 범위 실수로 인한 경우가 가장 많으며, 리스트/딕셔너리 등에 참조해야하는 원소 값이 없을 때도 문제가 발생한다.
- **6주차 키패드 누르기 문제**의 경우 딕셔너리에 (2,2), (5,5), (8,8), (0,0)와 같은 키값들을 누락시켜서 에러가 발생했다.

<br>

## [정규 표현식]

<br>

## 기타 Tip
1. 파이썬에서 재귀함수는 **1000회 이상 호출**하면 에러가 발생한다.
    - 재귀함수를 위한 스택에서 1000개 만큼의 공간만 확보했기 때문
 
2. while문에 불린(boolean) 혹은 조건형태가 아닌 값을 넣을 경우 루프가 돈다.(계속 반복)
- 아래의 **링크드 리스트** 코드에서 **node.next**의 경우 **None**값이 오기 전까지 루프를 돈다
```
class Node:
    def __init__(self, data, next=None):
        self.data = data
        self.next = next

def add(data):
    node = head
    while node.next:
        node = node.next
    node.next = Node(data) 
```
