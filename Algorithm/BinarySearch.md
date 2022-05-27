# BinarySearch
  
이진 탐색은 정렬되어 있는 리스트에서 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하는 방법.  
이진 탐색은 시작점, 끝점, 중간점을 이용하여 탐색 범위를 설정한다.  
  
**이진 탐색 알고리즘의 동작과정 예시**  
1.정렬된 데이터의 집합의 중앙 요소와 찾으려는 데이터 값을 비교.  
2.만약 찾으려는 값이 중앙 요소보다 작다면 왼쪽에서, 크다면 오른쪽에서 중앙요소 선택한다.  
위 과정을 중앙요소와 찾으려는 데이터 값과 일치할 때까지 반복.  
  
이진탐색은 선형탐색보다 거의 항상 빠른 편이며,  
배열의 크기가 500만개라면, 선형 탐색은 최대 500만번,  
이진 탐색은 최대 23회 이내로 찾을 수 있다.  
이진 탐색의 시간복잡도는 O(log n)이다.  
  
**이진 탐색 구현 예시**  
``` swift
import Foundation

func BinarySearch (_ arr : [Int], target : Int ) -> Int {
    var start = 0
    var end = arr.count - 1
    
    while start <= end {
        let mid = (start + end) / 2
        
        if arr[mid] == num { return true }
        if arr[mid] > num {
            end = mid - 1
        } else {
            start = mid + 1
        }
    }
    return false
}
```
