---
layout: post
title: "Jekyll 설정하기"
description: 
headline: 
modified: 2017-02-02
category: jekyll
tags: [jekyll]
image: 
feature: 
comments: true
mathjax: 
---

# Jekyll 설정하기

Jekyll을 설정하는 것은 생각보다 고통스럽다.

## Jekyll

* 간단하고 블로그스러운 정적 웹페이지 생성기
* 가장 큰 이점은 GitHub를 통해 Page, Blog 또는 WebSite를 무료로 호스팅 할 수 있음

## 요구사항(Requirements)

* GNU/Linux, Unix 또는 MacOS
* Ruby 버전 2.0 이상
* RubyGems
* GCC와 Make

## 설정하기(Set-Up)

### 운영체제(OS)

운영체제는 여러 가지가 있지만 우분투 16.04 LTS가 기타 패키지들이 최신이어서 선택함

* [Ubuntu 16.04 LTS](https://www.ubuntu.com/download/desktop)

### Ruby 설치

Ruby와 Ruby-dev 둘 다 필요함

```bash
sudo apt-get install ruby ruby-dev
```

### RubyGems

RubyGems는 Ruby를 설치 한 후 다음 명령어를 실행

```bash
sudo gem update --system
```

### GCC와 Make

GCC와 Make는 Ubuntu Desktop 버전을 설치해다면 자동으로 설치되어 있음

설치 여부가 궁금하다면 다음 명령어를 실행

```bash
gcc -v
make -v
```

Server 버전에는 포함된 패키지가 아니므로 다음 명렁어 실행

```bash
sudo apt-get install gcc
sudo apt-get install make
```

### Jekyll과 Bunlder Gem 설치

```bash
sudo gem install jekyll bundler
```

## 블로그(Blog) 설정하기


### Quick Start

Jekyll이 기본으로 제공해주는 템플릿으로 Jekyll을 처음 이용한다면 알고 가는 개념으로 실행해도 무방함

```bash
jekyll new myblog # ./myblog에 새 jekyll 사이트 생성
cd myblog         # myblog 디렉토리로 이동
bundle install    # Gemfile과 Gemfile.lock에 설정된 Gem들을 설치
jekyll serve      # https://localhost:4000에서 확인 가능
```

### 이미 만들어진 Theme 사용하기

* [jekyllthemes.org/](jekyllthemes.org)
* [https://jekyllthemes.io](https://jekyllthemes.io)
* [themes.jekyllrc.org/](themes.jekyllrc.org/)

위 링크에서 마음에 드는 Theme을 골라 repository를 clone한 후, 다음 명령어 실행

```bash
bundle install    # Gemfile과 Gemfile.lock에 설정된 Gem들을 설치
jekyll serve      # https://localhost:4000에서 확인 가능
```

## 소감

* Jekyll을 처음 접한다면 환경설정이 조금 어려움
* 원하는 Theme이 없다면 직접 만들어야 하지만, Jekyll의 철학에 맞는 기능을 가진 Theme은 여럿 존재함. 디자인이 문제.
* 설치와 삭제를 반복하여 이틀만에 원하는 Theme 적용 성공
* 적용 후에는 Markdown에 익숙하다면 포스팅하는 것에는 문제가 없음
* 내가 적용한 Theme은 hmfaysal의 [Omega Theme](https://github.com/hmfaysal/hmfaysal-omega-theme).
* **Specially Thanks to hmfaysal!!**
