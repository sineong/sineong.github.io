---
layout: default
title: Major
parent: Interview
nav_order: 1
---

# Major
{: .no_toc }

출제 가능성 있는 전공 내용 정리

참고 사이트 : https://kim-hyunsu.github.io/blog/undefined/graduate-entrance.html

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Major Required

### Data Structure

- array: 변수 / list: 리터럴
- max heap: 부모 노드의 키값이 자식 노드의 키값보다 크거나 같은 완전 이진 트리
    - priority queue 구현에 매우 적합. 최대 원소를 빼내면서 원소를 중간중간 추가할 수 있어야 하므로.
- max heap 구현시에 사용하는 자료구조
    - 배열
    - 힙의 마지막 노드의 위치를 빠르게 알 수 있고, 완전 이진 트리이므로 링크를 따로 저장하지 않아도 된다.(포인터 필요 X). memory-efficient.
- max heap 구현할 때 발생하는 메모리의 낭비
    - 배열로 구현할 경우 배열 재할당 문제
        - 할당해야하는 메모리의 2배씩 공간을 늘여서 재할당 하는 것
        - 데이터가 많을 경우 메모리 낭비 심하다.
- max value search / delete 비용
    - search: $O(1)$
    - delete and heapify 하는 것: $O(log n)$
- max heap 만드는 비용
    - 정렬되지 않은 array 를 맥스힙으로 만드는 비용은 $O(n)$

- max heap 에 insert/delete 하는 과정
    - 1-2-3-4-5-6 insert하고 2 delete하고 다시 7 insert
        - 맨 끝에 먼저 붙인 다음 parent 와 값 비교.
        - Heap property 침해하면 swap. 괜찮을 때까지 반복.
- 정렬시에 추가적인 메모리가 필요하지 않은 정렬: in-place sort라고 한다.
    - 추가적인 메모리에는 상수 정도의 임시 변수 등은 고려하지 않는다.
    - 다음 각각의 정렬 기법들이 in-place sort인지 O, X로 답하고 간략히 설명하라:
        - Insertion : O, $O(n^2)$
        - Selection : O, $O(n^2)$
        - Bubble :  O, $O(n^2)$
        - Merge : X, $O(nlogn)$
            - merge 할 때 $O(n)$ 의 extra space 필요하다
            - in-place merge 알고리즘이 존재하긴 함
        - Heap : O, $O(nlogn)$
        - Quick : X, $O(nlogn)$
            - $O(logn)$ stack space 필요

- 다음 자료구조에 새로운 데이터를 삽입하는 데 걸리는 시간을 데이터의 수 n에 관한 theta notation으로 답하시오:
    - BST: $\theta(log n)$
        - 검색과 동일. 삽입은 실패하는 검색 후 상수시간의 후처리를 하므로
    - Hash Table : amortized O(1)
        - The hash table should be well-implemented, or the efficiency can be compromised
        - (!!) 해쉬 충돌나면 어떻게 들어가는지. BST랑 비교.
- 다음 정렬 방법에 담긴 recursion을 설명하시오:
    - quicksort
    - selection sort
- AVL tree vs 일반 binary search tree
    - 각 노드에서 왼쪽 서브 트리의 높이와 오른쪽 서브 트리의 높이 차이가 1이하인 이진 탐색 트리를 말한다. AVL 트리는 트리가 비균형 상태로 되면 스스로 노드들을 재배치하여 균형 상태로 만든다.
    - 따라서 AVL트리는 균형 트리가 항상 보장되기 때문에 탐색, 삽입, 삭제 시간이 $O(log(n))$시간 안에 끝나게 된다.

### Algorithm
- Dijkstra Algorithm 이 음의 가중치를 갖는 edge를 허용하는가? 하면 왜 하는지 아니면 안하는 경우의 예를 보이시오.
    - 안한다. 최단 경로를 보장해주지 못하기 때문이다
    - 다익스트라 알고리즘에서 최단 경로를 구할 때 한번 확인한 node는 visited set에 넣고 다시 확인하지 않는데, 음의 가중치를 갖는 edge가 있으면 다른 곳을 돌아서 이미 visit한 node에 왔을 때 distance가 기존에 기록한 것 보다 더 작을 수 있다.
- 코드보고 시간복잡도 계산



