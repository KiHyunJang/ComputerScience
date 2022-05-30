# 소수 판별 알고리즘 (Prime Number Algorithm)
  
## 소수 판별 알고리즘의 선수 지식
1.자연수는 1과 소수 합성수로 이루어져있다.  
2.소수는 1과 자기 자신으로만 나누어 떨어지는 수이다. (약수 2개)  
3.합성수는 1과 소수가 아닌수 (약수 2개 초과)  
  
## 소수 판별 알고리즘
**일반적인 소수 판별 알고리즘**  
``` swift
func PrimeNumber (_ num : Int) -> Bool {
    guard num > 1 else { return false}
    for n in 2 ..< num {
        if num % n == 0 { return false }
    }
    return true
}
```
위 방법은 만약 5가 들어왔다고 가정.  
2부터 4까지 반복문을 통해 연산 후 나누어 떨어진다면,  
1과 자기 자신을 제외한 수가 나누어 떨어진다는 의미므로 소수가 아니다.  
하지만 1억과 같이 큰 숫자가 들어오면 너무 비효율적일 것이다.  
이것을 해결하기 위해 개선된 소수 판별 알고리즘이 있다.  
  
**개선된 소수 판별 알고리즘**  
``` swift
func PrimeNumber (_ num : Int) -> Bool {
    guard num > 1 else { return false}
    for n in 2 ..< Int(sqrt(Double(num)))+1 {
        if num % n == 0 { return false }
    }
    return true
}
```
탐색 범위를 num의 제곱근 까지로 바꾼 것.  
예를 들어서 16의 약수는 1,2,4,8,16이다.  
1 x 16 = 16  
2 x 8 = 16  
4 x 4 = 16  
서로 대칭하는 수끼리 곱하면 16이 나온다.  
어차피 이렇게 모든 수의 약수는 대칭하는 수끼리 곱하면 자기 자신이 나오므로,  
주어지는 수의 제곱근까지만 판별하면 된다.  
