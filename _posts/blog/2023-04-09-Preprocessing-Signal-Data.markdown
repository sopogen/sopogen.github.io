---
layout: post
title:  "신호 데이터 전처리 in Python"
date:   2023-04-09 12:00:00 +0800
category: studylog
tags: [studylog, python]
comments: true
use_math: true
img:
    path: /assets/img
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;신호 데이터라고 하면, 일반적으로는 음성 데이터를 가장 먼저 떠올립니다. 하지만 음성 데이터 이외에도 우리는 신호 속에 살고 있다고 해도 될 만큼 다양한 형태의 신호 데이터가 존재합니다. **시간에 따라 변화하는 모든 데이터는 신호 데이터로 볼 수 있기 때문입니다.** 따라서 생체 신호(뇌파, 심전도 등), 소리 데이터(금속 가공음 등) 뿐만 아니라, 주식 데이터, 온도 데이터 등도 하나의 신호 데이터로 볼 수 있습니다.  
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;그 유형이 다양한 만큼, 각각의 신호 데이터는 서로 다른 전처리를 필요로 합니다. 그러나 모든 신호 데이터에 통용될 수 있는 아주 기본적이고 핵심적인 전처리 방식이 존재합니다. 바로 신호를 주기가 다른 여러 개의 신호로 분리하여 분석하는 방식입니다. 이런 방식을 ***시간-주파수 분석(Time-frequency analysis)*** 이라고 합니다. 이번 포스팅에서는 시간-주파수 분석에 해당하는 기본적인 신호 데이터 전처리 방식들을 소개합니다.
{:style="opacity: 0.90; margin-bottom:70px"}

![quotes](/assets/img/quotation_mark.jpeg){: width="30"}{:style="display:block; margin-left:auto; margin-right:auto; margin-bottom:3px"}
## 모든 신호는 간단한 신호들의 합으로 나타낼 수 있다.
{:style="text-align:center; margin-top:0px; margin-bottom:30px"}