### Computer Architecture
- CPU 가 인스트럭션을 수행하는 대표적인 과정
    - 인스트럭션을 읽어오는 Fetch, 읽어온 인스트럭션 종류에 따라 각 유닛으로 보낵 적절한 제어 신호를 생성하는 Decoding, 인스트럭션의 연산 결과인 ALU의 출력값이 저장되는 Execution, 실행 결과값을 최종적으로 타겟 레지스터에 저장하는 Write back. 이 과정을 여러 clock에 나눠 실행.
- 파이프라이닝
    - 하나의 인스트럭션 수행이 완전히 끝날 때까지 기다리지 않고 인스트럭션 수행을 단계별로 나누어 여러 인스트럭션이 중첩되어 각 단계별로 진행되는 것.
    - cpu의 사이클이 갈수록 빨라질 때, 파이프라인의 단계가 더 세분화 된다.
    - 파이프라인 구조에서 depth란? 이것은 성능에 어떤 영향을 미치는가?
        - 파이프라이닝 stage 수. CPI = 1 + Pipeline stall clock cycles per instruction. 이상적으로는 depth가 깊어지면 성능이 향상되지만 발열문제가 있기 때문에 31단계 이상으로 높아지지 못했다.
    - 파이프라인 구조에서 발생할 수 있는 exception에는 무엇이 있는가? 어떤 방식으로 해결할 수 있는가?
        - Exceptions definition: “unexpected change in control flow”. Another form of control hazard. 종류로는 Page fault on instruction/data fetch, Misaligned memory access, Memory-protection violation, Undefined/illegal opcode, Arithmetic exception. System takes action to handle the exception
    - 파이프라이닝에서 발생하는 세 가지 문제점을 설명하고 그에 대한 해결책을 말하시오
        - CPU의 구성상의 문제로 인한 구조적인 위험(Structural Hazard)
        - 동일 리소스를 둘러싼 충돌(ID와 WB와의 충돌 -> 반클락씩 사용함으로써 회피)
        - 이전 단계의 데이터에 의존하게 되는 인스트럭션으로 인한 데이터 위험(데이터 포워딩을 통해 해결)
        - 분기 위험
- branch prediction이 왜 중요한가
    - branch prediction 안하면 결과가 나올때까지 계속 stall 해야하므로 CPI가 너무 늘어난다
- average memory access time 계산하는 방법
    - hit cycle * hit rate + miss cycle * miss rate
- 캐시의 크기가 늘어나면 access time에 어떤 변화가 생기는지
    - 느려진다. access time 증가. Physically memory size 가 커지만 distance 도 증가.
- RISC와 CISC의 차이점?
    - Reduced Instruction Set Computer / Complex instruction Set Computer.
    - RISC 방식은 모든 인스트럭션의 길이가 동일하며 일반적으로 CPU 의 처리단위인 한 워드와 동일하게 맞춰져있다. 또한 메모리 억세스는 일반적으로 LOAD/STORE 정도의 인스트럭션으로 제한되며 나머지는 모두 레지스터 기반의 연산이므로 상대적으로 레지스터 개수가 많다.
    - 이에 반해 CISC 의 인스트럭션 길이는 인스트럭션 마다 다르고 메모리와 직접 연산하는 인스트럭션이 많고 일반적으로 연산을 저장하는 어큐뮬레이터가 있어 계산을 위한 다수의 레지스터가 필요없다.
    - RISC랑 CISC 중에 뭐가 더 좋지? RISC.
    - 최근 고성능 CPU는 대부분이 RISC 방식을 채택하고 있다.
    - RISC 장점: 인스트럭션 길이가 모두 동일하므로 파이프라인 처리의 고속화 가능. 컴파일러 설계도 단순해짐. 신뢰도가  높다.
- MIPS
    - 총 32개의 범용 32비트 레지스터를 가지는 전형적인 RISC 방식 CPU.(모든 인스트럭션이 32bit)
- Amdahl's law란 무엇인가? 이것은 RISC architecture에 어떻게 적용되는가?
    - 컴퓨터 시스템의 일부를 개선할 때 전체적으로 얼마만큼의 최대 성능 향상이 있는지 계산하는 데 사용.  파이프라이닝할 때 차례로 수행되어야하는 비교적 적은 수의 instruction들이 전체적인 속도 향상을 제한함.
