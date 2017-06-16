---
layout: post
title: "운영체제 정리 및 복습"
description: 
headline: 
modified: 2017-06-14
category: OperatingSystem
tags: [OperatingSystem]
image: 
  feature: 
comments: true
mathjax: 
---
# Operating System

## Implementing File Systems

### Introduction

* BLOCK
  * 디스크와 메모리 사이를 오가는 데이터의 단위
  * 각 Block은 하나 이상의 섹터(Sector)를 가지는데, 보통 512bytes다.

### Virtual File Systems

* UNIX 계열과 non-UNIX 계열 파일 시스템을 동시에 지원한다.

* 하나의 System Call Interface로 다른 타입의 파일 시스템을 이용할 수 있다.

* VFS serves two important functions
  * 깔끔한 VFS Interface를 정의함으로써 구현(Implemetation)과 각각의 동작(Operations)을 분리한다.
  * File을 나타내는 독자적인 매커니즘을 제공한다. VFS는 vnode라고 불리는 구조체에 기반한다.

### Allocation Methods

* 정의
  * 파일을 위해 disk space를 어떻게 할당할 것인가?
  * Efficient Utilization과 Fast Access는 할당 방법에 의존한다.

* Contiguous Allocation
  * 각각의 파일은 인접한 block들의 집합으로 디스크에 점유한다.
  * 첫 block에 파일의 길이가 저장되어있다.
  * 문제점
    * 파일이 할당되었다가 해제되고 난 후에 새로운 파일을 할당하려고 할 때 전체적으로 남아있는 용량은 문제없지만, 블록들이 파편화되어 있기 때문에 할당하지 못할 수도 있다.
    * 하나의 파일에 용량을 얼만큼 잡아야 예측하기 어렵다.

* Linked Allocation
  * 각각의 파일은 block들의 Linked List로 구성되며, 디스크 상에 흩어져 있다.
  * 각 디렉토리 엔트리는 첫 block과 마지막 block을 가리키는 포인터를 가지고 있다.
  * 문제점
    * Random File Access에 대해 매우 큰 탐색 오버헤드를 가진다.
    * 포인터를 위해 용량이 필요하다.
  * 해결책
    * Cluster(Block들을 모아 만듬)를 할당한다.
    * 그러나 Internal Fragmentation이 발생한다.

* Indexed Allocation
  * Linked Allocation에서의 Direct File Access나 Random File Access 문제를 해결하기 위해 고안됨.
  * Index Block이라는 하나의 block에 모든 포인터를 모아놓는다.
  * Index Block
    * Disk-Block 주소의 배열
    * i-th block은 배열의 i-th 원소
  * 문제점
    * 작은 파일은 문제 없지만, 큰 파일의 경의 수천 개의 블록이 필요할 수 있다.
  * 해결책
    * 배열의 원소에 배열을 물려 깊게 만든다.

### Buffer Cache

* File에 접근할 때는 반드시 Disk에 접근해서 데이터를 가져와야 한다. 하지만 Disk Access는 큰 I/O Overhead를 유발한다.
* File 접근은 강한 Temporal Locality를 가진다.
* 따라서 중간에 Buffer Cache를 배치함으로써 Disk에 대한 접근을 최대한 줄인다.

---

## Memory Management Strategies

### Memory Mangement for Multiprogramming

* 몇 개의 프로세스들은 Physical Memory에 동시에 올라간다.

* OS와 다른 것들의 메모리 영역에 User Process가 접근하는 것을 보호하기 위해 Protection Mechanism이 제공되어야 한다.

* 해결책
  * Base와 Limit라는 레지스터를 사용한다.
  * Base 레지스터는 가장 작은 Physical Memory 주소를 가지고 있는다.
  * Limit 레지스터는 범위의 크기를 가지고 있는다.

### Logical Vs. Physical Adrress Space

* Logical Address
  * CPU에 의해 생성된 주소

* Virtual Address Space
  * 실행 중인 프로그램이나 프로세스에 의해 생성된 주소들의 집합

* Physical Address
  * Physical Memory 상의 주소

* Physical Address Space
  * 각 Logical Address는 대응되는 Physical Address를 가진다. Physical Address의 집합은 Virtual Address의 집합과 대응된다.

