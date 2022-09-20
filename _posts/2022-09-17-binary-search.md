---
title : "Binary Search"

excerpt : "BinarySearch"

categories: [Algorithm]

tags: [Algorithm, python, BinarySearch]

date: "2022-09-17"

layout : post



---

### BinarySearch

```python
# 이진 탐색 재귀 구현
'''
- 인덱스 시작점, 끝점 확인
- 양끝의 인덱스 나누어 가운데 인덱스 저장
- 찾는 수가 가운데 인덱스 값보다 크면 오른쪽, 작으면 왼쪽 탐색
- 위 단계 반복

- array 전체 배열, target 찾는 값, start 시작 인덱스,
end 끝 인덱스
'''
def binary(array, target, start, end):
    if start > end:
        return None

    mid = (start + end)//2
    print(f'mid : {mid}')

    if array[mid] == target:
        return mid

    elif target > array[mid]:
        return binary(array, target, mid+1, end)
        # binary(array, target, mid+1, end)

    elif target < array[mid]:
        return binary(array, target, start, mid-1)

    else:
        print('none')
        pass


# 전체 원소 갯수, 타겟 넘버
n, k = map(int, input().split())

array00 = list(map(int, input().split()))

result = binary(array00, k, 0, n-1)

if array00[result] == k:
    print(result+1)

else:
    print('원소가 존재 하지 않음')
```

------

####





