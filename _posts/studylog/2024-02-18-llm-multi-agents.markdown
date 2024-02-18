---
layout: post
title:  "LLM multi agent method 알아보기"
date:   2024-02-18 12:00:00 +0800
category: studylog
tags: [studylog]
comments: true
use_math: true
img:
    path: /assets/img
---
# LLM multi agent method 알아보기

## 기존 LLM agent method의 한계
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 기존의 llm based agent 방식은 LLM이 보다 다양한 기능을 수행할 수 있도록 만들었습니다. 덕분에 자료해석, 웹 검색, 계산 등 기존에 LLM 만으로 할 수 없었던 부분까지 자동화 할 수 있게 되었습니다. 
{:style="opacity: 0.90"}

다만, LLM based agent도 여러 한계점을 갖고 있습니다. 그 중 하나는 한 번 오류에 빠지기 시작하면 제대로 문제를 해결하기 어렵다는 점입니다. Agent 가 작동하는 와중에 잘못된 계획을 세우거나, 잘못 가져온 결과를 바탕으로 다음 프로세스를 진행하려고 하는 경우, 이를 고치지 못하고 그대로 잘못된 결과까지 도출하는 경우가 대부분입니다.  
{:style="opacity: 0.90"}


또 다른 문제점은, 여전히 매우 복잡한 문제는 해결하지 못한다는 점입니다. 간단한 프로그래밍은 가능하지만, 여러 개의 파일을 구현해야 하는 프로그래밍은 여전히 잘 수행하지 못합니다. 그 외에 보고서 작성 등의 복합적인 task에서도 제대로 된 결과물을 생성하기는 다소 어렵습니다.
{:style="opacity: 0.90"}

## Multi-agent의 등장
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Multi-agent 방식은 하나의 task를 수행하기 위해 여러 개의 agent를 활용하는 방식입니다. 여러 개의 역할이 다른 agent들을 구성하여 서로 다른 관점에서 task를 수행하도록 만들고, 이 agent들 끼리 상호작용을 통해 결과를 만들어냅니다. 어떻게 보면 회사에서 여러 직무의 사람들이 모여서 상호작용하며 업무를 수행하는 것과 동일한 맥락이라고 볼 수 있겠습니다.   
{:style="opacity: 0.90"}

Multi-agent 방식을 사용하게 되면 agent의 추론 과정에서 문제가 생기더라도, 다른 agent가 상호작용을 통해 이를 바로잡을 수 있습니다. 또한 매우 복잡하고 어려운 task도 각각의 agent들이 역할을 나눠서 수행하기 떄문에, 좀 더 잘 해결해 낸다는 장점이 있습니다.
{:style="opacity: 0.90"}