* Memory Management Unit(MMU)
  * Virtual Address를 대응되는 Physical Address로 변환해주는 CPU 내의 하드웨어 장치
  * 매핑 방법은 프로세서마다 다르다.

### The Need of Virtual Address

* 실제 Physical Memory 주소들을 본다는 것은 User Program에게 매우 힘들 것이다. 왜?
  * 유저들 스스로 특정 Physical Memory에 프로그램을 올려야 한다.
  * 다른 프로그램의 메모리 영역을 침범하지 않기 위해 조심히 코드를 짜야한다.

* The SOLUTION : Virtual Address
  * 유저 프로그램은 더 이상 Physical Memory를 신경쓰지 않아도 된다.
  * 모든 시작 주소가 0인 환상을 모든 실행 중인 프로그램이나 프로세스에게 준다.
  * MMU에 의해 프로그램은 적절한 위치의 Physical Memory에 적재된다.

### Swapping

* 프로세스가 실행되기 위해서 반드시 메모리에 올려져야 한다.

* 그러나 메모리의 부족으로 실행되지 않을 수 있다.

* Backing Store
  * 모든 프로세스의 메모리 이미지 카피 본을 저장할 수 있을 만큼 큰 크기의 저장소
  * 반드시 이 메모리 이미지들에 직접 접근을 지원해야한다.

* The SOLUTION : Swapping
  * 메모리 여유를 만들기 위해, 프로세스를 잠시 메모리 밖의 Backing Store와 Swap함.
  * 작업 완료 후 다시 되돌려서 실행한다.

### Memory Allocation

* Contiguous Memory Allocation
  * 프로세스들은 멀티프로그래밍을 지원하기 위해 동시에 Physical Memory에 올라가야 한다.
  * 재배치 할 때 각 프로세스 메모리를 보호하기 위해 Base와 Limit는 필수다.
  * 해결책 : Contiguous Allocation
    * 각 프로세스는 하나의 연속된 메모리 섹션을 가진다.

* External Fragmaentation
  * 프로세스들은 자주 메모리에 적재되거나 제거된다.
  * 제거 될 때 자잘하게 남은 메모리 공간으로 나뉠 수 있다.
  * 이런 파편화를 External Fragmentation라고 부른다.
  * 해결책
    * Compaction : 최적화 한다.
    * Non-Contiguous Address Space of Processes : 연속적인 하나의 메모리 영역을 가지는 대신에 분산 시켜서 적재한다.

### Paging

* 최신 어플리케이션과 시스템에서 프로세스들은 빈번히 종료되거나 스왑된다.

* 이런 경향 때문에, External Fragmentation으로 인해 Mulitprogramming의 효율이 감소될 수 있다.

* 해결책
  * Paging
    * Paging을 통해 프로세스의 Physical Address Space를 비연속적으로 할 수 있다.
    * Physical Memory를 Page Frame이라고 불리는 고정된 사이즈의 블록들로 쪼개고, Virtual Memory를 Page라 불리는 같은 사이즈의 블록들로 쪼갠다.

* Basic Operations of Paging
  * 프로세스가 실행될 때, Page들이 Backing Store의 가능한 Memory Frame에 적재된다.

* Address Translation
  * Virtual Memory Reference는 메인 메모리의 Page Frame과 해당 Page의 Offset으로 변환된다.

* Hardware Support
  * 프로세서 내의 MMU가 소프트웨어 도움 없이 Page를 Page Frame으로 변환한다.

### Address Translation Architecture

* Page Table
  * Page Table은 Page에 대응되는 Page Frame과의 Mapping 정보를 가지고 있다.
  * Virtual Address Space(or Process)당 하나의 Page Table이 존재한다.
  * Page Number (*p*)
    * Physical Memory에 있는 각 페이지의 Base Address를 포함하고 있는 Page Table의 Index로 사용된다.
  * Page Offset
    * Page와 Frame 내의 Offset

* Internal Fragmentation
  * 메모리를 필요한 것보다 조금 더 크게 잡을 경우에, 실제로 쓰이지 않는 잉여 공간을 의미한다.

