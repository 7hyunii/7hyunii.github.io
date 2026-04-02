---
title: "모노톤 스택 (Monotonic Stack) 완벽 정리"
date: "2026-04-02"
categories: "Algorithm"
tags: ['algorithm', 'stack']
math: true
---

## 모노톤 스택이란?

스택의 LIFO(Last In First Out) 성질을 활용하며, **스택 내 원소들이 항상 단조 증가나 단조 감소 상태를 유지**하도록 관리하는 스택입니다.

* **단조 증가 스택 (Increasing):** 밑에서부터 위로 갈수록 값이 커지는 상태 (오름차순)
* **단조 감소 스택 (Decreasing):** 밑에서부터 위로 갈수록 값이 작아지는 상태 (내림차순)

## 왜 사용하는가?

일반적으로 배열에서 **나보다 크거나 작은 다음 원소**를 찾으려면 이중 반복문을 사용하는 브루트 포스($O(N^2)$)가 필요합니다. 하지만 모노톤 스택을 사용하면 **각 원소를 스택에 최대 한 번 Push 하고 한 번 Pop** 하기 때문에 **$O(N)$** 의 시간 복잡도로 해결할 수 있습니다.


## 동작 예시

단조 증가 스택(Monotonic Increasing Stack)을 시뮬레이션 해보겠습니다.

이 배열을 순회하며 스택 내부가 항상 **오름차순**이 되도록 유지해 보겠습니다.
```powershell
Array : [2, 1, 4, 5, 3]
```

### Step 1. `2` 삽입
- 스택이 비어있으므로 첫 원소 2를 스택에 Push 합니다.
```powershell 
Monotonic Stack : [2]
```

### Step 2. `1` 삽입 시도

- Step 1이 끝난 스택의 `Top`은 `2`로, 삽입을 시도하는 `1`보다 큽니다.
- 따라서, 단조 증가를 유지하기 위해 `2`를 Pop 한 후 `1`을 Push 합니다.
```powershell
Monotonic Stack : [1]
Popped : 2
```

### Step 3. `4` 삽입 시도
- Step 2가 끝난 스택의 `Top`은 `1`로, 삽입을 시도하는 `4`보다 작습니다. 그대로 `4`를 Push 합니다.
```powershell
Monotonic Stack : [1, 4]
Popped : 
```

### Step 4. `5` 삽입 시도
- Step 3이 끝난 스택의 `Top`은 `4`로, 삽입을 시도하는 `5`보다 작습니다. 그대로 `5`를 Push 합니다.
```powershell
Monotonic Stack : [1, 4, 5]
Popped : 
```

### Step 5. `3` 삽입 시도
- Step 4가 끝난 스택의 `Top`은 `5`로, 삽입을 시도하는 `3`보다 큽니다. 단조 증가를 유지하기 위해 `5`를 Pop 합니다.
- 그 다음 `Top`도 `4`로, 삽입을 시도하는 `3`보다 큽니다. 단조 증가를 유지하기 위해 `4`를 Pop 합니다.
- 최종적으로 `3`을 Push 합니다.
```powershell
Monotonic Stack : [1, 3]
Popped : 5, 4
```

## 언제 떠올리는 것이 좋은가?
- **Next Greater Element:** 오른쪽에서 처음으로 나보다 큰 수 찾기 (예: '오큰수')
- **Next Smaller Element:** 오른쪽에서 처음으로 나보다 작은 수 찾기 
- **가장 가까운 값 찾기:** 나보다 작거나 큰 값이 처음 등장하는 인덱스 찾기
- **히스토그램 문제** 

등의 문제에 유용하게 사용할 수 있습니다.

### 관련 백준 문제
- [17298(오큰수)](https://www.acmicpc.net/problem/17298)
- [1725(히스토그램)](https://www.acmicpc.net/problem/1725)
- [6549(히스토그램에서 가장 큰 직사각형)](https://www.acmicpc.net/problem/6549)

...


---

### 구현 참고
실제 문제를 풀 때는 스택에 **인덱스**를 넣는 것이 유리할 때도 많습니다.

- 예시 템플릿
```python
stack = []
for i in range(len(arr)):

    while stack and arr[stack[-1]] > arr[i]:
        target_idx = stack.pop()

        # 기타 추가적인 로직 수행 ~
        
    stack.append(i) # 인덱스 삽입
```