- Write back과 Write through
    - Write back : cache 에만 update. 나중에 cache에서 뺄 때 memory로 update. 빠르다. Memory - cache Inconsistency 때문에 난감한 경우가 발생할 수도.
    - Write through : memory에 write할 때 cache 와 memory 둘 다 update. 상대적으로 느림.
- make common case fast라는 아이디어를 적용한 예를 다음에서 드세요.
    - ISA : MIPS puts typical constants in memory and loads them into special hardwired registers (e.g., $ 0)
      - Add “a few” opcodes that allow one operand to be stored in the instruction: addi, slti, li
    - memory structure : cache
- cache miss의 3종류를 쓰고 각각을 해결하는 방법을 쓰세요. 해결방법이 평균캐시접근 시간에 방해가 된다면 왜 그런지 쓰세요.
    - Compulsory : first reference miss.
    - Capacity : program working set is much larger than cache capacity
        - It can be reduced by a larger cache ( But! A large cache may increase the access time )
        - 데이터 구조의 압축으로 해결.
     - Conflict :  several blocks are mapped to the same set or block frame.
        - It can be reduced by a higher associativity ( But!! A higher associativity may increase the access time )
        - 어드레스를 서로 충돌나지않게 변경.

- 캐시를 디자인할 때 두 가지의 지역성(locality)을 활용하는데 이것이 무엇이고 어떻게 적용되는지 설명하시오
    - Temporal locality : 가장 최근에 읽어온 데이터는 다시 access할 때도 빠르게 access할 수 있도록 -> loop도는 코드에서 유용
    - Spatial locality : 한번 참고한 영역은 다시 access할 때 빠르게. Sequential execution.
    - Smaller blocks do not take maximum advantage of spatial locality But if blocks are too large, there are fewer blocks available, and more potential conflicts misses.

- 한블럭이 8byte인 cache의 총 용량이 64byte일때 가능한 cache의 종류의 수
    - 4가지.
        - 1-way associativity : 8 sets, 1 blocks each -> directly mapped
        - 2-way associativity : 4 sets. 2 blocks each
        - 3-way associativity : 2 sets. 4 blocks each
        - 4-way associativity : 1 set. 8 blocks. -> fully associative.
    - 위 캐시에서 set이 가장큰 경우와 작은 경우에서 hit ratio와 hit time에 대해 설명하시오
        - set size가 가장 큰 4-way가 hit ratio가 크다(miss rate이 낮다) Hit time은 길다. set size 가장 작은 1-way 는 hit ratio 작고 hit time은 짧다.

### OS
- 뮤텍스
    - 일종의 Locking 매커니즘. 열쇠를 가지고 있을 경우에만 locking 해둔 공유 데이터에 접근 가능하다.
- 세마포어
    - 세마포어는 동시에 리소스에 접근할 수 있는 '허용 가능한 Counter의 갯수'를 가지고 있는 Counter.
- 쓰레드(thread)
    - 어떤 한 프로세스의 실행환경에서 코드가 실행되는 과정 혹은 그 주체를 일컬음
- 멀티쓰레딩(multithreading)
    - 한 프로세스에서 여러개의 쓰레드가 공유하는 코드를 실행함을 의미함.
- 프로세스
    - 프로세스란 프로그램이 실행되는 동안의 모습을 말한다. 프로그램이 수행되기 위한 자원 소유의 단위. “One program can be several processes”. 프로세스는 컴퓨터가 계산하는데 있어 중심 역할을 수행하며, 온갖 상태 정보를 다 PCB에 유지한다 (텍스트 섹션, 프로그램 카운터, 스택, 데이터 섹션, 힙) // 프로세스 이미지 : 프로그램, 데이터, 스택, PCB의 모음.
- 멀티태스킹에서 메모리 swap이 무엇인가, 메모리swap이 멀티태스킹을 어떻게 변화시키는가
    - 프로세스를 실행 도중에 임시로 주 메모리에서 방출(swap out), 보조 메모리에 적재: 디스크 이용
    - CPU 스케쥴러가 다음으로 실행될 프로세스를 ready queue에서 고르고 dispatcher 호출. 자유 메모리 공간이 없다면 다른 프로세스 swap out (완전히 idle 한 프로세스만 swap out 해야한다) 실행시키고자 하는 프로세스 swap in

