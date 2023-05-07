---
layout: post
title:  "MLops를 위한 개발 도구 - 1"
date:   2023-05-07 12:00:00 +0800
category: studylog
tags: [studylog, python]
comments: true
use_math: true
img:
    path: /assets/img
---
![quotes](/assets/img/quotation_mark.jpeg){: width="30"}{:style="display:block; margin-left:auto; margin-right:auto; margin-bottom:3px"}
## 딥러닝 서비스에서 딥러닝 모델은 극히 일부일 뿐이다.
{:style="text-align:center; margin-top:0px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;딥러닝 서비스를 만든다고 하면 우리는 화려한 구조의 SOTA(State Of The Art: 최첨단) 모델이나, 초거대 AI 모델 등에 대해 생각하게 됩니다. 그러나 현실에서는, 딥러닝 서비스를 만드는데 있어서 딥러닝 모델은 그렇게 중요하지 않을 수도 있습니다. 모델 보다는 데이터를 수집하고, 처리하고, 라벨을 붙이는 작업 등이 훨씬 더 중요할 수도 있습니다. 
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;딥러닝 모델을 들여다 보더라도, 단순히 모델 아키텍쳐가 중요한 것이 아닙니다. 어떻게 모델을 지속적으로 디버깅할 것인지, 어떻게 결과를 모니터링할 것인지, 어떻게 배포할 것인지에도 중요합니다.
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;결과적으로 딥러닝 서비스를 만들기 위해서 아래와 같이 여러 요소가 필요하고, 다양한 도구를 사용해서 이런 요소들을 좀 더 쉽게 통제할 수 있습니다. 딥러닝 서비스를 만들기 위한 요소들은 크게 데이터, 모델 개발, 배포 총 3가지로 나눠볼 수 있습니다. 
{:style="opacity: 0.90"}

![mlops-1](/assets/img/2023-05-07/mlops-1.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"} 
출처: fullstackdeeplearning
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;본 포스트에서는 모델 개발에 해당하는 요소에서 어떤 작업이 필요하고, 각 작업에 어떤 개발 도구가 필요한지에 대해 짚어봅니다.
{:style="opacity: 0.90; margin-bottom:70px"}

---

## 1. 딥러닝 프레임워크
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

#### 프레임워크

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 딥러닝 프레임워크는 딥러닝 개발을 쉽게 수행하기 위해 미리 세팅된 프레임워크입니다. 이 프레임워크들의 주요 역할은 numpy 처럼 행렬연산을 쉽게 수행한다거나 하는 곳에 있지 않습니다. CUDA 위에 코드를 배포하여 딥러닝에 GPU를 쉽게 사용할 수 있게 해주고, 표준과 다른 optimizer나 데이터 인터페이스를 쉽게 커스터마이징하여 사용할 수 있다는 데에 장점이 있습니다.
{:style="opacity: 0.90"}

![mlops-2](/assets/img/2023-05-07/mlops-2.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"} 
출처: fullstackdeeplearning
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;딥러닝 프레임워크는 PyTorch, TensorFlow, Jax 등 다양한 종류가 있습니다. 이 세가지는 여러가지 배포 환경(CPU, GPU, TPU, 모바일)에 대해 최적화된 딥러닝을 수행한다는 공통점이 있습니다.
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Pytorch**는 그 중에서도 가장 널리 쓰이는 프레임워크 입니다. 디테일한 커스터마이징을 구현하는 데에 강점이 있으며, 2021 ML competition 우승자의 약 77%가 PyTorch를 사용했다고 합니다.
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Tensorflow**는 PyTorch 수준의 많은 이용자를 확보하고 있고, 여러가지 유용한 기능을 제공합니다. TensorFlow.js를 통해 웹 브라우저에서 딥러닝 모델을 학습시킬 수 있고, Keras를 통해서 매우 간단하게 개발할 수도 있습니다.
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Jax**는 최근 부상하고 있는 프레임워크로, 기존 프레임워크에 비해 실행속도가 빠르고 numpy 수준에서 코딩이 가능하다는 장점이 있습니다. 다만 딥러닝을 위해서는 Flax나 Haiku와 같은 추가적인 프레임워크를 사용해야 합니다.
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**FastAI**는 어떤 프레임워크보다 손쉽게 딥러닝 모델을 구현할 수 있습니다. 간단한 모듈 또는 API 형태로 딥러닝 모델의 모든 요소를 쉽게 만들 수 있습니다.
{:style="opacity: 0.90"}

#### Model zoo

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 딥러닝을 수행할 떄에는 대부분의 경우 누군가 이미 훈련한 모델 가중치를 사용하거나, 이미 개발한 모델 아키텍쳐를 수정하는 형태로 개발을 진행합니다. 따라서 이런 모델 가중치나 아키텍쳐를 가져올 수 있는 여러가지 방식도 필요합니다.
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **ONNX**는 딥러닝 모델을 저장하기 위한 표준입니다. 한 프레임워크에서 저장한 모델 가중치를 다른 프레임워크에서 사용가능하게 해줍니다. 
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **TIMM**은 SOTA ComputerVision 모델 아키텍쳐 및 모델 가중치를 다운 받을 수 있는 라이브러리 입니다.
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **HuggingFace**는 모델 아키텍쳐 및 가중치를 저장하는 가장 큰 웹 저장소입니다. 6만개가 넘는 다양한 모델 가중치를 다운 받을 수 있습니다. HuggingFace에서 제공하는 Transformers 라이브러리를 활용하면 업로드된 가중치를 코드 상에서 바로 다운 받아 사용할 수 있습니다.
{:style="opacity: 0.90; margin-bottom:70px"}

---


## 2. 분산 훈련
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;딥러닝 모델을 훈련시킬 때에는 GPU를 활용해서 훈련하는 경우가 많습니다. 이 때 필요한 GPU의 스펙이나 개수를 정하기 위해서는, 1. 얼마나 큰 데이터 배치를 사용하는지 2. 얼마나 많은 모델 파라미터를 사용하는지 의 2가지를 고려해야 합니다.
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;가장 좋은 경우는 GPU 한대로도 모든 데이터 배치와 모델 parameter를 충분히 학습시킬 수 있는 경우입니다. 이 경우 더 이상 늘릴 수 없을 때 까지 데이터 배치 사이즈를 늘려볼 수 있습니다.
{:style="opacity: 0.90"}

#### 데이터 병렬화
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;그런데 만약 모델은 충분히 학습가능하나, 데이터 배치가 하나의 GPU로 훈련시키기 어려운 경우, 데이터 병렬화를 시도해야 합니다. 
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PyTorch는 DistributedDataParallel 모듈을 통해 데이터 병렬 처리를 제공합니다. 한편 Horovod와 같은 써드파티 프레임워크를 사용해서 병렬처리를 진행할 수도 있습니다. Pytorch Lightening 을 사용하면 위 두가지 옵션 중 하나를 매우 간단하게 적용할 수 있습니다.
{:style="opacity: 0.90"}

#### 데이터 병렬화(Data Parallelism)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;그런데 만약 모델은 충분히 학습가능하나, 데이터 배치가 하나의 GPU로 훈련시키기 어려운 경우, 데이터 병렬화를 시도해야 합니다. 
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PyTorch는 DistributedDataParallel 모듈을 통해 데이터 병렬 처리를 제공합니다. 한편 Horovod와 같은 써드파티 프레임워크를 사용해서 병렬처리를 진행할 수도 있습니다. Pytorch Lightening 을 사용하면 위 두가지 옵션 중 하나를 매우 간단하게 적용할 수 있습니다.
{:style="opacity: 0.90"}

#### Sharded Data Parallelism
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;한편, 데이터 뿐만 아니라 모델도 하나의 데이터 GPU 내에서 학습하기 어려운 경우도 있습니다. 이 경우 Sharded data parallelism을 적용하는 것을 고려해볼 수 있습니다.
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;샤딩(Sharding)은 데이터베이스에서 사용되는 개념으로, 하나의 데이터 소스를 여러 분산된 시스템으로 조각내어 저장하는 방법입니다. 최근 마이크로소프트에서는 ZeRO라는 방법을 통해 딥러닝 모델의 계산을 sharding 하여, 메모리 사용량을 10배까지 줄이는 방식을 제안했습니다. 
{:style="opacity: 0.90"}

![mlops-3](/assets/img/2023-05-07/mlops-3.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"} 
출처: fullstackdeeplearning
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Microsoft의 Deepspeed 라이브러리를 통해 Sharded data parallelism 을 구현할 수 있습니다. Pytorch 내에서도 Fairscale 라이브러리를 통해 구현할 수 있으며, 단일 GPU내에서도 위와 같은 ZeRO 방식을 적용할 수 있습니다.
{:style="opacity: 0.90"}

#### 파이프라인 모델 병렬화(Pipeline Model Parallelism)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 모델 병렬화는 모델의 각 레이어를 각 GPU에 배치하는 것을 의미합니다. DeepSpeed 및 FairScale 라이브러리는 각 레이어에 해당하는 GPU가 완전히 활용되도록 계산을 파이프라인화하여 더 나은 성능을 제공합니다.
{:style="opacity: 0.90"}

![mlops-4](/assets/img/2023-05-07/mlops-4.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"} 
출처: fullstackdeeplearning
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;위에 소개한 3가지 병렬화 방식은 각각 딥러닝 파이프라인의 다른 부분에서 작용합니다. 따라서 GPT-3와 같이 초거대규모 딥러닝 모델을 훈련시키기 위해서는 위에 소개된 3가지 방식을 전부 사용할 수도 있습니다. 
{:style="opacity: 0.90"}

## References
[Full-stack deep learning](https://fullstackdeeplearning.com/course/2022/)