---
layout: post
title: "자료구조 복습 및 정리"
description: 
headline: 
modified: 2017-06-07
category: DataStructure
tags: [datastructure]
image: 
  feature: 
comments: true
mathjax: 
---
# 자료구조(Data Structure)

## Chapter 1. Precondition & Postcondition

### Precondition

* 어떤 함수를 호출하는 프로그래머는 precondition이 유요하다는 것을 보장해야한다.

* 함수를 작성하는 프로그래머는 함수가 실행을 시작할 때, precondition이 참일 것을 기대할 수 있다.

### Postcondition

* 함수를 작성하는 프로그래머는 함수가 실행을 종료할 때, postcondition이 참이라는 것을 보장해야한다.

---

## Chapter 2. Abstract Data Types

* Class는 멤버 변수(Member Variables)와 멤버 함수(Member Functions)를 가진다. 객체(Object)란, 데이터 타입이 Class인 변수다.

* 프로그래머는 반드시 어떻게 새로운 클래스 타입을 선언할지, 어떻게 멤버 함수들을 사용할지, 해당 클래스를 어떻게 사용할지 알아야 한다.

* 대부분, 클래스의 멤버 함수는 멤버 변수에 정보를 배치하거나 이미 멤버 변수에 있는 정보를 사용한다.

---

## Chapter 3. Container Classes

* 컴퓨터 과학에서 Container Class는 클래스, 데이터 구조 또는 인스턴스가 다른 객체의 컬렉션인 추상 데이터 타입이다.

* 다르게 말하면, Contanier는 특정 접근 방법을 따르는 정해진 방법으로 객체들을 저장한다.

---

## Chapter 4. Pointers & Dynamic Arrays

* Dynamic Array는 Pointer와 Dynamic Memory Allocation을 이용하여 구현된다.

* Dynamic은 프로그램 실행 전에 정해지는 것이 아닌, 프로그램 실행 중에 만들어지는 것을 뜻한다.

---

## Chapter 5. Linked Lists

### Linked List

* 순서가 정해진 연속된 data 아이템, 각각은 link를 통해 다음으로 연결되어 있다.

* Linked List는 data와 link를 가진 Node라는 것으로 구성된다.

* Linked List는 Length, Insert, Remove, Search, Locate, Copy, Clear 등을 멤버 함수로 가질 수 있다.

### Doubly Linked Lists

* 기본적으로 (Singly) Linked List와 같으나, Singly Linked List는 다음 Node만을 가리키는 반면에 Doubly Linked List는 다음 Node만 아니라 이전 Node도 가리킨다.

---

## Chpater 6. Template, Iterator & STL

### Template

* 만약 각각 다른 프로그램에서 목적이 같은 함수를 다른 데이터 타입을 이용하여 사용하려 한다면, 프로그램 개수 만큼의 함수를 정의하여 사용해야 한다.

* 위와 같은 문제를 해결하기 위해서 필요한 것이 Template이다.

* ANSI/ISO C++ Standard는 STL(Standard Template Library)를 지원한다.

### Iterator

* Iterator는 프로그래머가 컨테이너 안에 있는 모든 아이템들에게 쉽게 접근하게 도와주는 객체다.

---

## Chapter 7. Stakcs

### Stack 이란

* 마지막에 있는 곳으로만 삽입 또는 제거를 할 수 있는 순서가 있는 자료구조

### Stack의 Errors

* Stack OverFlow
  * Stack overFlow는 Stack이 꽉 찬 상태에서 push하려는 경우 발생한다.

* Stack UnderFlow
  * Stack UnderFlow는 Stack이 비어있는 상태에서 pop하려는 경우 발생한다.

### Arithmetic Expressions

* Infix Notation
  * 연산자가 피연산자 사이에 위치하는 표현 방식
  * ex) (3 + 4) * 7

* Prefix Notation
  * 연산자가 피연산자 앞에 위치하는 표현 방식
  * ex) * + 3 4 7

* Postfix Notation
  * 연산자가 피연산자 뒤에 위치하는 표현 방식
  * ex) 3 4 + 7 *

* Evaluating Postfix
  1. Stack 초기화
  1. 더 읽을 것이 없을 때 까지, 숫자면 스택에 넣고 연산자면 스택에서 숫자 두 개를 pop하여 계산한 뒤 스택에 넣는다.

---

## Chapter 8. Queues

### Queue 란

* 마지막에 있는 곳으로만 삽입이 가능하고 앞에 있는 곳으로만 제거가 가능한 순서가 있는 자료구조

* FIFO(First In, First Out)

### Queue의 Errors

* Queue OverFlow
  * Queue OverFlow는 Queue가 꽉 찬 상태에서 push하려는 경우 발생한다.

* Queue UnderFlow
  * Queue UnderFlow는 Queue가 비어있는 상태에서 pop하려는 경우 발생한다.

### Palindrome

* Queue이나 Stack을 이용하면 앞 부터 읽은 것과 뒤 부터 읽은 것이 같은 단어나 문장을 확인할 수 있다.

