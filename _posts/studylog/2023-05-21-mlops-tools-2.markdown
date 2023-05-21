---
layout: post
title:  "MLops를 위한 데이터 관리"
date:   2023-05-21 12:00:00 +0800
category: studylog
tags: [studylog]
comments: true
use_math: true
img:
    path: /assets/img
---
![quotes](/assets/img/quotation_mark.jpeg){: width="30"}{:style="display:block; margin-left:auto; margin-right:auto; margin-bottom:3px"}
## Garbage in, garbage out.
{:style="text-align:center; margin-top:0px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 머신러닝 성능을 높이기 위한 방법은 아주 다양합니다. 지금 수행중인 과제에 더 적합하도록 모델 아키텍쳐를 수정하거나, 여러가지 하이퍼파라미터를 조정해볼 수도 있습니다. 이 과정은 많은 고민과 실험을 필요로 하고, 결과적으로 머신러닝 모델의 성능을 높일 수 있을지에 대해서는 불투명합니다. 하지만 어떤 경우에서던 간에 반드시 모델의 성능을 높일 수 있는 방법이 있습니다. 바로 *좋은 데이터를 많이 구해서* 훈련시키는 것입니다.
{:style="opacity: 0.90"}

한편 반대로 생각해보면, 아무리 뛰어난 머신러닝 모델을 사용한다 하더라도 안좋은 데이터나 적은 데이터만 사용해서 모델을 학습시킨다면 제대로 작동하지 않는다는 말입니다. 컴퓨터 과학에서 유명한 문구인 Garbage in, Garbage out 도 이러한 상황을 말한다고 볼 수 있습니다. 따라서 머신러닝 모델을 활용한 서비스를 구상할 때, 가장 중요하게 생각해야할 것 중 하나는 바로 대량의, 양질의 데이터를 구하고 이를 잘 관리하는 것입니다. 오늘은 이 방법에 대해 개괄적으로 알아보도록 하겠습니다.
{:style="opacity: 0.90; margin-bottom:70px"}

---

## 1. 데이터 저장
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

#### 파일 시스템

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **파일 시스템**은 컴퓨터에서 데이터를 저장, 조직, 접근하는 방법을 정의하는 가장 기본적인 시스템입니다. 기본 단위는 텍스트 또는 이진 파일이고, 쉽게 덮어쓸 수 있습니다. 파일 시스템은 일반적으로 컴퓨터에 연결된 **디스크**(온프레미스 서버에 물리적으로 연결되어 있거나 클라우드에 연결되어 있음)에 있습니다.

디스크는 하드 디스크에서 SSD에 이르기까지 데이터 전송 속도와 대역폭이 다양합니다. 같은 SSD 내에서도 디스크 가장 느린 디스크(SATA SSD)와 가장 빠른 디스크(NVMe SSD) 사이에는 상당한 속도 차이가 있습니다.  다음은 각 디스크 및 상황 별 자료 전송에 걸리는 시간에 대한 그래프입니다. 
{:style="opacity: 0.90"}

![mlops-2-2](/assets/img/2023-05-21/mlops-2-2.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"} 
출처: fullstackdeeplearning
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}


#### 스토리지
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**스토리지**는 파일 시스템을 통한 API입니다. 기본 단위는 일반적으로 이진 형식(이미지, 사운드 파일, 텍스트 파일 등)의 개체입니다. 스토리지 서비스에 버전 관리 기능을 구축할 수 있습니다. 로컬 파일 시스템만큼 빠르지는 않지만 클라우드 내에서 충분히 빠르게 실행할 수 있습니다.

#### 데이터베이스
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터베이스는 영구적이고 빠르고 확장 가능한 스토리지인 동시에 구조화된 데이터 시스템입니다. 이를 위한 유용한 정신적 모델은 데이터베이스가 보유한 모든 데이터가 실제로 컴퓨터의 RAM에 있지만 데이터베이스 소프트웨어는 컴퓨터가 꺼져도 모든 것이 디스크에 안전하게 유지되도록 보장한다는 것입니다. RAM에 데이터가 너무 많으면 디스크로 확장됩니다.  
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이진 데이터를 저장할 때에는 데이터베이스에 저장하지 말고 스토리지 URL에 저장해야 합니다. 대부분의 경우 Postgres가 좋은 선택입니다. 비정형 JSON 및 해당 JSON을 통한 쿼리를 지원하는 오픈 소스 데이터베이스입니다. SQLite는 소규모 프로젝트에도 완벽하게 적합합니다.  
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;서로 참조하는 객체의 컬렉션을 다루는 대부분의 코딩 프로젝트는 결국 형편없는 데이터베이스를 구현합니다. 처음부터 데이터베이스를 사용하면 시간을 절약할 수 있습니다. 실제로 대부분의 MLOps 도구는 핵심 데이터베이스입니다(예: W&B - 실험 데이터베이스, HuggingFace Hub - 모델 데이터베이스, Label Studio - 라벨 데이터베이스).  
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**데이터 웨어하우스**는 온라인 트랜잭션 처리(OLTP)를 위한 데이터 저장소인 데이터베이스와 달리 온라인 분석 처리(OLAP)를 위한 저장소입니다. ETL(Extract-Transform-Load)이라는 프로세스를 통해 데이터를 데이터 웨어하우스로 가져옵니다: 여러 데이터 원본을 지정하면 데이터를 추출하여 균일한 스키마로 변환한 후 데이터 웨어하우스에 로드할 수 있습니다. 웨어하우스에서 비즈니스 인텔리전스 쿼리를 실행할 수 있습니다. OLAP와 OLTP의 차이점은 OLAP는 열 지향적인 반면 OLTP는 행 지향적이라는 것입니다.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**데이터 레이크**는 여러 소스의 데이터를 비정형으로 취합한 것입니다. 데이터 웨어하우스와 데이터 웨어하우스의 주요 차이점은 데이터 레이크가 모든 데이터를 버리고 나중에 특정 요구에 맞게 변환하는 ELT(Extract-Load-Transform) 프로세스를 사용한다는 것입니다. 큰 추세는 데이터 레이크와 데이터 웨어하우스를 통합하여 정형 데이터와 비정형 데이터를 함께 사용할 수 있도록 하는 것입니다. 이를 위한 두 가지 큰 플랫폼은 Snowflake와 Databricks입니다.

---

## 2. 데이터 탐색
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

![mlops-2-3](/assets/img/2023-05-21/mlops-2-23png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"} 
출처: fullstackdeeplearning
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터를 탐색하려면 해당 언어(대부분 SQL)를 사용해야 하며 점차 DataFrame이 사용됩니다. SQL은 수십 년 동안 존재해온 구조화된 데이터의 표준 인터페이스입니다. Pandas는 SQL과 같은 작업을 수행할 수 있는 Python 에코시스템의 주요 DataFrame입니다. 우리의 조언은 트랜잭션 데이터베이스와 분석 창고 및 호수와 상호 작용할 수 있도록 둘 다 유창하게 하는 것입니다. Pandas는 Python 데이터 과학의 핵심입니다. DASK DataFrame을 사용하여 코어를 통한 Panda 작업을 병렬화하고 RAPIDS를 사용하여 GPU를 통한 Panda 작업을 수행할 수 있습니다.
{:style="opacity: 0.90"}

## 3. 데이터 처리
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

![mlops-2-4](/assets/img/2023-05-21/mlops-2-4.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"} 
출처: fullstackdeeplearning
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;데이터 처리의 경우 필요한 기능들을 몇 가지 예시를 통해 살펴볼 수 있습니다. 매일 사진의 인기도를 예측하는 머신러닝 모델을 훈련시켜야 한다고 가정해 보겠습니다. 각 사진에 대해 교육 데이터는 다음을 포함해야 합니다:  
{:style="opacity: 0.90"}

1. 데이터베이스에 있는 메타데이터(예: 게시 시간, 제목 및 위치).  
2. 로그에서 계산해야 하는 사용자의 일부 기능(예: 오늘 로그인 횟수).  
3. 내용과 스타일 같은 사진 분류기의 출력.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;궁극적인 목표는 사진 인기 예측 모델을 훈련시키는 것이지만, 우리는 데이터베이스에서 데이터를 출력하고, 로그를 계산하고, 예측 결과를 출력하기 위해 모델을 실행해야 합니다. 결과적으로 작업 의존성이 있습니다. 일부 작업은 다른 작업이 완료될 때까지 시작할 수 없으므로 작업을 마치면 종속성이 시작됩니다. 이 종속성은 파일이 아니라 프로그램 및 데이터베이스이기도 합니다. 이 작업을 많은 서버에 분산시키고 많은 의존성 그래프를 동시에 실행할 수 있어야 합니다.  
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Airflow는 Python의 표준 스케줄러로, Python 코드를 사용하여 작업의 DAG(방향 비순환 그래프)를 지정할 수 있습니다. 해당 그래프의 연산자는 SQL 연산 또는 Python 함수일 수 있습니다. 이러한 작업을 배포하기 위해 워크플로 관리자는 태스크에 대한 대기열을 가지고 있으며 태스크에서 가져온 작업자를 관리합니다. 작업이 실패하면 작업이 다시 시작되고 작업이 완료되면 사용자에게 ping을 전송됩니다.  
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;여기서 가장 중요한 조언은 일을 지나치게 Overengineering을 하지 말라는 것입니다. 요즘은 CPU 코어와 RAM이 많은 기계를 쉽게 구할 수 있습니다. 예를 들어, UNIX는 강력한 병렬 처리, 스트리밍 및 고도로 최적화된 도구를 제공합니다.  
{:style="opacity: 0.90"}
