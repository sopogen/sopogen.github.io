---
layout: post
title:  "ChatGPT 20배 잘쓰기"
subtitle: "프롬프트 엔지니어 시리즈 3편"
date:   2023-07-16 12:00:00 +0800
category: studylog
tags: [studylog]
comments: true
use_math: true
img:
    path: /assets/img
---
![quotes](/assets/img/quotation_mark.jpeg){: width="30"}{:style="display:block; margin-left:auto; margin-right:auto; margin-bottom:3px"}

## ChatGPT는 몇몇 분야를 제외하고는, 믿기 힘들 만큼 제한적이다.(limited)
{:style="text-align:center; margin-top:0px"}
#### ***- Sam Altman, CEO of OpenAI.***
{:style="text-align:center; margin-top:0px; margin-bottom:60px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ChatGPT는 정말 많은 것들을 해낼 수 있습니다. 일반적인 지식은 물론 의학, 법학과 같은 전문적인 지식도 잘 대답해냅니다.
하지만 ChatGPT를 사용해서 어떤 서비스를 만든다고 하면, 여전히 여러가지 한계점들이 존재합니다. 
{:style="opacity: 0.90;"}

예를 들어 똑같은 질문을 물어봐도 매번 답변이 달라지기 때문에, 어떤 규칙에 따라 프로그래밍을 할 때 문제가 될 수 있습니다. 
그리고 한번에 입력할 수 있는 문자의 수가 제한적이기 때문에, 긴 문서등에 대해 한번에 물어보기가 어렵습니다.
{:style="opacity: 0.90;"}

그러나 최근 이런 ChatGPT의 한계를 여러가지 방법으로 없앨 수 있는 방법들이 속속 등장하고 있습니다.
이번 포스팅에서는 ChatGPT의 한계를 극복하고 서비스에 활용할 수 있도록 도와주는 몇 가지 방법들을 소개합니다.
{:style="opacity: 0.90; margin-bottom:70px"}
---

## ChatGPT API
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

## Sematic search
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

## LangChain
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ChatGPT가 사용하는 GPT-3.5, GPT-4 모델은 스스로 생각하고 계산하는 능력이 없습니다. 단지 학습된 대화에 따라, 이 맥락에서는 어떤 대화가 나오는 것이 좋을 지를 확률적으로 예측하는 것입니다. 따라서 ChatGPT를 사용할 때에는 많이 쓰일 만한 방식으로 질문을 던지는 것이 좋습니다.
{:style="opacity: 0.90; margin-bottom:50px"}

#### 한글보다 영어가 낫다
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}
ChatGPT는 다양한 언어를 처리할 수 있지만, 그중에서도 영어를 사용할 때 가장 높은 성능을 보입니다. 이는 ChatGPT가 주로 영어 데이터로 학습되었기 때문입니다. 다른 언어, 예를 들어 한국어를 사용할 때에는, 모델이 언어의 복잡성을 완전히 이해하지 못할 가능성이 있습니다. 특히나 일반적인 대화에서 잘 안쓰이는 속담, 사자성어 등이 들어갔을 때 더욱 어려워합니다. 따라서 가능하면 영어를 사용하여 프롬프트를 입력하면 더 나은 결과를 얻을 수 있습니다.
{:style="opacity: 0.90; margin-bottom:50px"}