* Memory Protection
  * OS나 다른 프로세스에 의해 허용되지 않는 메모리 영역에 침범하는 것을 방지해야 한다.
  * 해결책 : Protection Bit Per Page
    * Protection Bit는 각 Page Table Entry 당 하나씩 존재한다.
    * 하나의 Bit는 Page가 Read-Write인지 Read-Only인지 정의할 수 있다.
    * Page Number로 Physcial Memory와 대응되는 Page Table을 찾을 때, 해당 Bit가 Read-Only인 Memory에 Write를 하지 못하도록 확인한다.

* Valid-Invalid Bit
  * Virtual Memory가 Physical Memory보다 큰 경우에 일부 Page와 Frame이 매팽되지 않는 경우가 생긴다.
  * 이 때, Page들이 Frame과 매핑되어 있는지 확인하는 행동이 필요하다.
  * Mechanism
    * Valid-Invalid Bit는 페이지 당 Page Table Entry에 추가 된다.
    * Valid Bit 
      * Page와 Page Frame이 연결되어 있다.
    * Invalid Bit
      * Page와 Page Frame이 연결되어 있지 않다.

### Segmentation

* Segment
  * 프로그래머가 인지하는 논리적인 엔티티

* Segment의 타입
  * Text Code
  * Global Variation
  * Heap
  * Stacks
  * Standard C library or Imported Shared Library

* Segmentation
  * Virtual Address를 다양한 사이즈의 Segment로 쪼개는 것.

---

## Process Concepts

### Process

* Process란 실행 중인 Program이다.

* Process는 Virtual Address Space와 Control Information으로 구성된다.

* Process가 포함한 것들
  * Program Counter
  * Stack
  * Data Section
  * Control Information

* Process States
  * New : 생성되고 있는 중
  * Running : 명령어가 실행되고 있는 중
  * Waiting : 이벤트가 발생하기를 기다리는 중
  * Ready : 할당되기를 기다리는 중
  * Terminated : 실행이 종료됨

### Process Control Block(PCB)

* Process State
  * Ready, Running, Waiting, Halted 등

* Program Counter
  * 다음에 실행될 명령어의 주소

* CPU Register
  * Stack Points, General Purpose Registers

* CPU Scheduling Information
  * 우선순위, 스케쥴링 Queue, Nice Value

* Memory-Management Information
  * Base와 Limit 값, Page Table 등

* Accounting Information
  * 실제 사용 시간, 시간 제한 등

* I/O Status Information
  * 프로세스에 할당된 디바이스 리스트, File Descriptor Table 등

### Process Scheduling

* Multi-Programming
  * CPU 효율성을 극대화 하기 위해, 동시에 여러 프로세스를 실행한다.

* Time-Sharing
  * 여러 유저가 컴퓨터를 동시에 공유하는 것을 허용하기 위함이다.
  * 각 유저에게 적은 CPU 시간이 주어진다.

* Process Scheduler
  * 위에 언급된 두 기능성을 고려해야 한다.
  * 프로그램 실행을 위해 가능한 프로세스를 선택하고 CPU와 교체해야 한다.

### Context Switch

* Context란 PCB를 말한다.

* Context Switching 중에 일어나는 작업
  * 현재 프로세스의 PCB를 저장
  * 새로운 프로세스의 저장된 PCB를 적재
  * Cache와 TLB(Translation Lookup Buffer) 초기화

* Context Switching 중에는 시스템이 일을 할 수 없으므로 Overhead를 발생시킨다.

* Hardware의 지원에 따라 소요되는 시간이 달라진다.

### Interprocess Communication(IPC)

* 같이 작업하는 프로세스와 통신하는 방법

* 대표적인 방법
  * Shared Memory
    * 일정 메모리 영역을 공유하는 방법
  * Message System
    * 공유 변수에 의존하지 않고 프로세스 서로 통신하는 방법

### Shared Memory

* Shared Memory의 System Call을 사용해서 다른 프로세스의 메모리 영역에 접근할 수 있다.

* 한 프로세스가 공유 메모리 영역을 만들고, 다른 프로세스가 해당 공유 메모리 영역에 Attach 해야 한다.

### Message Passing

* 프로세스들이 같은 메모리 영역을 공유하지 않으면서 서로 통신하고 동기화하는 방법

* Operations
  * send(*message*)
  * receive(*message*)

