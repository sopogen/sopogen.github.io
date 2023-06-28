---
layout: post
title:  "프롬프트 엔지니어로 살아남기 - 1 필요 역량"
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
{:style="text-align:center; margin-top:0px"}
#### ***- Andrej Karpathy, 전 테슬라 AI Senior Director***
{:style="text-align:center; margin-top:0px; margin-bottom:60px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;생성형 AI는 이미 우리 삶에 깊게 침투하고 있습니다. 비단 개발자 뿐만 아니라 전문직, 사무직도 ChatGPT를 사용해서 문서 작업을 하는 모습을 쉽게 찾아볼 수 있으며, 디자이너들이 Midjourney, Stable diffusion을 사용해서 디자인 초안을 뽑아내는 것은 이제 드문 일이 아닙니다.
{:style="opacity: 0.90;"}

 생성형 AI를 잘 다루기 위해서는 AI에게 명령어를 입력해야 하는데, 이 명령어를 ***프롬프트***라고 합니다. 생성형 AI를 이용하면 코드 한줄 없이 영어로 된 명령어만으로도 실사에 가까운 그림을 뽑아내거나, 전문가가 쓴 듯한 보고서를 만들어 낼 수 있습니다. 다만 이 프롬프트를 어떻게 작성하느냐에 따라서 생성형 AI가 만들어내는 결과물의 퀄리티는 천차만별입니다. 
 {:style="opacity: 0.90;"}

 따라서 이 프롬프트를 '잘' 작성하는 것이 오늘날 중요한 능력으로 떠올랐습니다. 이렇게 영어 등의 자연어로 된 프롬프트를 잘 작성해주는 사람을 ***프롬프트 엔지니어(Prompt Engineer)*** 라고 합니다.
{:style="opacity: 0.90; margin-bottom:30px"}

![prompt1](/assets/img/2023-06-18/prompt-1.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

출처: 뤼튼테크놀로지
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

점점 더 많은 기업들이 생성형 AI를 더 잘 활용하기 위해 사내에서 프롬프트 엔지니어를 육성하거나, 심지어 채용하기 시작하고 있습니다. 해외에서도 높은 몸값에 프롬프트 엔지니어를 채용하는 것을 심심찮게 찾아볼 수 있으며, 국내에서도 점차 위와 같은 채용 공고가 올라오고 있습니다. 
{:style="opacity: 0.90;"}

 그런데 잘 생각해보면 프롬프트 엔지니어는 프로그래밍 언어를 사용하는 것도 아니고, 그저 한국어나 영어로 된 명령을 잘 하는 것 뿐입니다. 그럼에도 불구하고 왜 이렇게 많은 기업들이 필요로 하고 있으며, 높은 몸값을 주고서라도 채용하고 싶어하는 것일까요? 기업이 필요로 하는 프롬프트 엔지니어는 단순히 '영어 등 언어에 능숙한 사람'이 아니기 때문입니다. 그럼 프롬프트 엔지니어에게 필요한 역량이 도대체 무엇인지, 아래에서 확인해보도록 하겠습니다.  
{:style="opacity: 0.90; margin-bottom:70px"}
---

## 언어적 능력이 뛰어나야 한다?
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;프롬프트 엔지니어에 대해서 널리 알려진 오해는 *'프롬프트 엔지니어링은 코딩 없이 할 수 있다. 따라서 언어적 능력이 무엇보다 중요하다.'* 는 것입니다. chatGPT의 경우 잘 구조화된 언어로 프롬프트를 썼을 때, 비문으로 프롬프트를 작성한 경우보다 좋은 결과를 얻을 확률이 높습니다. 또한 다른 언어보다 영어로 썼을 때 훨씬 더 좋은 수준의 답변을 제공합니다. 
{:style="opacity: 0.90"}

따라서 언어적 능력, 특히 영어 능력이 프롬프트 엔지니어에게 있어 중요하다는 것은 틀린말이 아닙니다. 그러나 언어적 능력은 프롬프트 엔지니어에게 필요한 역량중 매우 일부일 뿐입니다. 
생성형 AI를 사용하다 보면 생성형 AI 자체에 대한 이해 없이는 해결하기 까다로운 문제들이 종종 발생합니다.  
{:style="opacity: 0.90"}

유명한 예를 통해 살펴보겠습니다. chatGPT로 123456 x 789를 계산한다고 해봅시다. 이 문제는 딱히 언어적 능력이 필요하지도 않은 쉬운 문제 같아 보입니다. 
그런데 놀랍게도, chatGPT는 정확한 결과를 내지 못합니다!
{:style="opacity: 0.90; margin-botton:70px"}

![123](/assets/img/2023-06-18/123.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}   

123456 x 789 의 정확한 결과는 97,406,784 입니다.
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

대체 이런 문제는 어떻게 해결해야 할까요? 애초에 왜 이런 일이 발생하는 걸까요? 
{:style="opacity: 0.90"}

결론부터 말하자면, GPT 모델 자체에는 산수 능력이 없기 때문이 이런 문제가 발생합니다.
GPT 모델은 학습 데이터를 참고해서, 문제와 비슷한 학습 데이터가 있다면 이에 해당하는 응답을 낼 뿐입니다.
예를 들어 학습 데이터에서 누군가가 12 x 34 = 408 이라고 했던 것을 기억했다가, 비슷한 질문이 들어오면 똑같이 대답하는 식입니다.
그런데 위와 같이 복잡한 산수는 학습 데이터에서 찾아보기 어려울 것입니다. 따라서 GPT가 제대로 된 응답을 내기 어렵습니다.
{:style="opacity: 0.90"}

따라서 위와 같은 복잡한 산수를 해결하기 위해서는, GPT 모델이 학습해봤을 만한 쉽고 작은 문제로 분해해서 물어보는 것이 필요합니다. 
예를 들어 6 x 789는 GPT가 충분히 학습했을 만한 작고 쉬운 문제입니다. 비슷하게 50 x 789도, 400 x 789도 그렇습니다.
이런 식으로 물어보면 정답을 얻어 낼 수 있습니다.  
{:style="opacity: 0.90; margin-botton:70px"}

![123-2](/assets/img/2023-06-18/123-2.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}   

이번에는 정확한 결과를 얻었습니다.
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

프롬프트 엔지니어링을 하면서 맞닥뜨리는 위와 같은 종류의 문제는 언어적인 역량으로 풀어내기 매우 어렵습니다. 
위에 설명드린 것처럼 GPT 모델 자체에 대한 최소한의 이해가 뒷받침되어야만 가능한 해결방안을 생각해볼 수 있습니다.
{:style="opacity: 0.90"}

이 뿐만 아니라, 생성형 AI의 API 서비스를 활용하기 위해서는 기본적인 프로그래밍 능력이 있어야 합니다. 또, 오픈 소스로 활용할 수 있는 모델들은 필요에 따라 직접 커스터마이징해서 사용해야 합니다. 
그리고 딥러닝 모델을 커스터마이징 하기 위해서도 **결국 모델에 대한 일정 수준 이상의 이해가 필요합니다.** 
{:style="opacity: 0.90; margin-bottom:70px"}

## 프롬프트 노하우
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;생성형 AI는 공통적으로 자연어(영어, 한글 등)을 입력으로 받아 결과를 낸다는 점에서 동일합니다. 그러나 생성형 AI에는 사실 상당히 다양한 종류가 있습니다.
- 텍스트 생성: GPT-4(ChatGPT), PALM-2(Bard)
- 이미지 생성: Midjourney, Stable Diffusion
- 음악 생성: MusicLM, MusicGen


위의 모델들은 자연어라는 비슷한 입력을 받지만, 세부적으로 원하는 바를 얻기 위해서 프롬프트 엔지니어링이 필요할 때, 각 모델들에는 **매우 다른 접근법**이 필요합니다.  
{:style="opacity: 0.90;"}

이미지 생성 모델과 텍스트 생성 모델의 프롬프트 간에는 말할 것도 없이 큰 차이가 존재하고, 같은 도메인의 생성 모델 안에서도 좋은 결과를 얻는 프롬프트는 다른 양상을 가지고 있습니다. **심지어 같은 모델이라도 버전에 따라 최적의 프롬프트가 달라질 수 있습니다.** 실제로 ChatGPT 같은 내에서도 GPT-3.5와 GPT-4 간에는 정말 큰 차이가 존재합니다.
{:style="opacity: 0.90; margin-botton:30px"}

![gpt3-bird](/assets/img/2023-06-18/gpt3-bird.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; margin-bottom:1px"}  
![gpt4-bird](/assets/img/2023-06-18/gpt4-bird.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; margin-bottom:1px"}  

위 프롬프트는 gpt-3.5에서 제대로 동작하지 않았지만, gpt-4에서는 매우 잘 동작했습니다 (심지어 운율까지 살렸습니다!)  
하지만 gpt-3.5에서도 다른 방식의 프롬프트를 써서 충분히 동일한 결과를 얻을 수도 있습니다.
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

따라서 프롬프트 엔지니어는 단순히 언어적 능력이 뛰어난 것만으로는 원하는 결과를 얻기 어렵습니다. 자신이 사용해야 하는 모델에 대해 이해하고 있으며, 각각의 모델에 대해 최적화된 프롬프트적 노하우를 알고 있어야 합니다.
{:style="opacity: 0.90;"}

{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

그렇다면 각 모델별로 최적화된 프롬프트를 사용하는 접근법은 어떻게 알아낼 수 있을까요? 각 모델에 대해 잘 이해하고 있으면 좋을까요? 안타깝게도 모델을 이해하는 것으로는 모델별로 최적의 프롬프트를 찾기에는 충분하지 않습니다. 현재 사용 중인 AI 모델의 구조를 아는 것은 어느 정도 도움이 되겠지만, 어떤 프롬프트를 사용했을 때 결과가 개선될 지는 해당 모델을 만든 당사자도 알기 어려운 정보입니다.  
{:style="opacity: 0.90;"}

![prompt2](/assets/img/2023-06-18/prompt-2.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}   

출처: Huali Ren et al(2021), Adversarial examples: attacks and defenses in the physical world
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

그렇다면 어떤 방식을 통해 최적화를 하면 좋을까요? 가장 널리 사용되는 방식은 내가 원하는 결과가 나올 때 까지 입력을 조금씩 바꿔서 넣어보는 선험적 방식, 즉 **노가다**입니다. 내가 원하는 결과가 나올 때 까지 다양한 시도를 해보는 것이죠. 
{:style="opacity: 0.90}

너무 단순해 보일지도 모르겠지만, 실제로 딥러닝 해킹 방법 중에서는 위 그림처럼 모델의 입력에 적당한 변화를 주고 출력을 관찰해서, 모델의 작동 방식을 파악하는 해킹 방법도 있습니다*(Adversarial Example)*.  프롬프트 엔지니어들도 이처럼 다양한 입력 방법들을 시도해보면서 어떤식으로 프롬프트를 잘 작성했을 때 생성형 AI가 더 나은 결과를 출력하는지를 파악해야만 합니다.
{:style="opacity: 0.90"}

물론 본인이 직접 모든 시행착오를 경험할 필요는 없습니다. 생성형 AI 별로 존재하는 **커뮤니티**를 통해서 노하우를 얻어볼 수도 있습니다. 정말 필요하다면 돈을 지불하고 프롬프트를 구매할 수도 있습니다. 
이와 같은 사이트들을 통해 얻은 프롬프트들로 더 나은 결과물을 얻을 수 있고, 더 나아가 어떤 프롬프트를 사용했을 때에 좋은 결과를 얻을 수 있는지 참조해볼 수도 있습니다.  
{:style="opacity: 0.90; margin-bottom:30px"}

![prompt3](/assets/img/2023-06-18/prompt-3.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}   

결국 단순히 모델의 이해를 넘어서 많은 실험 및 교류를 통해, 최적의 노하우를 알고 있는 것 또한 프롬프트 엔지니어에게 있어서 중요한 역량이라고도 볼 수 있겠습니다.  
(각 생성형 모델에 대한 노하우들에 대해서는 다음 시리즈에 이어서 설명하도록 하겠습니다.)  
{:style="opacity: 0.90; margin-bottom:70px"}

## 뺆의 미학
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;생성형 AI는 똑똑합니다. 잘 활용한다면 사람보다 나은 결과물을 충분히 낼 수 있습니다. 하지만 그렇다고 해서 생성형 AI가 만능이라는 말은 아닙니다. 
다양한 생성형 AI에 여러 프롬프트를 넣어보며 느낀점은, 공통적으로 **여러 가지 명령을 동시에 내릴수록 부정확한 결과를 낼 확률이 올라간다는 것입니다.**
{:style="opacity: 0.90"}

예를 들어, chatGPT를 통해서 영어 문제를 만들어 주는 간단한 서비스를 만드는 경우를 생각해보겠습니다. 
몇 가지 기능을 추가해서 좀 더 높은 수준의 문제를 만들어보고 싶습니다. 예컨대, 1. 토플 시험처럼 문제를 만들고,  2. 내가 문제를 맞추거나 틀리는 것에 따라 다음 문제의 난이도도 조정하는 기능도 추가해보고 싶습니다. 

위 요구사항을 전부 반영한 프롬프트는 아래와 같습니다. 
별도의 프로그래밍 없이, 이 프롬프트에다가 사용자의 정답만 입력하면 바로 원하는 서비스 완성입니다!

![prompt4](/assets/img/2023-06-18/prompt-4.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}   

그런데 이 프롬프트는 처음 몇 번에 대해서는 잘 작동하지만, 회차가 거듭될 수록 정확한 결과를 내지 못합니다. 
예를 들어 문제를 틀려도 그 다음에 더 어려운 문제를 준다던가, 처음에 주었던 '토플 시험처럼 문제를 만들어라' 라는 명령을 잊는다던가 하는 문제가 발생합니다.  
{:style="opacity: 0.90"}

![prompt5](/assets/img/2023-06-18/prompt-5.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}   

이전 문제를 틀렸음에도 더 어려운 문제가 나와 난이도 조절에 실패한 모습
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

그렇다면 프롬프트 엔지니어는 이런 경우에 어떻게 대처해야 할까요? 바로 **프롬프트 엔지니어링으로 해결해야 하는 문제와 아닌 문제를 분리하는 것** 입니다.
위에 언급했던 영어 문제 생성기의 사례를 다시 살펴보겠습니다.  
{:style="opacity: 0.90"}

위 사례에서는 하나의 프롬프트로 문제 형식 지정, 다음 문제 생성, 이전 문제 정답 여부에 따라 난이도 조정 등의 문제들을 한번에 해결하고자 했습니다. 
그런데 사실 이 중에서 난이도 조정 같은 경우, 생각해보면 굳이 chatGPT에게 맡기지 않아도 되는 문제입니다.  
{:style="opacity: 0.90"}

처음부터 정답을 받은 후에 사용자가 틀린 답을 입력하면 '아까 문제보다 더 쉬운 문제를 생성해줘' 라는 프롬프트를 한줄 추가하는 규칙만 있으면 되는 일입니다.
실제로 이런 식으로 접근하면 프롬프트도 훨씬 짧아지고, 이전보다 훨씬 더 잘 동작하는 것을 확인할 수 있습니다.  
{:style="opacity: 0.90"}

![prompt6](/assets/img/2023-06-18/prompt-6.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}   
새로 작성한 프롬프트
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

이처럼 프롬프트에서 AI가 해야할 일, 단순 규칙으로 할 수 있는 일을 분리해서 프롬프트를 가볍게 만드는 것도 프롬프트 엔지니어의 중요한 역량입니다.
물론 이를 수행하려면 유연하게 규칙을 세우고 생성형 AI 와 하나의 서비스 흐름으로 만들 수 있을 지를 기획하는 능력이 뒷받침되어야 합니다.
{:style="opacity: 0.90; margin-botton:70px"}


## 결론
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

프롬프트 엔지니어에게 필요한 역량은 세 줄로 요약하자면 다음과 같습니다:  
- 내가 사용할 생성형 AI 모델에 대한 이해  
- 어떤 방식으로 프롬프트를 넣으면 더 나은 결과를 얻을 수 있을 지에 대한 노하우  
- 생성형 AI에게 필요한 최소한의 일만 시키고, 나머지 일은 다른 방식으로 생성형 AI와 엮어 낼 수 있는 기획력  
{:style="opacity: 0.90"}

이번 포스팅에서는 생성형 AI 전반에 대해 필요한 역량에 대해 다루었습니다.  
다음 포스팅에서는 각 생성형 AI 별 모델에 대한 **기본적인 이해**와 원하는 결과를 얻을 수 있는 **구체적인 노하우**를 다루도록 하겠습니다.