![[prompt-korean](/assets/img/2023-07-01/prompt-korean.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  
![[prompt-english](/assets/img/2023-07-01/prompt-english.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

#### 많이 있을 법한 방식으로 물어봐라
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}
ChatGPT는 단순한 질문 뿐만 아니라 프로그래밍, 의학, 수학, 법학 등과 같은 전문 분야의 질문도 곧잘 대답할 수 있습니다. 그런데 각 전문분야, 특히 수학에 대해 세세하게 물어볼 수록 정답을 모르거나 잘못된 정답을 말하는 정답인 것 처럼 말하는 이른바 **환각(Hallucination)현상**이 일어나기 쉽습니다. 
{:style="opacity: 0.90}

이 경우에 사용할 수 있는 방법 중 한가지는 바로 많이 있을 법한 방식으로 물어보는 것입니다. 예를 들어 복잡한 수학 문제를 푼다고 하면, 그것을 한번에 물어보는 것 보다 각각의 작은 단위의 문제로 물어본 후에, 이를 다시 합치도록 하는 것이 정답을 얻을 확률이 높습니다. 예를 들어 이전 포스팅에서 소개한 것처럼 123456 x 789를 계산하라고 하면, ChatGPT는 일반적인 방식으로는 정답을 맞추지 못합니다. (6 x 789) + (50 x 789) ... 와 같이 더 많이 있을 법한 작은 문제로 나눠서 주는 것이 정답을 얻을 수 있는 방식입니다.
{:style="opacity: 0.90}

![123](/assets/img/2023-06-18/123.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}   
![123-2](/assets/img/2023-06-18/123-2.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"} 

이 때, 어투 또한 해당 분야에서 자주 사용되는 방식으로 물어보는 것이 좋습니다. 만약 코드를 질문한다면 stackoverflow나 github issue처럼, 수학의 경우 stackexchange에 질문하는 것처럼 물어보세요! 위의 경우에도 문제를 낼 때 방정식의 형태로 제공하면 문제를 잘 해결하는 것을 확인했습니다. 그러나 같은 방식이라도 아래와 같이 언어를 많이 포함해서 제공하면 오히려 정답을 잘 맞추지 못합니다.

![123-3](/assets/img/2023-07-01/123-3.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px; margin-bottom:70px"}   


## GPT는 많은 내용이 들어간다
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ChatGPT를 이용할 때 한번에 보낼 수 있는 대화의 길이는 제한되어 있습니다. 그래서 보통 ChatGPT는 한번에 보낸 대화만큼의 입력만 들어간다고 생각하기가 쉽습니다. 그러나 그렇지 않습니다. ChatGPT에게 한번 질문을 입력하면, 그 질문을 포함해서 한 chat 내에 쌓인 나의 모든 질문과 ChatGPT의 모든 답변이 다시 ChatGPT 모델의 입력으로 주어지게 됩니다. 
{:style="opacity: 0.90}

따라서 ChatGPT가 앞의 대화의 맥락을 파악할 수 있는 이유는, 앞에 나왔던 모든 대화를 다시 GPT 모델의 입력으로 넣기 때문입니다. 이 부분을 인지하고 있다면, ChatGPT에게 좀 더 현명한 방식으로 명령을 내릴 수 있습니다. 아래의 예시들은 이러한 특성을 이용하여 좀 더 좋은 결과를 얻을 수 있는 방법들입니다.
{:style="opacity: 0.90}

#### 무한히 대화할 수 없다
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}
위에서 말했다시피 ChatGPT와 나눴던 대화 내용은 매번 대화를 나눌 때마다 전부 다시 ChatGPT의 입력으로 주어집니다. 따라서 내가 짧은 문장으로 질문하더라도, 여러 번의 대화를 거쳐왔다면 ChatGPT 모델이 한번에 처리해야 하는 대화의 양은 어느 순간 상당히 많아집니다. 
{:style="opacity: 0.90}

이렇게 많은 입력을 넣을 경우에는 입력 길이 제한에 걸릴 수 있습니다. ChatGPT에 한번에 입력할 수 있는 대화의 길이는 GPT-3.5 기준으로 4096 토큰, GPT-4 기준으로 8192 토큰입니다. 여기서 토큰은 GPT가 소화하는 최소한의 단위입니다. [이 링크](https://platform.openai.com/tokenizer)에서 간단하게 내가 입력하는 문장이 몇 토큰인지 확인해볼 수 있습니다.
{:style="opacity: 0.90}

일반적으로 영어의 경우 75단어당 100토큰 정도로 이루어져 있습니다. 문제는 한글인데요, 한글의 경우 한 글자당 2-3개의 토큰이 사용됩니다. 따라서 영어보다 훨씬 빠르게 토큰이 소모되고, 이론상 2000자 정도의 대화가 오고가면 끝나는 양입니다.
{:style="opacity: 0.90}
![hello](/assets/img/2023-07-01/hello.png){: width="400"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}   
![hello-kor](/assets/img/2023-07-01/hello-kor.png){: width="400"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

동일한 음절의 단어더라도 영어로 'hello'를 입력하면 1개의 토큰으로 인식되지만, 한글로 '안녕하세요'를 입력하면 14개의 토큰으로 인식됩니다.
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}


어찌되었든 전체 대화의 길이가 제한되어 있기 때문에, 제한에 걸리지 않기 위해서는 좀 더 효율적으로 대화를 할 필요가 있습니다. 예를 들어 같은 대화 내에서 질문했던 이전 대화내용을 참조할 경우에는, "이전에 했던 ~~에 대한 내용 말인데.." 와 같이 간단하게 물어보는 것이 더 효율적입니다. 또 만약 대화 길이 제한을 초과했다면, 새 대화를 열고 최근 2-3 개의 질문과 응답을 새 대화의 입력으로 넣는 방법도 있습니다.
{:style="opacity: 0.90}

물론 위와 같은 방법은 ChatGPT 서비스를 사용할 떄의 임시 방편이며, 이런 방법을 통해서는 논문이나 긴 보고서 등을 ChatGPT에게 입력하는데에는 여전히 제한이 있습니다. 간단한 프로그래밍을 통해 이를 본격적으로 해결하는 방법론에 대해서는 다음 포스트에서 다루도록 하겠습니다.
{:style="opacity: 0.90}


#### 시스템 설정을 이용하라
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}
위에서 말한 것처럼, ChatGPT는 매번 이전의 모든 대화를 입력으로 받습니다. 그래서 사용자가 맨 처음에 어떤 대화를 나누고, 이후에 더 많은 대화를 나눌수록 이것이 점점 희석되어 나중에는 이에 대한 내용을 잘 대답하지 못할 수 있습니다.
{:style="opacity: 0.90}

그런데 ChatGPT가 응답할 때마다 매번 어떤 규칙에 따라 응답하도록 만들고 싶을 때가 있습니다. 이런 경우에는 어떻게 해야 할까요? 바로 가장 처음에 ChatGPT에게 'You are helpful data scientist', '~~처럼 생각해라' 라는 식으로 역할을 정해주는 것입니다. 
{:style="opacity: 0.90}

이 방식은 그냥 대화를 나누는 것과는 어떻게 다를까요? ChatGPT 상에서는 보이지 않지만 실은 사용자가 ChatGPT에게 내리는 명령은 내부적으로 두 가지 방식으로 나누어집니다. 하나는 user, 하나는 system입니다. 일반 user로써 나누는 대화는 대화가 축적됨에 따라 희석될 수 있지만, system으로서 내린 명령은 ChatGPT에게 매번 출력 규칙으로서 적용됩니다. 
{:style="opacity: 0.90}

![chatgpt-playground](/assets/img/2023-07-01/chatgpt-playground.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}   

ChatGPT 사이트가 아닌 [이 링크](https://platform.openai.com/playground)를 통해 들어가면, system 메시지와 user 메시지가 분리되어 있음을 볼 수 있습니다.
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

그런데 위와 같이 'You are...' 를 포함하는 명령어는 ChatGPT에게 system 명령으로 전달됩니다. 따라서 많은 대화를 나누더라도 ChatGPT가 system 명령에 따라 일관성 있는 방식으로 대답하도록 할 수 있습니다.
{:style="opacity: 0.90}

## GPT는 그자리에서 배운다
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}
위에서 말씀드린 것처럼, ChatGPT는 질문을 던지면 그 다음에 나올 대답 중 가장 높은 확률을 가지는 단어로 대답합니다. 그말인 즉슨 가장 일반적이고 많이 나올법한 방식으로만 대답한다는 것입니다. 그런데 만약 특수한 문제를 푼다고 할 때에는 


#### 고기 잡아주기
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}


#### 고기 잡는 법 가르치기
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}


---
## 결론
다음에는 단순 프롬프트가 아니라 프로그램 내에 어떤식으로 사용할 수 있을지 알랴줌
플러그인 + API 

## References -->