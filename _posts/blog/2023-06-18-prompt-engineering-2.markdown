---
layout: post
title:  "ChatGPT 500배 잘쓰기"
subtitle: "프롬프트 엔지니어 시리즈 2편"
date:   2023-06-18 12:00:00 +0800
category: studylog
tags: [studylog]
comments: true
use_math: true
img:
    path: /assets/img
---
![quotes](/assets/img/quotation_mark.jpeg){: width="30"}{:style="display:block; margin-left:auto; margin-right:auto; margin-bottom:3px"}
## ChatGPT는 무서울 정도로 뛰어나다(scary good)
{:style="text-align:center; margin-top:0px"}
#### ***- Elon Musk***
{:style="text-align:center; margin-top:0px; margin-bottom:60px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ChatGPT는 첫 등장 이후, 전 세계 업무의 패러다임을 바꿔버렸습니다. 많은 사람들은 궁금한 것이 있으면 이제 검색 엔진 대신 ChatGPT를 사용합니다. 코드가 필요할 땐 stack overflow 대신 사용합니다. 보고서를 쓸 때도, 소설을 쓸 때도, 어떤 글이건 좋은 초안을 작성해줄 수도 있습니다.  
{:style="opacity: 0.90;"}

 ChatGPT의 뛰어난 점 중 하나는 바로 어떤 식으로 질문해도 웬만하면 어떻게든 대답한다는 것입니다. 질문에 뭔가 빠져있으면 다시 물어봐주기도 하고, 스스로 질문의 의도를 유추해서 대답해주기도 합니다. 하지만 그러다보니 의도를 잘못 파악해서 정확히 사용자에게 필요한 대답을 하지 못할 때도 많습니다. 
 {:style="opacity: 0.90; margin-bottom:50px"}

![error-prompt](/assets/img/2023-06-18/error-prompt.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

이번 포스팅에서는 어떻게 프롬프트를 써야 ChatGPT가 더 좋은 결과를 내도록 할 수 있을 지를 알아봅니다. ChatGPT 공식 문서와 커뮤니티에서 유명한 노하우들, 그리고 제 개인의 노하우를 참고하였습니다.
{:style="opacity: 0.90; margin-bottom:70px"}
---

## 학습된 모델이다
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}
ChatGPT가 사용하는 GPT-3.5, GPT-4 모델은 스스로 생각하고 계산하는 능력이 없습니다. 단지 학습된 대화에 따라, 이 맥락에서는 어떤 대화가 나오는 것이 좋을 지를 확률적으로 예측하는 것입니다. 따라서 ChatGPT를 사용할 때에는 많이 쓰일 만한 방식으로 질문을 던지는 것이 좋습니다. 아래에는 그 예시를 들어드리겠습니다.
{:style="opacity: 0.90; margin-bottom:50px"}

### 한글보다 영어가 낫다
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}
ChatGPT는 다양한 언어를 처리할 수 있지만, 그중에서도 영어를 사용할 때 가장 높은 성능을 보입니다. 이는 ChatGPT가 주로 영어 데이터로 학습되었기 때문입니다. 다른 언어, 예를 들어 한국어를 사용할 때에는, 모델이 언어의 복잡성을 완전히 이해하지 못할 가능성이 있습니다. 특히나 일반적인 대화에서 잘 안쓰이는 속담, 사자성어 등이 들어갔을 때 더욱 어려워합니다. 따라서 가능하면 영어를 사용하여 프롬프트를 입력하면 더 나은 결과를 얻을 수 있습니다.
{:style="opacity: 0.90; margin-bottom:50px"}