### Priority Queue

* 각 엔트리들이 우선순위를 가지고 있어서, 삽입된 순서와 제거되는 순서가 일치하지 않는다.

---

## Chapter 9. Recursive Thinking

### Recursive Thinking

* Recursive Programming을 통해 문제를 작은 부분부터 해결하여 큰 문제를 해결할 수 있다.

* Recursive Programming은 호출마다 Memory의 Stack 영역에 쌓이므로, 많은 Recursive Function Call(재귀 함수 호출)은 Memory Stack Overflow를 유발할 수 있다.

---

## Chapter 10. Trees

### Tree란

* Tree는 Node들의 유한 집합이다.

* Tree는 어떤 노드도 가지지 않을 수 있으며, 이 경우 Null 또는 빈(Empty) 트리라고 부른다.

* 부모(Parent)는 어떤 노드에서 위로 연결된 노드를 뜻한다.

* 자식(Child or Childern)은 어떤 노드에서 아래로 연결된 노드를 뜻한다.

* 자손들(Siblings)은 같은 부모를 가진 노드들을 뜻한다.

* 뿌리(Root)는 부모를 가지지 않는 최상위 노드를 뜻한다.

* 잎(Leaf)은 자식이 없는 노드를 뜻한다.

* 조상(Ancestor)은 어떤 노드의 부모 노드들을 뜻한다. 부모 노드의 부모도 해당 노드의 조상이다.

* 후손(Descendant)은 어떤 노드의 자식 노드들을 뜻한다. 자식 노드의 자식도 해당 노드의 후손이다.

* 하위 트리(Subtree)는 기존 트리에 속한 부분적인 트리를 뜻한다.


### Binary Tree(이진 트리)

* 모든 노드가 최대 2개의 자식 노드를 가질 수 있다.

### Full Binary Tree(정 이진 트리)

* 모든 leaf가 같은 depth를 가진다.

* leaf가 아닌 모든 노드들은 2개의 자식 노드를 가진다.

### Complete Binary Tree(완전 이진 트리)

* 가장 깊은 depth를 제외한 depth의 노드들은 모두 존재해야 한다.

* 가장 깊은 depth의 노드들은 왼쪽으로 채워진다.

* 가장 깊은 depth가 모두 채워진 것도 Complete Binary Tree다.

### Representing a Binary Tree

* With Array
  * Root는 [0]
  * Left는 [2i + 1]
  * Right는 [2i + 2]

* With Node
  * data_field : 데이터 저장
  * left_field : Left를 가리키는 포인터 저장
  * Right_field : Right를 가리키는 포인터 저장

### Tree Traversals

* Traversals of Binary Trees
  * Pre-Order
    1. Root에서 시작
    1. Recursive Call을 이용한 Left Subtree 탐색
    1. Recursive Call을 이용한 Right Subtree 탐색
  * In-Order
    1. Recursive Call을 이용한 Left Subtree 탐색
    1. Root 탐색
    1. Recursive Call을 이용한 Right Subtree 탐색
  * Post-Order
    1. Recursive Call을 이용한 Left Subtree 탐색
    1. Recursive Call을 이용한 Right Subtree 탐색
    1. 마지막으로 Root 탐색

### Binary Search Tree

Binary Search Tree는 다음 조건을 만족하는 Binary Tree이다.

* 어떤 노드의 Left Subtree의 값은 항상 해당 노드의 값보다 작거나 같다.

* 어떤 노드의 Right Subtree의 값은 항상 해당 노드의 값보다 크다.

---

## Chapter 11. Tree Projects

### Heap

* Heap은 특정 노드 N의 값이 항상 자식들보다 큰 Complete Binary Tree이다.

### Representing Heap with Priority Queue

* Adding New Entry
  1. Complete Binary Tree에 맞게 마지막 노드에 새 값을 넣는다.
  1. 위쪽 방향으로 Parent와 비교하여 새 값이 크면 Swap한다.

* Removing an Entry
  1. 마지막 노드의 값을 삭제하고자 하는 노드에 삽입.
  1. 교체한 값을 아래쪽 방향으로 Child와 비교하여 작으면 Swap한다.

### B-Trees

* Rules of B-Tree
  * 단일 노드에 저장될 수 있는 최소 개수를 의미하는 양의 정수 *Minimum*이 있다.
  * Rules
    1. 노드의 데이터 수가 N개이면 자식의 수는 항상 N+1개여야 한다. 즉, 노드 2개의 데이터를 가진다면 그 노드의 자식은 반드시 3개여야 한다.
    1. 노드 내의 데이터는 반드시 정렬된 상태여야 한다.
    1. 노드의 데이터 D1의 왼쪽 서브 트리는 D1보다 작은 값들로 이루어져 있어야 하고, D1의 오른쪽 서브 트리는 D1보다 큰 값들로 이루어져 있어야 한다.
    1. Root 노드가 자식이 있다면 적어도 2개 이상의 자식을 가져야 한다.
    1. Root 노드를 제외한 모든 노드는 적어도 *Minimum/2*개의 데이터를 가지고 있어야 한다. ex) 5차 B트리라면 각 노드는 적어도 2개의 데이터를 가지고 있어야 한다.
    1. Leaf 노드로 가는 경로의 길이가 모두 같다. 즉, Leaf 노드는 모두 같은 레벨에 존재한다.
    1. 입력 자료는 중복될 수 없다.