- 어떤 작업은 여러 개의 부분 작업(sub-task)들로 이루어진다. 주어진 작업을 이런 부분 작업들로 나눠서 해결하는 방식을 사용하려 할 때, thread 기반으로 하는 것과 process 기반으로 하는 것 중에 더 나은 것은 무엇인가? 설명하라.
    - thread 기반. thread는 자동적으로 그들이 속한 프로세스의 자원들과 메모리를 공유한다. 이것의 이점은 한 응용프로그램이 같은 주소공간 내에 여러개의 다른 작업을 하는 쓰레드를 가질 수 있다는 것. 또한 프로세스 생성을 위해 메모리와 자원을 할당하는 것은 비용이 많이 드므로 자신이 속한 프로세스의 자원을 공유하는 thread가 더 경제적이다.

- Access control list가 matrix에 비해 가지는 장점은 무엇인가?
    - 1) Access control list
        - 특정 데이터 및 프로그램에 접근할 수 있는 사용자를 지정한다. ACL에서는 일반적으로 접근할 수 있는 사용자와 사용할 수 있는 서비스 기능의 목록을 가지고 있다. 예를 들어, 파일 XYZ에 대해 ACL에 (Alice, delete)와 같은 목록이 있다면, Alice에게 XYZ 파일을 삭제할 권한을 부여한 것이다.
    - 2) Access matrix
        - 주체와 객체의 접근허용권한을 주체는 행(row)으로 객체는 열(column)로 나타난 테이블이다. 한 명의 사용자가 가지는 다양한 리소스에 대한 권한을 나타내는 것은 행(row)이다. 예를 들면 다음과 같다.
        - 사용자 l 파일1 l 파일2 l 파일3
          사용자1 l 읽기 l 쓰기 l 실행
          사용자2. l. R/W l NONE l R
        - 위 형태는 임의적 접근통제기법(DAC: Discretionary Access Control) 유형의 접근통제로서 단점으로 테이블 관리가 어렵다는 점이 있다. 이에 반해 ACL은 객체의 관점에서 접근권한을 지정한 목록이다.

- 디스크에 대한 SCAN 알고리즘은 어떤 요청을 무한정 연기할 수 있는가? 만약 그렇다면 예를 들어 설명하시오.
    - 네. SSTF (Shortest Seek Time First) 알고리즘에서 14와 186이 큐에 들어있는데 14를 처리하는 동안 계속 14근처에 새로운 요청이 들어온다면 186 요청은 무한정 연기되는 기아 현상이 발생할 가능성이 있다.

- 두 개의 process가 ready 상태에 있다. 한 프로세스는 cpu bound job이고, 다른 하나는 i/o bound job이다. 둘 중 어느 프로세스를 수행하는 것이 유리한가? 왜 그런가?
  - i/o bound job. Utilization 을 maximize 하기 위해서는 i/o bound job을 먼저 수행하고 i/o에서 대기하는 동안(i/o device busy) cpu bound job을 수행하면 된다.

- 교착상태(데드락)
  - 4가지 필요조건
    - mutual exclusion
    - hold and wait
    - no preemption
    - circular wait
  - 이것들을 어떻게 막을 수 있나 (prevent)
    - 필요조건 네 가지가 성립하지 않게 미리 조치함. 어느 하나 만이라도 성립하지 않으면 OK
    - 안전한 상태(safe state) : 시스템 상태가 안전하다는 말은 시스템이 어떤 순서로든 프로세스들이 요청하는 모든 자원을 dead lock 없이 차례로 할당해줄 수 있다는 것
        - 종류별 자원개수가 하나 : resource allocation graph
        - 종류별 자원개수가 여러개 : Banker’s algorithm: 다수의 프로세스가 자원을 이용하려고 할 때, 각 프로세스의 요구를 만족할 수 있는 순서를 발견함 (만일 존재한 다면)
  - 데드락을 해소하는 방법
    - 1) process termination : 전체 혹은 하나 이상의 프로세스 실행을 취소하여 deadlock 싸이클 제거 // 비용이 너무 크거나 overhead 크다
    - 2) resource preemption
    - 3) select victim - minimize cost
      - 희생된 프로세스(victim)은 후진 (rollback)
      - starvation 가능 -> 해결방법 : cost factor 에 rollback 횟수 추가

- 한 블록이 4KB일 때, 디스크의 크기가 4TB인 경우에서 page table entry의 크기
  - 4TB / 4KB = 2^30
- PTE의 크기를 줄이는 방법
  - Multi level paging.


### Programming Language

---

## Major Elective

### Database
### Network
