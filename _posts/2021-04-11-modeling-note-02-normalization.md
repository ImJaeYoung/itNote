---
title:  "관계형 데이터 모델링 노트 : 02 정규화 이야기"
search: false
categories:
  - Data Modeling
tags:
  - Data
  - Data Modeling
  - Modeling
  - 관계형 데이터 모델링 노트
  - 데이터 모델링
  - 정규화
  - Normalization
---
<br/>
# Chapter 2 : 정규화 이야기

## 서론
  * "관계형 데이터 모델링 노트" 책을 통해 진행한 이론 스터디 두번째 시간이다. 모델링을 진행하면서 제일 중요한게 엔티티를 정의하는것이다. 엔티티라는 것은 "어떤것"을 얘기하는데 이때 어떤 것이란, 사람또는 사물같이 유형적인 것 뿐만 아니라 개념같은 무형적인 것도 포함이 된다.
  <br/>
  <br/>
  * 엔티티 정의를 정확하게 하기 위해서는 그 엔티티가 가지고 있는 특성/성격(속성/관계)을 잘 정의해야 된다.
  <br/>
  그래서 엔티티가 잘 정의 되었는지 확인하는 것이 중요한데, 이런한 기법이 정해져 있는것이 없다. 왜냐하면 보는 시각이나 관리하고자 하는 정보의 수준에 따라 엔티티 정의가 달라질 수 있기 때문이다.
  <br/>
  그래도 실무적인 차원에서는 이 정규화를 통해서 일괄적으로 엔티티 정의를 명확하게 할 수 있다.

  <br/>
  ![image-center](/assets/images/2021-04-11_normalization.png){: .align-center}

  [출처 : https://velog.io/@bsjp400]

## 정규화에 대한 서설

  * 정규화와 통합화는 모델링의 꽃이다.
  <br/>

  * 일반적으로 정규화는 순서대로 진행되지 않는다. 상향식 방법이면 속성을 제거 하면서 정규화가 수행되고, 하향식 방법이면 생각하는 과정을 거치면서 3, 4 정규화가 수행된다.
  <br/>

  * 정규화는 업무 요건에 종속되어 있다. 정규화를 업무 요건에 맞도록 수행하는 것이지, 요건과 무관하게 최대한 분해하는 것이 정규화는 아니다.
  <br/>

## 정규화란?

  * 칸토어의 집합의 정의에서 **<U>"서로 명확히 구별"</U>** 이라는 내용이 있다. 이는 정규화와 관련되어 있다. 정규화는 식별자를 통해 유사한 속성들을 모으고, 종속되지 않는 독립적인 속성들을 분해한다. 이 과정을 통해 서로(**엔티티**) 명확히 구별한다.
  <br/>

  * **"정규화를 간단하게 표현하자면 속성을 제자리에 위치 시키는 것이다."**
  <br/>

  * 관계형 데이터 모델이 도려면 속성의 종속성과 의존성을 분석해 더는 분해될 수 없는 엔티티로 만드는 정규화 과정을 반드시 거쳐야 한다.
  <br/>

  * **정규화는 데이터를 완전히 이해하는 과정이다.** 정규화는 데이터를 분석하고 정의하는 과정이므로, 정규화를 한다는 것은 모델링을 한다는 것과 동일한 개념이다.
  <br/>

  * **더 이상 추가할 속성이 없는 모델보다, 제거할 속성이 없는 모델이 완벽한 모델이다.**
  <br/>

## 함수 종속이란?
  * 데이터 종속성
    - 데이터 종속성에는 함수 종속과 다가 종속, 조인 종속, 파생 종속 등이 존재한다.
    - 그 집합을 대표하는 속성과 나머지 속성 사이의 연관 관계가 함수 종속이다.
    - 함수 종속은 업무 조건에 종속된다. 이를 통해 업무 조건이 달라지면 함수 종속 또한 변경될 수 있다는 것을 알 수 있다.

## 결정자와 종속자
  * 속성간의 종속성을 분석할 때 기준이 되는 값을 **결정자**라고 한다. 그리고 결정자의 값에 의해 정해질 수 있는 값을 종속자라고 한다.

## 함수 종속과 폐포
  * 함속 종속은 키와 밀접한 연관이 있다. 왜냐하면 함수 종속에 결정자가 키가 되도록 릴레이션을 분해하는 과정이 정규화이기 때문이다.
  <br/>

  * 폐포는 X에 종속되었다고 추론할 수 있는 모든 속성의 집합을 의미한다. 즉 X -> (Y,Z)라면 X의 폐포는 X자신과 Y와 Z이다.

## 정규화 하면 좋아지는 것
  * **1) 완전성**
    - 정규화의 가장 커다란 목적 중의 하나는 중복 데이터를 제거하는 것이다. 중복 데이터를 사용하지 않으면 불완전한 데이터를 발생시키는 아노말리(이상)가 생기지 않아 데이터 무결성과 데이터 품질이 좋아진다.
    <br/>
    <br/>

  * **2) 확장성**
    - 정규화를 하면 모델의 확장성이 좋아진다. 정규화를 통해 비 식별자 속성을 주 식별자에 종속시키면 데이터가 명확해진다. 데이터 정체성이 그대로 반영된 모델 구조에서는 업무가 수정되거나, 추가되어도 엔티티에 반영하기 수월해진다.
    <br/>

