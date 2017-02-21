---
layout: post
title: "Using Tweets to Predict the Stock Market"
description: "졸업작품을 위한 논문 번역 및 분석"
headline: 
modified: 2017-02-16
category: thesis
tags: [thesis]
image: 
  feature: 
comments: true
mathjax: 
---

# Using Tweets to Predict the Stock Market

author : Zhiang Hu, Jian Jiao, Jialu Zhu

## 1. Abstact

우리는 이 프로젝트를 통해 영향력 있는 트위터 유저와 그에 해당하는 하나의 주식 가격 움직임 사이의 관계를 찾아내려 한다.

우리가 사용할 데이터는 Tesla의 CEO인 Elon Musk의 트윗들과 Tesla의 주식 가격이다.

[SVM](https://en.wikipedia.org/wiki/Support_vector_machine)(Support Vector Machine) Model을 사용하여 다양한 시도를 할 것이다.

## 2. Background

영향령 있는 트위터 유저들의 트윗은 특정 주식 가격에 영향을 미칠 수 있다는 것을 발견했다.

예를 들어, 최근에 유명한 전기 자동차 회사인 Tesla의 주식은 자율 주행에 대한 Elon Musk(Tesla CEO)의 트윗이 업데이트 되고 난 후에 크게 상승했다.

게다가, AP(Associated Press) 통신의 트위터 계정이 백악관에서 폭발이 있을 것이라는 거짓 트윗을 올리고 난 후 다우 존스와 S&P 500 지수는 1%가 하락했다.

## 3. Prior Work

트위터나 다른 SNS을 이용한 주식 시장 예측에 대한 연구는 많이 존재한다.

2010년에, Bollen et al.은(는) Self-Organizing Fuzzy Neural Network와 Google Profile of Mood States(GPOMS)와 트위터 데이터를 사용하여 87.6%의 정확도로 DJIA 이동 방향을 예측했다.

그들은 "Calm" Mood Profile이 주식 시장 예측을 위한 최적의 결과를 산출한다는 것을 발견했다.

## 4. Methods

### 4.1 Data Process

* 4.1.1 Tweet Data
  * 이 프로젝트의 첫 과제는 트위터에게서 데이터를 가져오는 것이다. 과거 연구에 사용된 데이터들은 트위터의 개인 정보 보호 정책으로 인해 더는 사용이 불가능하다.
  * 그러므로, 트위터 계정의 트윗 내용과 favorite 수, 리트윗 수를 가져오기 위해 Tweepy(트위터 개발자 도구)를 사용해야 한다.
  * 특정 유저에게서 최대 3200개의 트윗 정보를 수집할 수 있다.
  
## 5. Analysis

* SVM?
  * Support Vector Machine의 약자로, 기계 학습의 분야 중 하나다.
  * 패턴 인식, 자료 분석을 위한 지도 학습 모델이며, 주로 분류와 회귀 분석을 위해 사용한다.
  * 우리가 원하는 결과를 위해서 어떤 분석 알고리즘을 써야 하는지, 다른 알고리즘도 찾아보자.
* Tweepy?
  * Twitter API에 쉽게 접근하게 도와주는 Python Library이다.
  * 다른 논문에서는 Twitter API에 어떻게 접근했는지 살펴보자.