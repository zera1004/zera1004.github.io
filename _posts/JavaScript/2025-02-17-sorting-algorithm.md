---
title: "[Algorithm] 정렬 알고리즘(Sorting Algorithm)의 종류"
excerpt: "정렬 알고리즘(Sorting Algorithm)의 종류 알아보기(선택 정렬, 버블 정렬, 병합 정렬, 삽입 정렬, 퀵 정렬, 힙 정렬"

categories:
  - JavaScript
tags:
  - [JavaScript, Algorithm]

toc: true
toc_sticky: true

date: 2025-02-17 21:05:00 +0900
last_modified_at: 2025-02-17 21:05:30 +0900
---

## 선택 정렬 (Selection Sort)

주어진 배열에서 가장 작은 요소를 찾아서 정렬되지 않은 부분의 맨 앞에 교환하는 방식.

```js
function selectionSort(arr) {
    const n = arr.length;
    for (let i = 0; i < n; i++) {
        let minIndex = i;
        for (let j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
    }
    return arr;
}

// 사용 예
console.log(selectionSort([64, 25, 12, 22, 11]));
```

```
초기 배열: [64, 25, 12, 22, 11]

1. 첫 번째 반복:
   - 가장 작은 요소 11을 찾고 64와 교환합니다.
   → [11, 25, 12, 22, 64]

2. 두 번째 반복:
   - 나머지에서 가장 작은 요소 12를 찾고 25와 교환합니다.
   → [11, 12, 25, 22, 64]

3. 세 번째 반복:
   - 나머지에서 22를 찾고 25와 교환합니다.
   → [11, 12, 22, 25, 64]

4. 네 번째 반복:
   - 마지막 두 요소는 이미 정렬되어 있습니다.
→ [11, 12, 22, 25, 64]
```


<br>

## 버블 정렬 (Bubble Sort)

인접한 요소를 비교하여 필요에 따라 교환함으로써 가장 큰 요소를 배열의 끝으로 "버블"처럼 이동시키는 방식.

```js
function bubbleSort(arr) {
    const n = arr.length;
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
            }
        }
    }
    return arr;
}

// 사용 예
console.log(bubbleSort([64, 34, 25, 12, 22, 11, 90]));
```

```
초기 배열: [64, 34, 25, 12, 22, 11, 90]

1. 첫 번째 반복 (끝까지):
   → [34, 25, 12, 22, 11, 64, 90]

2. 두 번째 반복:
   → [25, 12, 22, 11, 34, 64, 90]

3. 세 번째 반복:
   → [12, 22, 11, 25, 34, 64, 90]

4. 네 번째 반복:
   → [12, 11, 22, 25, 34, 64, 90]

5. 다섯 번째 반복:
   → [11, 12, 22, 25, 34, 64, 90]

결과: [11, 12, 22, 25, 34, 64, 90]
```

<br>

## 병합 정렬 (Merge Sort)

배열을 반으로 나누고 각각을 재귀적으로 정렬한 후 두 정렬된 배열을 병합하는 방식.

```js
function mergeSort(arr) {
    if (arr.length <= 1) {
        return arr;
    }

    const mid = Math.floor(arr.length / 2);
    const left = mergeSort(arr.slice(0, mid));
    const right = mergeSort(arr.slice(mid));

    return merge(left, right);
}

function merge(left, right) {
    const result = [];
    let i = 0, j = 0;

    while (i < left.length && j < right.length) {
        if (left[i] < right[j]) {
            result.push(left[i]);
            i++;
        } else {
            result.push(right[j]);
            j++;
        }
    }

    return result.concat(left.slice(i)).concat(right.slice(j));
}

// 사용 예
console.log(mergeSort([38, 27, 43, 3, 9, 82, 10]));
```

```
초기 배열: [38, 27, 43, 3, 9, 82, 10]

1. 분할 단계:
   - [38, 27, 43]와 [3, 9, 82, 10]으로 나눕니다.
   - [38]와 [27, 43]로 나누고, [27]과 [43]로 나눕니다.
   - [3, 9]와 [82, 10]으로 나눕니다.

2. 정복 단계 (병합):
   - [27]과 [43]을 병합하여 [27, 43]로 만듭니다.
   - [38]과 [27, 43]을 병합하여 [27, 38, 43]으로 만듭니다.
   - [3]과 [9]을 병합하여 [3, 9]으로 만듭니다.
   - [82]와 [10]을 병합하여 [10, 82]로 만듭니다.
   - [3, 9]과 [10, 82]을 병합하여 [3, 9, 10, 82]로 만듭니다.

3. 최종 병합:
   - [27, 38, 43]과 [3, 9, 10, 82]을 병합하여 최종 결과 [3, 9, 10, 27, 38, 43, 82]를 생성합니다.
```

