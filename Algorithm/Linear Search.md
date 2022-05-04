# 선형 탐색 알고리즘(Linear Search Algorithm)
   
## 선형 탐색
선형 탐색이란 말 그대로 선형적으로 왼쪽부터 오른쪽으로 차례대로 탐색하는 것을 의미한다.   
[3,4,5,1,5,7,8,4,2,1,8]값을 가진 배열에서   
내가 8을 찾는다면 왼쪽에서부터 차례대로 탐색하며 만약 8을 찾았다면   
탐색을 종료한다.   
​   
정렬 되지 않은 데이터에서 매우 효과적이며, 구현하기 쉽다는 장점이 있다.   
하지만 최악의 경우 O(n)의 시간복잡도를 가지며 배열의 크기가 커질수록 시간이 오래걸린다는 단점이 있다.   
   
## 선형 탐색 구현
``` swift
func linearSearch<T: Equatalbe>(_ array: [T], _ object: T) -> Int? {
    for (index, obj) in array.enumerated() where obj == object {
        return index
    }
    return nil
}
```
