# CPU 스케줄링
  
## 프로세스의 상태 4가지를 설명하라.
- running : cpu 선점한 상태인 프로세스
- ready : 메모리 등 cpu 선점조건을 만족하고, cpu를 기다리는 상태
- blocked(wait, sleep) : 프로세스가 요청한 event가 만족되지 않아 cpu를 당장 주어도 실행할 수 없는 상태 (예: I/O 작업이 필요한 상태)
- suspended : 외부적인 이유(메모리에 너무 많은 프로세스가 있거나, 사용자가 프로세스를 중단시켰을 때)로 프로세스가 정지된 상태
  
## 스케줄러의 종류를 설명하라
스케쥴러는 각각의 프로세스 Queue 에 대해 프로세스를 push, poll하는 OS코드를 말한다.  
  
1. **장기스케줄러(Long-term scheduler or job scheduler)**  
메모리는 한정되어 있는데 많은 프로세스들이 한꺼번에 메모리에 올라올 경우, 대용량 메모리(일반적으로 디스크)에 임시로 저장된다.  
이 pool 에 저장되어 있는 프로세스 중 **어떤 프로세스에 메모리를 할당하여 ready queue 로 보낼지 결정**하는 역할을 한다.  
  
- 메모리와 디스크 사이의 스케줄링을 담당.
- 프로세스에 memory(및 각종 리소스)를 할당(admit)
- degree of Multiprogramming 제어(실행중인 프로세스의 수 제어)
- 프로세스의 상태new -> ready(in memory)
  
*cf) 메모리에 프로그램이 너무 많이 올라가도, 너무 적게 올라가도 성능이 좋지 않은 것이다. 참고로 time sharing system 에서는 장기 스케줄러가 없다. 그냥 곧바로 메모리에 올라가 ready 상태가 된다.*  
  
2. **단기스케줄러(Short-term scheduler or CPU scheduler)**  
- CPU 와 메모리 사이의 스케줄링을 담당.
- **Ready Queue 에 존재하는 프로세스 중 어떤 프로세스를 running 시킬지 결정.**
- 프로세스에 CPU 를 할당(scheduler dispatch)
- 프로세스의 상태 ready -> running -> waiting -> ready
  
3. **중기스케줄러(Medium-term scheduler or Swapper)**  
- **여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫓아냄 (swapping)**
- 프로세스에게서 memory 를 deallocate
- degree of Multiprogramming 제어
- **현 시스템에서 메모리에 너무 많은 프로그램이 동시에 올라가는 것을 조절하는 스케줄러.**
- 프로세스의 상태 ready -> suspended
  
## 프로세스를 스케줄링하기 위한 Queue 종류는?
- Job Queue : 현재 시스템 내에 있는 모든 프로세스의 집합
- Ready Queue : 현재 메모리 내에 있으면서 CPU 를 잡아서 실행되기를 기다리는 프로세스의 집합
- Device Queue : Device I/O 작업을 대기하고 있는 프로세스의 집합
  
## 프로세스를 관리하는 시스템콜 4가지와 각각의 과정을 설명하라
- fork : 프로세스를 생성하는 시스템콜
- 부모 프로세스는 0이상의 리턴값을 가지고 자식 프로세스는 리턴값이 0이다
  
- exec : execpl 인터페이스를 통해 새로운 프로세스를 실행하는 시스템콜
  
- wait : 자식 프로세스가 종료될 때까지 부모 프로세스를 block 상태로 만들고, 종료되면 부모 프로세스를 ready 상태로 만드는 시스템콜
  
- exit : 모든 자원을 반납시켜 프로세스를 종료시키는 시스템콜
- 자발적으로 컴파일러가 실행하거나 부모가 강제로 자식프로세스를 종료시킬 때나 부모가 종료될 때 실행된다.
  
## CPU 스케쥴러와 Dispatcher를 설명하라
- cpu 스케쥴러 : ready 상태의 프로세스 중 running 프로세스를 고르는 os 코드
- dispatcher : cpu 스케쥴러가 고른 프로세스에게 cpu에 넘기는 os코드(문맥교환)
  
## CPU 스케쥴링이 필요한 상태변화 4가지를 설명하라
- running → blocked : by 시스템콜
- running → ready : by time interrupt
- blocked → ready
- terminated : 프로세스 끝낼 때
  
## 스케쥴링 성능척도 5가지를 설명하라
- cpu 이용률
- 처리량
- 소요시간, 대기시간, 응답시간
  