![[prompt-korean](/assets/img/2023-07-01/prompt-korean.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  
![[prompt-english](/assets/img/2023-07-01/prompt-english.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

### 많이 있을 법한 방식으로 물어봐라
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}
ChatGPT는 단순한 질문 뿐만 아니라 프로그래밍, 의학, 수학, 법학 등과 같은 전문 분야의 질문도 곧잘 대답할 수 있습니다. 그런데 각 전문분야, 특히 수학에 대해 세세하게 물어볼 수록 정답을 모르거나 잘못된 정답을 말하는 정답인 것 처럼 말하는 이른바 **환각(Hallucination)현상**이 일어나기 쉽습니다. 
{:style="opacity: 0.90}

이 경우에 사용할 수 있는 방법 중 한가지는 바로 많이 있을 법한 방식으로 물어보는 것입니다. 예를 들어 복잡한 수학 문제를 푼다고 하면, 그것을 한번에 물어보는 것 보다 각각의 작은 단위의 문제로 물어본 후에, 이를 다시 합치도록 하는 것이 정답을 얻을 확률이 높습니다. 예를 들어 이전 포스팅에서 소개한 것처럼 123456 x 789를 계산하라고 하면, ChatGPT는 일반적인 방식으로는 정답을 맞추지 못합니다. (6 x 789) + (50 x 789) ... 와 같이 더 많이 있을 법한 작은 문제로 나눠서 주는 것이 정답을 얻을 수 있는 방식입니다.
{:style="opacity: 0.90}

![123](/assets/img/2023-06-18/123.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}   
![123-2](/assets/img/2023-06-18/123-2.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"} 

이 때, 어투 또한 해당 분야에서 자주 사용되는 방식으로 물어보는 것이 좋습니다. 만약 코드를 질문한다면 stackoverflow나 github issue처럼, 수학의 경우 stackexchange에 질문하는 것처럼 물어보세요! 위의 경우에도 문제를 낼 때 방정식의 형태로 제공하면 문제를 잘 해결하는 것을 확인했습니다. 그러나 같은 방식이라도 아래와 같이 언어를 많이 포함해서 제공하면 오히려 정답을 잘 맞추지 못합니다.

![123-3](/assets/img/2023-07-01/123-3.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px; margin-bottom:70px"}   


## 모든 것을 기억한다
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}
ChatGPT를 이용할 때 한번에 보낼 수 있는 대화의 길이는 제한되어 있습니다. 그래서 보통 ChatGPT는 한번에 보낸 대화만큼의 입력만 들어간다고 생각하기가 쉽습니다. 그러나 그렇지 않습니다. ChatGPT에게 한번 질문을 입력하면, 그 질문을 포함해서 한 chat 내에 쌓인 나의 모든 질문과 ChatGPT의 모든 답변이 다시 ChatGPT 모델의 입력으로 주어지게 됩니다. ChatGPT는 이런 식으로 나와의 대화의 맥락을 파악하는 것입니다.
{:style="opacity: 0.90}

이 부분을 인지하고 있다면, ChatGPT에게 좀 더 현명한 방식으로 명령을 내릴 수 있습니다. 아래의 예시들은 이러한 특성을 이용하여 좀 더 좋은 결과를 얻을 수 있는 방법들입니다.
{:style="opacity: 0.90}

### 구체적이되 많이 시키진 마라
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}
위에서 말했다시피 ChatGPT와 나눴던 대화 내용은 매번 대화를 나눌 때마다 전부 다시 ChatGPT의 입력으로 주어집니다. 따라서 내가 짧은 문장으로 질문하더라도, 여러 번의 대화를 거쳐왔다면 ChatGPT 모델이 한번에 처리해야 하는 대화의 양은 어느 순간 상당히 많아집니다. 
{:style="opacity: 0.90}

## 시스템 설정
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}
위에서 말한 것처럼, ChatGPT는 매번 이전의 모든 대화를 입력으로 받습니다. 그래서 사용자가 맨 처음에 어떤 대화를 나누고, 이후에 더 많은 대화를 나눌수록 이것이 점점 희석되어 나중에는 이에 대한 내용을 잘 대답하지 못할 수 있습니다.
{:style="opacity: 0.90}

그런데 ChatGPT가 응답할 때마다 매번 어떤 규칙에 따라 응답하도록 만들고 싶을 때가 있습니다. 이런 경우에는 어떻게 해야 할까요? 바로 맨 처음에 ChatGPT에게 '~~~ 처럼 생각해라', '~~~ 처럼 행동해라' 라는 식으로 페르소나를 정해주면 됩니다. 
{:style="opacity: 0.90}

이 방식은 그냥 대화를 나누는 것과는 어떻게 다를까요? ChatGPT에게는 동일한 명령을 내리는 것 처럼 보이지만, 실은 사용자가 ChatGPT에게 내리는 명령은 두 가지 방식으로 나누어집니다. 하나는 user, 하나는 system입니다. 일반 user로써 나누는 대화는 대화가 축적됨에 따라 희석될 수 있지만, system으로서 내린 명령은 ChatGPT에게 매번 출력 규칙으로서 적용됩니다. 그런데 위와 같이 '~~~ 처럼 생각해라' 를 포함하는 명령어는 ChatGPT에게 system 명령으로 전달됩니다. 따라서 많은 대화를 나누더라도 ChatGPT가 일관성 있는 방식으로 대답하도록 할 수 있습니다.
{:style="opacity: 0.90}

<!-- # 똑똑하다

## In-context learning
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

## 포맷화
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}


---
## 결론
다음에는 단순 프롬프트가 아니라 프로그램 내에 어떤식으로 사용할 수 있을지 알랴줌
플러그인 + API 

## References -->