<br>

## 삽입 정렬 (Insertion Sort)

배열을 두 부분(정렬된 부분과 정렬되지 않은 부분)으로 나누고, 정렬되지 않은 부분의 첫 번째 요소를 정렬된 부분에 적절한 위치에 삽입하는 방식.

```js
function insertionSort(arr) {
    for (let i = 1; i < arr.length; i++) {
        const key = arr[i];
        let j = i - 1;
        while (j >= 0 && key < arr[j]) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
    return arr;
}

// 사용 예
console.log(insertionSort([12, 11, 13, 5, 6]));
```

```
초기 배열: [12, 11, 13, 5, 6]

1. 첫 번째 반복 (11 삽입):
   - [11, 12, 13, 5, 6]

2. 두 번째 반복 (13은 이미 정렬됨):
   - [11, 12, 13, 5, 6]

3. 세 번째 반복 (5 삽입):
   - [5, 11, 12, 13, 6]

4. 네 번째 반복 (6 삽입):
   - [5, 6, 11, 12, 13]

결과: [5, 6, 11, 12, 13]
```

<br>

## 퀵 정렬 (Quick Sort)

피벗을 선택하고 배열을 피벗보다 작은 요소와 큰 요소로 나누어 재귀적으로 정렬하는 방식.

```js
function quickSort(arr) {
    if (arr.length <= 1) {
        return arr;
    }
    const pivot = arr[Math.floor(arr.length / 2)];
    const left = arr.filter(x => x < pivot);
    const middle = arr.filter(x => x === pivot);
    const right = arr.filter(x => x > pivot);
    
    return [...quickSort(left), ...middle, ...quickSort(right)];
}

// 사용 예
console.log(quickSort([3, 6, 8, 10, 1, 2, 1]));
```

```
초기 배열: [3, 6, 8, 10, 1, 2, 1]

1. 피벗 선택 (예: 10):
   - [3, 6, 8, 1, 2, 1] | 10

2. 다음 피벗 선택 (예: 8):
   - [3, 6, 1, 2, 1] | 8 | [10]

3. 다음 피벗 선택 (예: 6):
   - [3, 1, 2, 1] | 6

4. 다음 피벗 선택 (예: 3):
   - [1, 2, 1] | 3

5. 정렬된 배열로 병합:
   - 결과: [1, 1, 2, 3, 6, 8, 10]
```

<br>

## 힙 정렬 (Heap Sort)
힙 자료 구조를 기반으로 하는 정렬 알고리즘입니다. 배열을 힙으로 변환하고, 최대 힙의 루트(최대값)를 배열의 끝으로 이동시키는 과정을 반복하여 정렬.

```js
function heapSort(arr) {
    const n = arr.length;

    for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }

    for (let i = n - 1; i > 0; i--) {
        [arr[0], arr[i]] = [arr[i], arr[0]];
        heapify(arr, i, 0);
    }

    return arr;
}

function heapify(arr, n, i) {
    let largest = i;
    const left = 2 * i + 1;
    const right = 2 * i + 2;

    if (left < n && arr[left] > arr[largest]) {
        largest = left;
    }

    if (right < n && arr[right] > arr[largest]) {
        largest = right;
    }

    if (largest !== i) {
        [arr[i], arr[largest]] = [arr[largest], arr[i]];
        heapify(arr, n, largest);
    }
}

// 사용 예
console.log(heapSort([12, 11, 13, 5, 6, 7]));
```

```
초기 배열: [12, 11, 13, 5, 6, 7]

1. 최대 힙 형성:
   - [13, 11, 12, 5, 6, 7]

2. 최대값 13을 배열의 끝으로 이동:
   - [7, 11, 12, 5, 6, 13]

3. 남은 요소에 대해 최대 힙 형성:
   - [12, 11, 7, 5, 6] | 13

4. 최대값 12를 배열의 끝으로 이동:
   - [6, 11, 7, 5, 12, 13]

5. 이 과정을 반복하여 최종 결과:
   - [5, 6, 7, 11, 12, 13]
```