## 아노말리(Anomaly)
  * 아노말리는 데이터 이상현상이다. 데이터가 서로 맞지 않는 아노말리는 중복 데이터 때문에 발생한다.
  <br/>

  * **1) Update Anomaly**
    - 릴레이션에서 속성의 값을 업데이트할 때 발생하는 데이터 이상 현상.
    <br/>

  * **2) Delete Anomaly**
    - 릴레이션에서 인스턴스를 삭제할 때 발생하는 데이터 이상 현상.
    <br/>

  * **3) Insert Anomaly**
    - 릴레이션에 새로운 인스턴스를 삽입할 때 발생하는 데이터 이상 현상.
    <br/>

## 정규형과 비정규형
  * 정규형과 비정규형의 특징
    - **1) 비정규형**
      - 업무 요건의 변경에 매우 취약하다. 즉 모델의 확장성이 좋지 않다.
      - 인덱스 수가 증가하고, 속성을 종으로 보여주는 화면에 대한 쿼리가 복잡해진다.
      - 반복 속성이 추가될 가능성이 없을때 사용할 수 있다.
      - 전체 속성 레벨로 관리 되므로 해당 데이터의 자식 엔티티를 가질 수 없다.
      <br/>

    - **2)정규형**
      - 업무 요건의 변경에 유연하다. 즉 확장성이 좋은 모델이다.
      - 인덱스 수가 감소하고, 속성을 횡으로 보여주는 화면에 대한 쿼리가 복잡해진다.
      - 반복 속성이 추가될 가능성이 존재할 때 사용한다.
      - 인스턴스 레벨로 관리 되므로 데이터의 자식 엔티티를 가질 수 있다.
      <br/>