* Direct Communication
  * 프로세스들끼리 직접 통신하는 방식
  * 각 프로세스들이 서로 Link되어 있어야 가능하다
  * Disadvantage
    * 통신하던 프로세스 중 하나가 종료되었을 때 예상치 못한 결과를 가져올 수 있다.

* Indirected Communication
  * MailBox를 통해 통신하는 방식
  * MailBox와만 연결되어 있으면 된다.

### Synchronization

* Message Passing은 Blocking일 수 있고 Non-Blocking일 수 있다.

* **Blocking**은 *synchronous(동기적)*
  * **Blocking Send**는 메세지를 받게 될 때 까지 Sender를 Block시키고, Message Queue가 꽉 찼을 때 Block 시킨다.
  * **Blocking Receive**는 메세지를 도착할 때 까지 Receiver를 Block 시킨다.

* **Non-Blocking**은 *asynchronous(비동기적)*
  * **Non-Blocking Send**는 Sender가 계속 메세지를 보낼 수 있다.
  * **Non-Blocking Receive**는 Receiver가 계속 메세지를 받을 수 있게 한다.

---

## Process Schedulings

### CPU Scheduler

* 실행할 준비가 된 Ready Queue 내의 프로세스를 선택한다.

* CPU로 해당 프로세스를 보낸다.

* CPU의 의사 결정(Decision-Making)
  * Running -> Waiting
    * 프로세스가 I/O 작업을 요청했을 때
  * Running -> Ready
    * 프로세스가 Time Slice를 소모했을 때
  * Terminates

* Non-Preemptive(비선점형) Scheduling
  * 프로세스가 종료되거나 Waiting 상태로 바뀌기 전까지 CPU를 점유하고 있는 방식

* Preemptive(선점형) Scheduling
  * 현재 실행 중인 프로세스를 잠시 중단하고 다른 프로세스를 실행하는 방식

### Dispatcher

* Dispatcher Module은 Scheduler에 의해 선택된 프로세스에 대한 CPU의 Control을 지원한다.

* Dispatcher Module
  * Switching Context(문맥교환)
  * User Mode로 전환
  * 프로그램을 재시작하기 위해 유저 프로그램 내에서 적절한 위치로 점핑

* Dispatcher Latency
  * Dispatcher가 실행 중인 프로세스를 중지하고 새로운 프로세스를 실행하기까지 걸리는 시간

### Scheduling Algorithms

* Ready Queue에 있는 프로세스 중 어떤 프로세스를 CPU에 할당할지 결정하는 방법.

* First-Come, First-Served(FCFS) Algorithm
  * 작업이 요청된 순서대로 CPU에 할당하는 방법
  * FIFO Queue를 이용하여 구현
  * Non-Preemptive

* Shortest-Job-First(SJF) Algorithm
  * 다음 CPU Burst Time이 작은 프로세스를 CPU에 할당한다.
  * Non-Preemptive의 경우, 프로세스 한번 CPU에 할당되면 CPU Burst Time을 모두 소모할 때 까지 선점되지 않는다.
  * Preemptive의 경우, 새 프로세스가 도착했을 때 현재 프로세스의 남아있는 CPU Burst Time과 새 프로세스의 CPU Burst Time을 비교하여 적은 CPU Burst Time을 가진 프로세스를 CPU에 할당한다.
  * SJF는 평균 대기 시간이 최소이므로 최적이다.
  * 그러나 실제 구현상 어려움이 있다.
    * 실제로 프로세스의 CPU Burst Time을 측정할 수 없다.
    * 프로세스가 언제 I/O 작업을 하거나 종료될지 알 수 없다.

* Priorty Algorithm
  * 각 프로세스는 우선순위 번호를 가진다.
  * 가장 높은 우선순위를 가진 프로세스가 CPU에 할당된다.

* Round-Robin(RR) Algorithm
  * Time Sharing System을 위해 고안되었다.
  * 기본적으로 FCFS를 따른다.
  * 모든 프로세스는 같은 우선순위를 가지며, 정해진 Time Slice를 사용하면 Ready Queue로 보내진다.

* MultiLevel Queue Algorithm
  * Ready Queue를 여러 Queue로 나눈다.
  * 프로세스들은 각각의 속성에 따라 하나의 Queue에 배치된다.
  * 각각의 Queue는 자신만의 Scheduling Algorithm을 가진다.