![multi-agents-1](/assets/img/2024-02-18/multi-agents-1.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

Xi, Zhiheng, et al. "The rise and potential of large language model based agents: A survey." (2023).
{:style="text-align:center; opacity: 0.60; margin-bottom:60px; font-size: 12px"}

Multi-agent 방법론은 크게 두 가지로 나누어집니다. 여러 개의 agent들이 서로 협력해서 최종 결과를 만들어 내는 **Cooperative Engagement (협동적 참여)** 방식과 상충하는 agent들이 서로 상호작용하여 합의에 이르도록 하는 **Adversarial Interactions (적대적 상호작용)** 방식입니다.
{:style="opacity: 0.90; margin-bottom:80px;"}

---
## Cooperative Engagement (협동적 참여)
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Cooperative Engagement (협동적 참여) 방식은 현재 가장 널리 사용되는 multi-agent 방식입니다. 이름에서부터 알 수 있다시피, 별개의 agent들이 서로 협력하여 문제를 해결하는 방식입니다. 
{:style="opacity: 0.90"}

아래 예시는 voting 을 이용해 간단한 multi-agent 협동적 참여를 구현한 논문입니다. 법관의 역할을 수행하는 별개의 agent 3개를 만들고, 각 agent의 판단을 다수결의 원칙에 따라 종합하여 최종 결론을 내립니다.
{:style="opacity: 0.90"}

![multi-agents-2](/assets/img/2024-02-18/multi-agents-2.png){: width="400"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

Hamilton, Sil. "Blind Judgement: Agent-Based Supreme Court Modelling With GPT." 2023
{:style="text-align:center; opacity: 0.60; margin-bottom:80px; font-size: 12px"}  

Microsoft에서 발표한 Autogen은 이러한 협동적 참여 방식의 multi-agent system을 쉽게 구현할 수 있는 framework 입니다. 그림에서 보는 것 처럼 각각의 task를 풀기 위해서 다양한 구조의 협동 방식을 커스터마이징 할 수 있습니다.
{:style="opacity: 0.90"}


![multi-agents-3](/assets/img/2024-02-18/multi-agents-3.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

Wu, Qingyun, et al. "Autogen: Enabling next-gen llm applications via multi-agent conversation framework." (2023)  
{:style="text-align:center; opacity: 0.60; margin-bottom:80px; font-size: 12px"}



---
## Adversarial Interactions (적대적 상호작용)
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  앞의 협동적 참여 방식은 각각의 agent 가 서로 다른 역할을 수행하며 다양한 기능을 수행할 수 있는 장점이 있었습니다. 그러나 하나의 agent 에서 환각 현상이 발생하면, 그 agent 와 협동하는 다른 agent도 그 환각 현상의 영향을 받게 되는 단점이 있습니다.  
{:style="opacity: 0.90"}

Adversarial Interactions (적대적 상호작용) 방식은 비교적 최근 도입된 multi-agent 시스템입니다. 앞의 협동적 참여 방식과는 달리, 서로 상충하는 여러 agent들이 논쟁해가며 합의에 이르도록 하는 방식으로 agent들을 협동시킵니다.  
{:style="opacity: 0.90"}

![multi-agents-5](/assets/img/2024-02-18/multi-agents-5.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

Du, Yilun, et al. "Improving Factuality and Reasoning in Language Models through Multiagent Debate." arXiv preprint arXiv:2305.14325 (2023)  
{:style="text-align:center; opacity: 0.60; margin-bottom:60px; font-size: 12px"}

위 그림은 가장 간단한 적대적 상호작용 방식인 Multi-agent Debate 입니다. 위 논문에서는 어떤 문제를 풀기 위해 서로 다른 방식으로 문제를 푸는 agent 1, 2를 준비합니다. Round 1에서는 agent들이 각자 문제를 풉니다. Round 2에서 agent 1에는 agent 2가 round 1 에서 푼 결과를 참고하고, Agent 2는 agent 1이 푼 결과를 참고하도록 합니다. 이렇게 두 agent가 합의될 때 까지 위 과정을 반복해서 최종 결과를 내는 방식입니다.
{:style="opacity: 0.90"}

위와 같은 방식을 사용하게 되면 agent들끼리 의사소통하는 데에 기존보다 훨씬 더 많이 LLM이 사용됩니다. 따라서 시간이나 컴퓨팅 자원이 많이 사용됩니다. 하지만 agent들에서 환각이 발생하더라도 이를 여러 단계의 토론을 통해서 수정할 수 있고, 복잡한 문제에서도 정확한 답을 얻을 확률이 높아지는 확실한 장점이 있습니다.

## References
* Xi, Zhiheng, et al. "The rise and potential of large language model based agents: A survey." arXiv preprint arXiv:2309.07864 (2023).
* Hamilton, Sil. "Blind Judgement: Agent-Based Supreme Court Modelling With GPT." The AAAI-23 Workshop on Creative AI Across Modalities. 2023.
* Wu, Qingyun, et al. "Autogen: Enabling next-gen llm applications via multi-agent conversation framework." arXiv preprint arXiv:2308.08155 (2023)
* Du, Yilun, et al. "Improving Factuality and Reasoning in Language Models through Multiagent Debate." arXiv preprint arXiv:2305.14325 (2023)