## Chapter 12. Searching

### Serial Search(Linear Search)

* 처음부터 끝까지 순서대로 찾고자 하는 것을 찾아내는 방식

* 가장 단순한 Searching 방법이지만 매우 느린 방법이다.

### Binary Search

* 정렬된 상태의 배열을 정 가운데 index와 찾고자 하는 값을 비교하여 값을 찾아내는 방식

* 하지만, 정렬되지 않는 배열에 적용할 수 없다는 단점을 가진다.

### Hashing

* 특정 Key를 Hash Function에 넣어 얻은 값을 index로 사용하여 해당 index에 데이터를 저장하는 방식

* 다른 Key값이 같은 index를 내놓는 Collision이 발생할 수 있다. Collision의 해결방법이 필요하다.

### Open-Address Hashing

* Linear Probing
  * 특정 Hash Function을 통해 얻어낸 index를 *hash(key)* 라고 한다.
  * 만약 *data[hash(key)]* 가 비어있으면 저장하고 끝낸다.
  * 비어있지 않으면, *data[hash(key)+1]* 를 확인하고 비어있으면 저장후 종료, 비어있지 않으면 index를 하나씩 늘려가면서 확인한다.

* Doublie Hasing
  * Linear Probing의 경우 Clustering Problem으로 인해 Insertion 작업의 시간이 오래 걸릴 수 있다.
  * *Hash Function 1*과 *Hash Function 2*를 정의한다.
  * *Hash Function 1*을 통해 얻어낸 index가 비어있지 않으면 *Hash Function 2*를 통해 얻은 값을 index에 더한다.

### Chanined Hashing

* Array가 하나 이상의 Entry를 가질 수 있는 Hashing 방법이다.

* Collision이 발생하면 해당 index에 새로운 Entry를 추가한다.

### Table

* Table은 record에 대해 Insertin, Deleting, Locating을 수행하는 container이다.

* Single Key Field에 의해 결정된다.

* Hash와 Table의 개념이 합펴진 것이 HashTable이다.

### Hash Functions

* *Division* Hash Functions
  * 보통 *key % table_size*
  * table_size는 소수인 경우가 제일 이상적이다

* *Mid_Square* Hash Functions
  * *key * key* 를 2진수로 바꾼 후, 중간 digit을 선택

* *Multiplicative* Hash Functions
  * *a * key(0<a<1)* 의 값에서 숫자 몇 개를 선택
  * ex) key = 157, a = 0.0234521, 0.0234521 * 157 = 3.6819797에서 681 선택

---

## Chapter 13. Sorting

### Quadratic Sorting Algorithms

* Selection Sort(선택 정렬)
  1. 최대 범위부터 시작하여 범위를 하나씩 줄여나간다.
  1. 해당 범위에서 가장 큰 수를 찾아 마지막 index와 swap한다.

* Insertion Sort(삽입 정렬)
  1. 해당 *index* 값의 적절한 위치를 *index 0*부터 *index - 1* 사이에서 찾아 정렬하는 방식.

---

## Chapter 15. Graphs

### Graph

* Graph는 Node와 Node 사이의 Link로 이루어진 비선형적 자료구조다.

* Tree와 다르게 어떤 형식으로도 연결될 수 있고, 비어있을 수도 있다.

### Graph Definitions

* Undirected Graphs
  * *vertices*와 *edges*로 이루어진 유한 집합이다.
  * *edges*는 방향(direction)을 가지지 않는다.
  * *vertices*와 *edges* 둘 다 이름(Label)을 가진다.

* Directed Graphs
  * Undirected Graph와 같이 *vertices*와 *edges*로 이루어진 유한 집합이다.
  * Undirected Graph와 다르게 *edges*는 방향을 가진다.
  * Undirected Graph와 같이 *vertices*와 *edges* 둘 다 이름(Label)을 가진다.

* Loop
  * 자기 자신과 연결된 *vertex*의 *edge*.

* Path
  * *vertex*의 연속

### Graph Traversals

* Depth-First Search
  * 시작 vertex에서 이웃 vertex로 탐색을 진행하고, 또 그 이웃의 이웃으로 진행한다.
  * 더 이상 탐색을 진행할 이웃이 없을 때, 뒤로 돌아간다.
  * Stack 또는 Recursion으로 수행할 수 있다.

* Breadth-First Search
  * 시작 vertex의 모든 이웃들을 탐색하고, 이웃의 이웃을 탐색하는 방식으로 진행한다.
  * 탐색 가능한 모든 vertex에 방문했을 때 탐색이 종료된다.
  * Queue로 수행할 수 있다.