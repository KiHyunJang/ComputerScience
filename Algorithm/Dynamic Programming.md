# Dynamic Programming
  
DP는 메모리를 적절히 사용하여 수행 시간 효율성을 비약적으로 향상시키는 방법이다.  
이미 계산된 결과(작은 문제)는 별도의 메모리 영역에 저장하여 다시 계산하지 않도록 한다.  
DP의 구현은 일반적으로 top-down, bottom-up 두 가지 방식이다.  
  
DP는 문제가 다음의 조건을 만족할 때 사용할 수 있다.  
**1.최적 부분 구조**  
큰 문제를 작은 문제로 나눌 수 있으며 작은 문제의 답을 모아서 큰 문제를 해결할 수 있다.  
  
**2.중복되는 부분 문제**  
동일한 작은 문제를 반복적으로 해결해야 한다.  
  
top-down, bottom-up의 설명을 위해 피보나치 수열을 예시로 들어보겠다.  
**탑다운 방식**  
``` swift
func FibonacciNumbers(_ n: Int) -> Int {
    
    if n == 1 || n == 2{
        return 1
    } else if n == 0{
        return 0
    } else {
        return fibonacci(n-1) + fibonacci(n-2)
    }
}
```
위는 피보나치 수열을 재귀를 통해 탑다운 방식으로 풀어낸 것이다.  
  
**바텀업 방식**  
``` swift
func FibonacciNumbers(_ num: Int) -> Int {
    var dpTable: [Int] = [0, 1]

    guard num > 1 else { return n }

    for n in 2...n {
        dpTable.append(cache[n - 2] + cache[n - 1])
    }

    return dpTable[num]
}
```
위는 피보나치 수열을 바텀업을 이용한 방식이다.  
다이나믹 프로그래밍의 전형적인 형태는 바텀업 방식이다.  
결과 저장용 리스트는 DP테이블이라고 부른다.  
  
**탑다운과 바텀업 정리**  
흔히 top-down은 재귀 호출을, bottom-up은 반복문을 이용해 구현한다.  
Top-down 방식은 점화식을 이해하기 쉽다는 장점이 있고, Bottom-up 방식은 함수를 재귀 호출하지 않기 때문에 시간과 메모리 사용량을 줄일 수 있다는 장점이 있다.  
  
**DP와 분할 정복의 차이점**  
둘 다 최적 부분 구조를 가질 때 사용할 수 있다. (큰 문제를 작은 문제로 나누고 작은 문제의 답이 큰 문제를 해결할 수 있는 경우)  
하지만 차이점은 부분 문제의 중복이다.  
DP는 문제들이 서로 영향을 미치며 부분 문제가 중복.  
분할 정복은 동일한 부분 문제가 반복적으로 계산X  
ex)퀵 정렬에서 한번 분할이 이루어진 후 같은 피봇은 다시 처리X  