## 정규형 유형
  * **1) 제 1 정규형**
    - 모든 속성은 반드시 하나의 값을 가져야 한다.
    - 1 정규화와 관련된 속성은 다가 속성과 복합성이 있다. 다가 속성은 하나의 값을 가져야 되는 부분과 연관이 있고, 다가 속성은 같은 종류의 값을 여러 개 가지는 속성을 의미한다.
    - 이때 하나의 값(속성)은 업무적으로 의미가 있는 값으로 봐야 된다.
    <br/>

    - **정규형 대상**
      - 다가 속성이 사용된 릴레이션
      ![image-center](/assets/images/2021-04-11_01_normalization_01.jpg){: .align-center}
      <br/>

      - 복합 속성이 사용된 릴레이션(ex: 고객성명을 성과 명으로 나눌 수 있다.)
      ![image-center](/assets/images/2021-04-11_01_normalization_02.jpg){: .align-center}
      <br/>

      - 유사한 속성이 반복된 릴레이션
      ![image-center](/assets/images/2021-04-11_01_normalization_03.jpg){: .align-center}
      <br/>

      - 중첩 릴레이션(하나의 인스턴스 내부에 다시 인스턴스가 존재하는 형태의 릴레이션)
      ![image-center](/assets/images/2021-04-11_01_normalization_04.jpg){: .align-center}
      <br/>

  * **2) 제 2 정규형**
    - **부분 함수 종속 제거**
    - 릴레이션의 모든 속성이 후보 식별자 전체에 종속적이면 제 2 정규형이다. 만약에 일반 속성 중에 후보 식별자 전체에 종속되지 않고 일부에 종속된 속성이 있다면 제 2 정규형이 아니다.
    ![image-center](/assets/images/2021-04-11_02_normalization_01.jpg){: .align-center}
    <br/>

  * **3) 제 3 정규형**
    - **이행적 함수 종속 제거**
    - 식별자가 아닌 일반 속성 간에 종석성이 존재하면 안된다.
    ![image-center](/assets/images/2021-04-11_03_normalization_01.jpg){: .align-center}
    <br/>

  * **4) BC 정규형**
    - BC 정규형은 3 정규형 보다 엄격한 정규형이다.
    - 모든 결정자는 주 식별자이어야 한다.
    ![image-center](/assets/images/2021-04-11_BC_normalization_01.jpg){: .align-center}
    <br/>

  * **5) 제 4 정규형**
    - **다가 속성(MD: Multivalued Dependency)** 개념에 기반되는 정규형이다.
    - 두개의 다가 속성 값 사이에 다대다 관계가 발생하면, 다가 종속되었다고 한다.
    - 하나의 A 값에 대응하는 여러 개의 B값이 있고 A 값에 대응하는 여러 개의 C 값이 있으며, B 값과 C 값 사이에는 아무런 상관 관계가 없는데 A, B, C 값을 하나의 릴레이션으로 관리할 때 다가 종속이 발생한다.
    ![image-center](/assets/images/2021-04-11_04_normalization_01.jpg){: .align-center}
    <br/>

    ![image-center](/assets/images/2021-04-11_04_normalization_03.jpg){: .align-center}
    <br/>

    ![image-center](/assets/images/2021-04-11_04_normalization_02.jpg){: .align-center}
    <br/>

  * **6) 제 5 정규형**
    - 5 정규형은 조인 종속 개념을 기반으로 수행된다.
    <br/>

    - 어떤 릴레이션을 분해한 다음에 조인해서 다시 원래의 릴레이션으로 복원할 수 있다면, 그 릴레이션은 조인 종속이 존재하는 릴레이션이다.
    <br/>

    - 5 정규형은 더는 분해할 수 없는 릴레이션으므로 가장 이상적인 정규형이지만, 데이터를 하나의 릴레이션에서 관리해도 아노말리 현상이 발생하지 않기 때문에 조인종속이 발생하는 상태로 릴레이션을 관리하는 것이 현실적이다.
    <br/>

    - 5 정규형은 지나치게 이론적이며 이상적인 정규형이다. DBMS에서 실제로 사용하는 것은 적합하지 않지만, 다른 정규형과 구분하기 위해서는 알아야 하는 정규형이다.
    <br/>

    ![image-center](/assets/images/2021-04-11_05_normalization_01.jpg){: .align-center}
    <br/>

## 정규화 요약
  * 아래 표를 통해서 정규화에 대한 요약을 정보를 볼수 있다.
  <br/>
  ![image-center](/assets/images/2021-04-11_normalization_summary.jpg){: .align-center}

## 정규형와 성능
  * 정규형의 단점이 오직 성능 저하에만 있는 것은 아니다. 간혹 정규형을 이해 못해서 데이터를 엉뚱하게 다루는 경우도 있다.
  <br/>
  * 정규형이 성능이 나빠지는 원리를 조회할 때 사용하는 블록이 늘어나서 그렇다고 하지만, 오히려 블록 하나에 여러개의 로우를 위치 시킬 수 있어 메모리 적중률이 높일 수 있다.
  <br/>
  * 정규형은 비 정규형에 비해서 쓰기 성능이 좋다.