* MultiLevel Feedback-Queue Alrogirthm
  * 한번 할당된 우선순위는 변하지 않는데, 이는 한 번 할당된 Queue에서 다른 Queue로 이동이 없는 것을 의미한다.
  * 이와 같은 상황은 CPU Utilization을 하락시킨다.
  * Mulitilevel Feedback Queue Algorithm은 프로세스의 우선순위에 변화를 주어 Queue간 이동이 가능하게 만든다.

---

## Threads

### Motivation of Threads

* Process의 문제점
  * 큰 Context Switching Overhead
  * 큰 프로세스 생성 시간
  * 큰 동기화 Overhead

### Multithreading

* 프로세스는 여러 Thread를 가질 수 있다.

* 현대 운영체제는 Multithreading 환경을 제공한다.

* Procedure Calls vs. Multithreading
  * 공통점
    * 다른 function이나 thread에 선언된 변수에 접근할 수 없다.
    * Global Data 또는 Heap 영역은 function이나 thread가 접근할 수 있다.
  * 차이점
    * Thread 하나당 Stack 하나를 가진다.
    * Function들의 병행 실행.

* Thread의 장점
  * 적은 Context Switching Overhead
  * 매우 짧은 Thread 생성 시간
  * 적은 동기화 Overhead
  * 작은 메모리 점유

* Thread와 Process의 관계
  * Process는 Thread들의 집합과 자원의 집합으로 구성된다.
  * 실행의 단위는 Thread
  * Process는 Thread에게 실행 환경을 제공한다.

### Multithreading Methods

* Many-to-One
  * 많은 User-Level Thread가 하나의 Kernel-Level Thread에 연결되는 방식
  * 단점
    * 하나의 User-Level Thread가 Block System Call을 호출할 경우에 프로세스 전체가 Block된다.

* One-to-One
  * 하나의 User-Level Thread가 하나의 Kernel-Level Thread에 연결되는 방식
  * 장점
    * 어떤 Thread가 Block System Call을 호출해도 다른 Thread가 실행될 수 있게 한다.
  * 단점
    * User-Level Thread 생성이 Kernel-Level Thread 생성이다.
    * Context Switching Overhead가 시스템 내의 thread 수에 의존한다.

* Many-to-Many
  * 많은 User-Level Thread가 그보다 적은 수의 Kernel-Level Thread에 대응되는 방식
  * 장점
    * Kernel-Level Thread의 개수 제한을 고려하면, 이 모델은 좋은 병행성을 제공한다.
  * 단점
    * 실제 병행성이 좋지는 않다. 4-to-3 모델의 경우 3개의 User-Level Thread가 Blocking System Call을 호출할 경우, 프로세스는 Block된다.

---

## Synchronizations

### Race Condition

* 다수의 Thread 또는 Process가 같은 데이터에 접근하여 조작할 때, 그 결과가 특정 순서에 따라 달라질 때를 Race Condition이라 한다.

### Critical Section Problem

* *Crtical* Section
  * 여러 Thread 또는 Process가 접근 가능한 공유 메모리 또는 공유 자원을 뜻한다.

* The SOLUTION : Synchronization
  * Mutual Exclusion
    * 어떤 프로세스가 Critical Section에서 작업하고 있으면, 다른 프로세스들이 접근하지 못하게 하는 방법
  * Progress
    * Critical Section에서 작업하는 프로세스가 없는 상태에서 Critical Section에 진입하고자 하는 프로세스가 존재할 때, Critical Section에 들어가고자 하는 다음 프로세스 선택은 무기한 연기될 수 없는 방법
  * Bounded Waiting
    * 제한된 대기 시간을 두어 다른 프로세스들이 Critical Section에 접근 가능하게 하는 방법

### Synchronization : LOCK

* LOCK
  * 동기화를 하기 위한 일반적인 방법
  * 현대 운영체제는 LOCK 메커니즘과 관련된 API를 지원함
  * ex) Mutex

* Terminology
  * Locking
    * Critical Section에 들어가기 위해 LOCK을 획득한 상태
  * Unlocking
    * Critical Section에서 빠져나와 LOCK을 놓은 상태

### Spin Lock

* Simple Lock 또는 Simple Mutex로 불린다.

