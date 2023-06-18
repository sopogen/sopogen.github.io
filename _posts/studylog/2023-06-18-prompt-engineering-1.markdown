---
layout: post
title:  "프롬프트 엔지니어란"
date:   2023-06-18 12:00:00 +0800
category: studylog
tags: [studylog]
comments: true
use_math: true
img:
    path: /assets/img
---
![quotes](/assets/img/quotation_mark.jpeg){: width="30"}{:style="display:block; margin-left:auto; margin-right:auto; margin-bottom:3px"}
## 새로운 프로그래밍 언어 중 가장 인기있는 것은 **영어**다
{:style="text-align:center; margin-top:0px;}
#### ***- Andrej Karpathy, 전 테슬라 AI lead***
{:style="text-align:center; margin-top:0px; margin-bottom:60px"}

 생성형 AI는 더 이상 이미 우리 삶에 깊게 침투하고 있습니다. 비단 개발자 뿐만 아니라 전문직, 사무직도 ChatGPT를 사용해서 문서 작업을 하는 모습을 쉽게 찾아볼 수 있으며, 디자이너들이 Midjourney, Stable diffusion을 사용해서 이미지를 뽑아내는 것은 이제 드문 일이 아닙니다.
{:style="opacity: 0.90;"}

 생성형 AI를 잘 다루기 위해서는 AI에게 명령어를 잘 입력해야 하는데, 이 명령어를 프롬프트라고 합니다. 이 프롬프트를 어떻게 작성하느냐에 따라서 생성형 AI가 만들어내는 퀄리티는 천차만별입니다. 따라서 이 프롬프트를 '잘' 작성하는 것이 중요해졌는데, 이렇게 프롬프트를 잘 작성해주는 사람을 ***프롬프트 엔지니어(Prompt Engineer)*** 라고 합니다.
{:style="opacity: 0.90;"}

![prompt1](/assets/img/2023-06-18/prompt-1.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"} 
출처: wrtn
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

 점점 더 많은 기업들이 생성형 AI를 더 잘 활용하기 위해 프롬프트 엔지니어를 육성하거나, 심지어 채용하기 시작하고 있습니다. 해외에서도 높은 몸값에 프롬프트 엔지니어를 채용하는 것을 심심찮게 찾아볼 수 있으며, 국내에서도 점차 위와 같은 채용 공고가 올라오고 있습니다. 
{:style="opacity: 0.90;"}

 그런데 한편으로는 이런 생각도 들 수 있습니다. 프로그래밍 언어를 사용하는 것도 아니고, 그저 한국어나 영어로 주문을 잘 하는 것 뿐인데 왜 이렇게 많은 기업들이 필요로 하고 있으며 저렇게 웃돈을 주고서라도 데려가고 싶어하는 것일까요? 아래 내용을 통해 프롬프트 엔지니어에게 필요한 역량이 무엇인지도 확인해보도록 하겠습니다.   
{:style="opacity: 0.90; margin-bottom:70px"}
---

## 단순히 언어의 문제는 아니다.
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

 일반적으로 생성형 AI에게 투입하는 명령어를 전부 '프롬프트'라고 통칭합니다. 그런데 생성형 AI에는 사실 상당히 다양한 종류가 있습니다.
- 텍스트 생성: GPT-4(ChatGPT), PALM-2(Bard)
- 이미지 생성: Midjourney, Stable Diffusion
- 기타: Musicgen(음악)    


물론 위의 생성형 AI는 자연어(영어, 한글 등) 을 입력으로 받아 결과를 낸다는 점에서는 동일합니다. 그러나 세부적으로 원하는 바를 얻기 위해서 프롬프트 엔지니어링이 필요할 떄, 각 모델들에는 **매우 다른 접근법**이 필요합니다.  
{:style="opacity: 0.90;"}

이미지 생성 모델과 텍스트 생성 모델의 프롬프트 간에는 말할 것도 없이 큰 차이가 존재하고, 같은 도메인의 생성 모델 안에서도 좋은 결과를 얻는 프롬프트는 다른 양상을 가지고 있습니다. **심지어 같은 모델이라도 버전에 따라 최적의 프롬프트가 달라질 수 있습니다.** 실제로 GPT-3.5 모델을 사용한 ChatGPT와 GPT-4가 사용가능한 ChatGPT Pro 간에는 정말 큰 차이가 존재합니다.
{:style="opacity: 0.90;"}

따라서 프롬프트 엔지니어는 자신이 사용하고자 하는 각각의 모델에 대해 최적화된 프롬프트적 접근법을 알고 있어야 합니다. 만약 다양한 모델을 사용하게 된다면 각 모델의 특성은 무엇인지, 각 모델에는 어떤 방식으로 프롬프트를 작성해야 원하는 결과를 얻을 수 있을지 등을 파악하고 최적의 결과를 뽑아낼 수 있어야 합니다.
{:style="opacity: 0.90;"}

## 노가다
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

그렇다면 각 모델별로 최적화된 프롬프트를 사용하는 접근법은 어떻게 알아낼 수 있을까요? 각 모델에 대해 잘 이해하고 있으면 좋을까요? 안타깝게도 모델을 이해하는 것으로는 모델별로 최적의 프롬프트를 찾기에는 충분하지 않습니다. 현재 사용 중인 AI 모델의 구조를 아는 것은 어느 정도 도움이 되겠지만, 어떤 프롬프트를 사용했을 때 결과가 개선될 지는 해당 모델을 만든 당사자도 알기 어려운 정보입니다. 특히 최근 대부분의 대규모 생성형 AI의 경우 모델 구조를 비공개하고 있기 떄문에, 모델 자체로 부터 정보를 얻기 어렵습니다.
{:style="opacity: 0.90;"}

![prompt2](/assets/img/2023-06-18/prompt-2.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"} 
출처: Huali Ren et al(2021), Adversarial examples: attacks and defenses in the physical world
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

그렇다면 어떤 방식을 통해 최적화를 하면 좋을까요? 가장 즐겨 사용되는 방식은 '선험적 방식', 즉 **노가다**입니다. 내가 원하는 결과가 나올 때 까지 다양한 시도를 해보는 것이죠. 너무 단순해 보일지도 모르겠지만, 실제로 딥러닝 해킹 방법 중에서는 위 그림처럼 입력에 적당히 작은 변화를 주고 모델의 출력을 관찰해서, 모델의 작동 방식을 파악하는 해킹 방법도 있습니다***(Adversarial Example)***. 프롬프트 엔지니어들도 이처럼 다양한 입력 방법들을 시도해보면서 어떤식으로 프롬프트를 잘 작성했을 때 생성형 AI가 더 나은 결과를 출력하는지를 파악해야만 합니다.
{:style="opacity: 0.90; margin-bottom:70px"}