## **FCFS(First Come First Served)**
#### **특징**  
- 먼저 온 고객을 먼저 서비스해주는 방식, 즉 먼저 온 순서대로 처리.
- 비선점형(Non-Preemptive) 스케줄링일단 CPU 를 잡으면 CPU burst 가 완료될 때까지 CPU 를 반환하지 않는다. 할당되었던 CPU 가 반환될 때만 스케줄링이 이루어진다.
  
#### **문제점**  
- convoy effect소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상이 발생한다.
  
## **SJF(Shortest - Job - First)**
#### **특징**  
- 다른 프로세스가 먼저 도착했어도 CPU burst time 이 짧은 프로세스에게 선 할당
- 비선점형(Non-Preemptive) 스케줄링
  
#### **문제점**  
- starvation효율성을 추구하는게 가장 중요하지만 특정 프로세스가 지나치게 차별받으면 안되는 것이다. 이 스케줄링은 극단적으로 CPU 사용이 짧은 job 을 선호한다. 그래서 사용 시간이 긴 프로세스는 거의 영원히 CPU 를 할당받을 수 없다.  
  
## **SRTF(Shortest Remaining Time First)**
#### **특징**  
- 새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어진다.
- 선점형 (Preemptive) 스케줄링현재 수행중인 프로세스의 남은 burst time 보다 더 짧은 CPU burst time 을 가지는 새로운 프로세스가 도착하면 CPU 를 뺏긴다.
  
#### **문제점**  
- starvation
- 새로운 프로세스가 도달할 때마다 스케줄링을 다시하기 때문에 CPU burst time(CPU 사용시간)을 측정할 수가 없다.
  
## **Priority Scheduling**
#### **특징**  
- 우선순위가 가장 높은 프로세스에게 CPU 를 할당하는 스케줄링이다. 우선순위란 정수로 표현하게 되고 작은 숫자가 우선순위가 높다.
- 선점형 스케줄링(Preemptive) 방식더 높은 우선순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU 를 선점한다.
- 비선점형 스케줄링(Non-Preemptive) 방식더 높은 우선순위의 프로세스가 도착하면 Ready Queue 의 Head 에 넣는다.
  
#### **문제점**  
- starvation
- 무기한 봉쇄(Indefinite blocking)실행 준비는 되어있으나 CPU 를 사용못하는 프로세스를 CPU 가 무기한 대기하는 상태
  
#### **해결책**  
- 아무리 우선순위가 낮은 프로세스라도 오래 기다리면 우선순위를 높여주자.
  
## **Round Robin**
#### **특징**  
- 현대적인 CPU 스케줄링
- 각 프로세스는 동일한 크기의 할당 시간(time quantum)을 갖게 된다.
- 할당 시간이 지나면 프로세스는 선점당하고 ready queue 의 제일 뒤에 가서 다시 줄을 선다.
- `RR`은 CPU 사용시간이 랜덤한 프로세스들이 섞여있을 경우에 효율적
- `RR`이 가능한 이유는 프로세스의 context 를 save 할 수 있기 때문이다.
  
#### **장점**  
- `Response time`이 빨라진다.n 개의 프로세스가 ready queue 에 있고 할당시간이 q(time quantum)인 경우 각 프로세스는 q 단위로 CPU 시간의 1/n 을 얻는다. 즉, 어떤 프로세스도 (n-1)q time unit 이상 기다리지 않는다.
- 프로세스가 기다리는 시간이 CPU 를 사용할 만큼 증가한다.공정한 스케줄링이라고 할 수 있다.
  
#### **주의할 점**  
설정한 `time quantum`이 너무 커지면 `FCFS`와 같아진다. 또 너무 작아지면 스케줄링 알고리즘의 목적에는 이상적이지만 잦은 context switch 로 overhead 가 발생한다. 그렇기 때문에 적당한 `time quantum`을 설정하는 것이 중요하다.

## Multilevel Queue
- ready queue를 여러 개로 분할하여 각 큐에 독립적인 스케쥴링 알고리즘을 갖게하는 방법
- 먼저 처리하는 interactive한 프로세스의 큐는 RR 알고리즘을 가지고,
- 그 후에 처리하는CPU bound 프로세스는 FCFS 알고리즘을 가진다.
  
#### Multilevel Feedback Queue
- Multilevel Queue방식에서 다른 큐로 이동 가능한 방법을 말한다.
  
## **Real time scheduling**
데드라인 개념이 추가된 스케쥴링 알고리즘
  
- Hard real-time 스케쥴링 : 데드라인 안에 반드시 끝내도록 스케쥴링을 해야하는 알고리즘
- Soft real-time 스케쥴링 : 일반 프로세스에 비해 높은 priority를 갖도록 해야하는 알고리즘
