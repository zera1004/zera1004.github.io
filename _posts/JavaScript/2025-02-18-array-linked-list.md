---
title: "[Data structure] Array와 LinkedList"
excerpt: "데이터 구조 Array와 LinkedList의 차이점과 각각의 장단점"

categories:
  - JavaScript
tags:
  - [JavaScript, Data structure]

toc: true
toc_sticky: true

date: 2025-02-18 20:38:00 +0900
last_modified_at: 2025-02-18 20:39:30 +0900
---

## 배열 (Array)

배열은 같은 데이터 타입의 요소들이 연속적으로 저장되는 데이터 구조.  
각 요소는 인덱스를 통해 접근할 수 있음.

**특징**  
고정 크기: 배열의 크기는 생성 시 결정되며, 이후에 변경할 수 없음.  
연속 메모리: 배열의 요소들은 메모리에서 연속적으로 할당.  
빠른 접근: 인덱스를 사용하여 O(1) 시간 복잡도로 요소에 접근할 수 있음.

**장점**  
빠른 인덱스 접근: 특정 인덱스에 있는 요소에 즉시 접근할 수 있음.  
메모리 효율성: 메모리 할당이 연속적이므로 캐시 성능이 좋음.

**단점**  
고정 크기: 배열의 크기를 변경할 수 없으므로, 초기 크기를 잘못 설정하면 낭비가 발생하거나 부족할 수 있음.  
삽입 및 삭제의 비효율성: 배열의 중간에 요소를 삽입하거나 삭제할 경우, 나머지 요소들을 이동해야 하므로 O(n) 시간 복잡도가 필요.

<br>

## 연결 리스트 (Linked List)

연결 리스트는 각 요소(노드)가 데이터와 다음 노드를 가리키는 포인터를 포함하는 데이터 구조.  
노드들은 메모리에서 연속적으로 저장되지 않아도 됨.

**특징**  
동적 크기: 연결 리스트는 크기가 동적이며, 필요에 따라 노드를 추가하거나 삭제할 수 있음.  
노드 구조: 각 노드는 데이터와 다음 노드를 가리키는 포인터로 구성.

**장점**  
동적 크기: 필요에 따라 노드를 추가하거나 삭제할 수 있어 메모리 사용이 유연함.  
삽입 및 삭제의 효율성: 리스트의 중간에 노드를 삽입하거나 삭제하는 것이 O(1) 시간 복잡도로 가능 (해당 노드에 대한 포인터만 있으면).

**단점**  
느린 접근: 특정 인덱스에 있는 요소에 접근하려면 O(n) 시간 복잡도가 필요. 노드를 순회해야 하기 때문.  
추가 메모리 사용: 각 노드가 포인터를 추가로 저장해야 하므로, 배열에 비해 메모리 사용이 비효율적일 수 있음.

<br>

## 요약

| 특성           | 배열 (Array)               | 연결 리스트 (Linked List) |
| -------------- | -------------------------- | ------------------------- |
| 크기           | 고정 (변경 불가)           | 동적 (변경 가능)          |
| 메모리         | 연속적                     | 비연속적                  |
| 접근 시간      | O(1) (인덱스 접근)         | O(n) (순회 필요)          |
| 삽입/삭제 시간 | O(n) (중간 요소 이동 필요) | O(1) (포인터 변경만 필요) |
| 메모리 효율성  | 효율적 추가                | 포인터로 비효율적         |
