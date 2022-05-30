# 에라토스테네스의 체 알고리즘 (Sieve of Eratosthenes)
  
기원전 200년부터 사용된 검증된 알고리즘이며,  
고대그리스 수학자인 에라토스테네스가 만들어 낸 소수를 찾는 방법이다.  
마치 체로 치듯이 수를 걸러낸다고 하여, 에라토스테네스의 체라고 부른다.  
​  
이 알고리즘은 1부터 n까지의 자연수 중에서 소수를 모두 구하시오 와 같은 문제에서 매우 좋은 성능을 보여준다.  
  
지워지지 않은 가장 낮은 자연수부터 소수라면 그 수의 배수를 n까지 모두 지우는 것을 반복.  
우리는 코드로 True and False로 나타낼 것이다.  
  
**에라토스테네스의 체 구현**  
``` swift
func Sieve_of_Eratosthenes(_ num : Int ) -> [Int] {
    var answer = [Int]()
    var arr = [Bool]()
    
    for _ in 0...num{
        arr.append(true)
    }
    
    arr[0] = false
    arr[1] = false
    
    for i in 0 ..< num+1 {
        if arr[i] == true{
            answer.append(i)
            for j in stride(from: i * 2, through: num , by: i) {
                arr[j] = false
            }
        }
    }
    return answer
}
```