우선 시간-주파수 분석이 왜 필요한지 부터 살펴보겠습니다. 우리가 보게 되는 신호의 형태는 아래와 같이 복잡한 형태입니다. (높은 확률로 이것보다 더 복잡한 형태입니다.)
![signaly](/assets/img/2023-04-09/signal_y.png){: width="800"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이렇게 복잡하게 생긴 신호는 패턴을 파악하기도 어렵고, 그로부터 특징을 추출하기도 어렵습니다. 그런데 사실 이 신호는 일정한 주기를 가지는 규칙적인 신호들이 합쳐진 신호입니다. 아래 보시는 것 처럼 좀 전의 신호는 제가 사인파 3개를 합쳐서 만들어 낸 신호입니다. 
{:style="opacity: 0.90"}
![signaly1y2y3](/assets/img/2023-04-09/signal_y1y2y3.png){: width="800"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이렇게 나눠서 보면 처음의 복잡한 신호보다 훨씬 더 패턴을 파악하기 쉽고, 특징을 잡아내기도 쉽습니다. 따라서 원래 신호를 규칙적인 신호들의 합으로 나타내는 것은 신호 데이터 처리에 있어 기본적인 요소입니다. 이렇게 신호를 주기적인 신호들의 합으로 표현하는 것이 시간-주파수 분석입니다.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;그런데 이 신호처럼 주기적인 신호의 합으로 완성된 신호가 아니라, 처음부터 복잡하게 생긴 신호는 어떻게 처리해야 할까요? 예를 들어 음성 데이터나, 주식 데이터 등은 처음부터 복잡하게 생겼는데, 이렇게 이쁘게 분해낼 수 없는 것이 아닐까요? 사실 이런 신호들을 처리하는 데에도 똑같은 방식을 사용할 수 있습니다. 기본적으로 **모든 신호는 사인파의 합으로 나타낼 수 있습니다.** 아래는 마이크로소프트의 1년간 주식 변동 그래프와, 이를 사인파로 분해한 그래프입니다.
![msstock](/assets/img/2023-04-09/ms_stock_price.png){: width="800"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}
![msstockdecomp](/assets/img/2023-04-09/ms_stock_price_decomp.png){: width="800"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이처럼 다양한 형태의 신호 데이터는 모두 기본적인 형태의 신호 여러 개의 합으로 나타낼 수 있습니다. 물론 위와 같이 복잡한 그래프는 훨씬 더 많은 신호의 합으로 나타내야 하겠지만, 우선은 모든 신호가 분해 가능하다는 사실만 알아두면 좋을 것 같습니다. 다만 이렇게 신호를 분해하는 방법에도 여러 가지 방법이 존재하는데, 대표적인 방법에 대해 아래에서 소개하겠습니다.  

---

## 1. 고속 푸리에 변환 (Fast Fourier Transform)
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;신호 데이터는 원래 시간에 따른 진폭의 변화를 나타내는 데이터입니다. 그래서 신호 그래프의 x축과 y축은 각각 시간과 진폭을 나타냅니다. 그런데 위에서 신호는 사실 다양한 주기를 가지는 신호들로 분해할 수 있음을 확인했습니다. 즉, 신호 데이터는 사실은 시간, 진폭, 주기(주파수)에 대한 정보를 모두 가지고 있는 데이터인 셈입니다.   
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이 신호 데이터를 시간-진폭 간 관계에서 주기(주파수)-진폭 간 관계로 바꿔주는 가장 기본적인 방식이 바로 ***이산 푸리에 변환(Discrete Fourier Transform)*** 입니다. 아래 그림과 같이 원본 신호(빨간색)가 다양한 주파수의 사인파로 분리되고, 그 각각의 사인파에 해당하는 진폭을 나타내는 데이터(파란색)로 변환됩니다.  
{:style="opacity: 0.90"}

![FFT1](/assets/img/2023-04-09/FFT.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  
출처: Wikipedia  
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;***고속 푸리에 변환은(Fast Fourier Transform)***은 이산 푸리에 변환을 빠르게 수행하는 방법입니다. 일반적으로 O(N^2)의 복잡도인 이산 퓨리에 변환에 비해 O(NlogN)의 복잡도로 수행할 수 있다는 장점이 있습니다. 수행 코드는 아래와 같습니다:  
{:style="opacity: 0.90"}

~~~python
import numpy as np
import matplotlib.pyplot as plt

def fft_example(signal):

    fft_result = np.fft.fft(signal)  # FFT
    freqs = np.fft.fftfreq(len(signal), 1/fs)  # Frequency bins
    return fft_result, freqs

fs = 1000  # Sampling frequency
t = np.arange(0, 1, 1/fs)  # Time vector
f1, f2, f3 = 5, 40, 20  # Frequencies
signal = 0.5*np.sin(2 * np.pi * f1 * t) + 1.7*np.sin(2 * np.pi * f2 * t) + 1.1*np.sin(2 * np.pi * f3 * t)   # Signal

fft_result, freqs = fft_example(signal)

plt.figure(figsize=(20, 3))
plt.subplot(1, 2, 1)
plt.plot(t, signal)
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.title("Time Domain")

plt.subplot(1, 2, 2)
plt.plot(freqs, np.abs(fft_result))
plt.xlabel("Frequency (Hz)")
plt.ylabel("Magnitude")
plt.title("Frequency Domain")
plt.show()

~~~
![FFT2](/assets/img/2023-04-09/FFT2.png){: width="800"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 위 코드에서는 진폭과 주파수가 다른 3가지의 신호를 합쳐서 하나의 신호를 만들고, 그 신호를 다시 고속 푸리에 변환했습니다. 그 결과 세 가지 신호가 각각 어떤 주기와 진폭을 가지고 있는지를 다시 얻을 수 있습니다.  

---
## 2. 단기 푸리에 변환 (Short Time Fourier Transform)
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이산 및 고속 푸리에 변환을 통해서는 신호의 주파수 성분을 볼 수 있었습니다. 그런데 고속 푸리에 변환을 통해 얻은 결과에는 시간에 따른 정보가 아예 없습니다. 이 떄문에 만약 신호의 주파수 성분이 시간에 따라 변화한다면, 예를 들어 특정 시간 이후에 새로운 주파수의 신호가 추가된다면, 이러한 변화를 확인할 수 없습니다.  
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;따라서 신호가 시간에 따라서 변화할 수 있는 경우, 시간, 주파수, 진폭 간의 관계를 동시에 나타낼 수 있도록 하는 방법이 필요합니다. 이를 위해 등장한 것이 ***단기 푸리에 변환(Short Time Fourier Transform)***입니다. 단기 푸리에 변환은 신호를 작은 단위의 시간으로 쪼개어서, 각 시간 단위에 대해 고속 푸리에 변환을 실시합니다. 그렇게 짧은 시간 단위 마다 주파수-진폭 데이터를 얻고, 이 데이터를 연결해서 시간-주파수-진폭 간 관계를 모두 나타낼 수 있는 데이터를 생성합니다. 
{:style="opacity: 0.90"}

![STFT1](/assets/img/2023-04-09/STFT1.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  
출처: Fischman, Rajmil. (1997). The phase vocoder: theory and practice. Organised Sound. 2. 127 - 145.
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 위 그림은 단기 푸리에 변환의 수행 과정에 대한 그림립니다. 단기 푸리에 변환을 수행하면 시간-주파수-진폭 값을 가지는 3차원의 결과가 만들어지는데, 이를 표현하기 위해서 x축은 시간, y축은 주파수, 그리고 색상으로 진폭을 표현하는 그래프를 그리게 됩니다. 이 그래프를 ***Spectrogram***이라고 합니다. 고속 푸리에 변환 및 spectrogram은 scipy.signal 라이브러리를 통해 구현할 수 있습니다.
{:style="opacity: 0.90"}

~~~python
import scipy.signal

def stft_example(signal):
    f, t, Zxx = scipy.signal.stft(signal, fs, nperseg=30)
    return f, t, Zxx

fs = 1000
t = np.arange(0, 2, 1/fs)
f1, f2 = 5, 40
signal = np.sin(2 * np.pi * f1 * t) + np.sin(2 * np.pi * f2 * t * np.exp(-5*t))

f, t, Zxx = stft_example(signal)

plt.figure(figsize=(20, 3))
plt.subplot(1, 2, 1)
plt.plot(np.arange(0, 2, 1/fs), signal)
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.title("Time Domain")

ax_stft = plt.subplot(1, 2, 2)
plt.pcolormesh(t, f, np.abs(Zxx), shading='gouraud')
plt.xlabel("Time (s)")
plt.ylabel("Frequency (Hz)")
plt.title("Spectrogram")

ax_stft.set_ylim(0, 100)
plt.show()

~~~
![STFT2](/assets/img/2023-04-09/STFT2.png){: width="800"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 코드에 사용한 신호 데이터는 일정한 주파수가 계속되는 신호와, 시간에 따라 주파수가 점점 작아지는 신호의 합성 신호입니다. 단기 푸리에 변환을 통한 spectrogram을 확인해 보면, 시간에 따라 주파수가 다른 신호가 나타나는 것을 확인할 수 있으며, 시간에 따라 일정 주기의 신호만이 남는 사실 또한 알 수 있습니다.
{:style="opacity: 0.90"}

## References
[Wikipedia](https://en.wikipedia.org/wiki/Short-time_Fourier_transform)