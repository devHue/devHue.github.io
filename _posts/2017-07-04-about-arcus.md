---
layout: post
title: "About Arcus"
description:
headline:
modified: 2017-07-04
category: Work
tags: [Arcus]
image:
  feature:
comments: true
mathjax:
---
# About Arcus

Arcus에 대한 기본적인 이해가 필요하여 작성한다.

## Arcus Cache Cloud

Arcus는 Naver Corp에서 개발한 Memcached 기반의 캐시 클라우드다. Arcus-Memcached는 Naver 서비스들의 기능 및 성능 요구 사항을 지원하도록 크게 수정되었다. Arcus는 Memcached의 기본 Key-Value 데이터 모델 외에도 구조화된 형태로 복수의 Value를 저장 및 탐색하기 위해 Collection Data Structure(List, Set, B+tree)를 지원한다.

Arcus는 ZooKeeper를 사용하여 다수의 Memcached node의 cluster를 관리한다. 각 Cluster 또는 Cloud는 각각 자신의 Service Code로 식별된다. Service Code를 Cloud의 이름이라고 생각하면 편하다. 사용자는 즉석에서 Memcached Nodes 또는 Clouds를 추가 및 제거할 수 있다. 그리고 Arcus는 자동으로 실패한 Node를 제거한다.

Arcus의 아키텍쳐는 아래 이미지에 나와있다. Memcached Node는 그들의 이름(IP Address:port number)로 식별된다. ZooKeeper는 소유하고 있는 Memcached Node의 이름과 Service Code의 데이터베이스를 관리한다. 또한, Cash List라는 각 Cloud 내의 살아있는 Node들의 리스트를 관리한다.

시작할 때, 각 Memcached Node는 ZooKeeper와 접촉하고 그들이 가진 Service Code를 찾는다. 그러면 Node는 그들의 이름을 Cash List에 삽입하고, 클라이언트가 볼 수 있게 된다. ZooKeeper는 주기적으로 Cache Node가 살아있는지 체크하고, 만약 죽었다면 해당 Node를 Cache Cloud에서 제거한 후 Cache List를 갱신하고 클라이언트에게 알린다. Arcus 클라이언트는 그 최신 Cache List를 가지고 Key-Value 오퍼레이션에 대한 Cache Node를 찾기 위해 Consistent Hashing을 한다. Hubble은 Cache Cloud의 통계 자료를 수집하고 보여준다.

![Arcus Architecture](/images/arcus-architecture.png)

## Supported OS Platform

현재 Arcus는 64-bit Linux만 지원한다. 아래의 운영체제에서 테스트 되었다.

* CentOS 6.x 64bit

* Ubuntu 12.04 LTS 64bit

만약 다른 운영체제를 지원하는 것에 관심이 있다면, 시도해보고 발생하는 이슈를 알려주면 된다.

## END

본문은 Arcus의 README를 개요 부분만 단순 해석한 것이다. 더 많은 정보를 알고 싶다면 아래의 링크를 참고하면 된다.

<https://github.com/naver/arcus>