* 특정 자원이 Spin Lock에 의해 보호되고 있을 경우, Thread는 자원이 Unlock될 때 까지 *Busy-Wait*한다.

### Semaphore

* 많은 하드웨어적 방법들이 프로그래머들이 사용하기에 복잡하다.

* Semaphore는 덜 복잡하다.

* Counting Semaphore
  * Semaphore를 여러 개 두고 사용

* Binary Semaphore
  * 하나의 Semaphore만 사용
  * Mutex와 같음

### Solution of Busy-Waiting

* Busy-Waiting 대신 Sleep 또는 Block을 사용
  * Semaphore를 기다리기 위해 Wait 하는 것은 비효율적, 즉시 Sleep 또는 Block 사용

* Block과 Busy-Waiting의 차이점
  * Block을 호출할 경우,프로세스가 Semaphore와 관련된 Waiting Queue로 이동됨

### Deadlock

* 두 개 이상의 프로세스들이 서로의 작업이 끝나기만을 기다리고 있는 상태

* Deadlock 발생 조건
  * Mutual Exclusion
    * 프로세스들이 필요로 하는 자원에 대해 배타적인 통제권을 요구.
  * Hold & Wait
    * 프로세스가 할당된 자원을 가진 상태에서 다른 자원을 기다린다.
  * No Preemptive
    * 프로세스가 어떤 자원을 사용하고 스스로 놓기 전까지 다른 프로세스가 해당 자원을 사용할 수 없다.
  * Circular Wait
    * 각 프로세스는 순환적으로 다음 프로세스가 필요로 하는 자원을 가지고 있는 경우다.

* Deadlock 발생 예방
  * Mutual Exclusion
    * 교착 상태는 두 개 이상의 프로세스가 공유 가능한 자원을 사용할 때 발생하는 것이므로 공유 불가능한, 즉 상호 배제 조건을 제거하면 된다.
  * Hold & Wait
    * 한 프로세스에 수행되기 전에 모든 자원을 할다이키고 나서 잠유하지 않을 때에는 다른 프로세스가 자원을 요구하도록 하는 방법이다.
  * No Preemptive
    * 비선점 프로세스에 대해 선점 가능한 프로토콜을 만든다.
  * Circular Wait
    * 자원 유형에 따라 순서를 매긴다.

---

## Secondary Storage Structure

### Disk Structure

* Disk Access Time
  * Disk에서 Sector를 Fetch하여 Memory에 올리는 시간
  * Positioning Time + Transfer Time

* Positioning Time
  * Seek Time + Rotational Time
  * Seek Time
    * Disk Arm을 요구하는 Cylinder로 이동하는 시간
  * Rotational Time
    * 요구된 Sector가 Disk Head로 회전하는 시간

* Head Crash
  * Disk Platter는 보호층으로 코팅되어 있다.
  * 가끔 Disk Head가 Disk Platter를 긁어 자기 표층을 손상시키는 경우를 Head Crash라 한다.

* Disk Sector or Block
  * 현대 Disk Driver는 하나의 큰 Disk Sector의 1차원 배열로 구성되어 있다.
  * Sector는 Cylinder Number, Cylinder 내의 Track Number, Track 내의 Sector Number로 매핑되어 있다.
  * Sector는 전송의 가장 작은 단위다.

### Disk Scheduling

* First-Come, First-Served(FCFS)
  * 들어온 순서대로 수행
  * 단점
    * Request에 따라 탐색 길이가 길어질 수 있다.

* Shortest-Seek-Time_First(SSTF)
  * 시작 포지션에서 가장 가까운 지점부터 탐색을 시작
  * 단점
    * 시작 지점과 멀리 있는 경우 Starvation이 발생할 수 있음

* SCAN
  * Disk Arm의 진행 방향이 한 쪽 끝으로 진행.
  * 끝에 도착하면 반대 방향으로 재탐색

* C-SCAN
  * SCAN과 마찬가지로 진행 방향이 한 쪽 끝으로 진행.
  * 끝에 도착하면 반대 방향이 아닌 Disk의 시작 지점으로 이동하여 재탐색

* LOOK & C-LOOK
  * SCAN과 C-SCAN 같이 한 방향으로 진행하되 해당 방향에 더 이상 탐색할 목표가 없으면 방향을 바꿈