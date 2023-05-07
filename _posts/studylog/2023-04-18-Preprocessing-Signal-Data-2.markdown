---
layout: post
title:  "신호 데이터 전처리 - 웨이블릿 변환"
date:   2023-04-18 12:00:00 +0800
category: studylog
tags: [studylog, python]
comments: true
use_math: true
img:
    path: /assets/img
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;앞서 설명한 고속 푸리에 변환 및 단기 푸리에 변환은 주파수 영역에서 신호를 분석하는데 유용하지만, 신호의 주파수 성분이 시간에 따라 급격하게 변하는 경우에는 한계가 있습니다. 웨이블릿 변환은 이러한 문제를 해결하기 위해 개발된 신호 분석 방법입니다. 웨이블릿 변환은 기존의 푸리에 변환에서 사용되는 사인파와 코사인파 대신 웨이블릿 함수를 사용하여 시간-주파수 영역에서 신호를 분석합니다. 웨이블릿 함수는 일반적으로 시간 영역에서 길이가 제한된 함수로, 신호의 지역적 특성을 더 잘 포착할 수 있습니다.
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;웨이블릿 함수는 특정한 모양을 가지고 있으며, 여러 개의 웨이블릿 함수가 존재합니다. 웨이블릿 변환을 수행하려면 먼저 웨이블릿 함수를 선택해야 합니다. 각 웨이블릿 함수는 서로 다른 특성을 가지고 있으며, 분석하려는 신호에 맞는 웨이블릿 함수를 선택하여 사용해야 합니다.  
{:style="opacity: 0.90; margin-bottom:70px"}

---

## 1. 이산 웨이블릿 변환 (Discrete Wavelet Transform)
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ***이산 웨이블릿 변환(Discrete Wavelet Transform, DWT)***은 웨이블릿 변환의 한 종류로, 신호를 다양한 주파수 밴드에서 다양한 해상도로 분석합니다. 이산 웨이블릿 변환은 신호를 더 작은 웨이블릿 함수로 분해하고, 이를 통해 신호의 다양한 주파수 성분과 시간 영역 정보를 얻을 수 있습니다.
{:style="opacity: 0.90"}

![dwt1](/assets/img/2023-04-18/dwt1.png){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  
출처: https://www.cambridge.org/core/books/abs/wavelet-radio/theory-of-wavelets/744BC8F3421FC7022D6A9D757DDCA36A
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;파이썬에서 PyWavelets 라이브러리를 사용하여 이산 웨이블릿 변환을 수행할 수 있습니다. 아래 코드는 이산 웨이블릿 변환의 예를 보여줍니다. 
{:style="opacity: 0.90"}

~~~python
import pywt
import numpy as np
import matplotlib.pyplot as plt

fs = 1000
t = np.arange(0, 1, 1/fs)
f1, f2 = 5, 40
signal = np.sin(2 * np.pi * f1 * t) + np.sin(2 * np.pi * f2 * t * np.exp(-5*t))

coeffs = pywt.wavedec(signal, 'db4', level=5)

plt.figure(figsize=(20, 3))
plt.subplot(1, 2, 1)
plt.plot(t, signal)
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.title("Time Domain")

plt.subplot(1, 2, 2)
plt.stem(coeffs[0], markerfmt=' ')
plt.xlabel("Coefficient Index")
plt.ylabel("Coefficient Value")
plt.title("Discrete Wavelet Transform")

plt.show()

~~~
![dwt2](/assets/img/2023-04-18/dwt2.png){: width="800"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 위 코드에서는 신호를 이산 웨이블릿 변환을 사용하여 분해했습니다. 그 결과, 원본 신호의 다양한 주파수 성분을 나타내는 계수를 얻을 수 있습니다.

---
## 2. 연속 웨이블릿 변환 (Continuous Wavelet Transform)
{:style="text-align:center; margin-top:50px; margin-bottom:30px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;연속 웨이블릿 변환(Continuous Wavelet Transform, CWT)은 시간-주파수 영역에서 신호의 특성을 분석하는 데 사용되는 또 다른 웨이블릿 변환 방법입니다. CWT는 신호의 모든 지점에서 다양한 크기의 웨이블릿 함수를 사용하여 신호를 분석합니다. 이를 통해 신호의 세부 특성을 놓치지 않고 정밀한 시간-주파수 분석을 수행할 수 있습니다.
{:style="opacity: 0.90"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;따라서 신호가 시간에 따라서 변화할 수 있는 경우, 시간, 주파수, 진폭 간의 관계를 동시에 나타낼 수 있도록 하는 방법이 필요합니다. 이를 위해 등장한 것이 ***단기 푸리에 변환(Short Time Fourier Transform)***입니다. 단기 푸리에 변환은 신호를 작은 단위의 시간으로 쪼개어서, 각 시간 단위에 대해 고속 푸리에 변환을 실시합니다. 그렇게 짧은 시간 단위 마다 주파수-진폭 데이터를 얻고, 이 데이터를 연결해서 시간-주파수-진폭 간 관계를 모두 나타낼 수 있는 데이터를 생성합니다. 
{:style="opacity: 0.90"}

![cwt1](/assets/img/2023-04-18/cwt1.gif){: width="600"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  
출처: [Wikipedia](https://en.wikipedia.org/wiki/Continuous_wavelet_transform)
{:style="text-align:center; opacity: 0.60; margin-bottom:30px; font-size: 12px"}

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 파이썬에서는 scipy 라이브러리를 사용하여 연속 웨이블릿 변환을 수행할 수 있습니다. 아래 코드는 연속 웨이블릿 변환의 예를 보여줍니다.
{:style="opacity: 0.90"}

~~~python
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import cwt, morlet2

fs = 1000
t = np.arange(0, 1, 1/fs)
f1, f2 = 5, 40
signal = np.sin(2 * np.pi * f1 * t) + np.sin(2 * np.pi * f2 * t * np.exp(-5*t))

widths = np.arange(1, 31)
cwtmatr = cwt(signal, morlet2, widths, w=6)

plt.figure(figsize=(20, 3))
plt.subplot(1, 2, 1)
plt.plot(t, signal)
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.title("Time Domain")

plt.subplot(1, 2, 2)
plt.imshow(cwtmatr, extent=[0, 1, 1, 31], cmap='jet', aspect='auto', vmax=abs(cwtmatr).max(), vmin=-abs(cwtmatr).max())
plt.xlabel("Time (s)")
plt.ylabel("Scale")
plt.title("Continuous Wavelet Transform")
plt.colorbar()

plt.show()

~~~
![cwt2](/assets/img/2023-04-18/cwt2.png){: width="800"}{:style="display:block; margin-left:auto; margin-right:auto; padding:5px"}  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;위 코드에서는 신호를 연속 웨이블릿 변환을 사용하여 분해했습니다. 결과로 얻은 시간-주파수 영역에서 신호의 다양한 주파수 성분을 시각적으로 확인할 수 있습니다.
{:style="opacity: 0.90"}


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이산 웨이블릿 변환과 연속 웨이블릿 변환은 모두 시간-주파수 분석에 사용되지만, 각각의 변환 방법은 특정한 응용영역에 적합한 성능을 보입니다. 이산 웨이블릿 변환(DWT)은 계산적 효율성이 뛰어나기 때문에 신호 압축이나 잡음 제거와 같은 응용 분야에 적합합니다. 반면, 연속 웨이블릿 변환(CWT)은 시간-주파수 분석에서 더 높은 해상도를 제공하며, 더 정밀한 신호 특성을 분석하는 데 사용됩니다. 예를 들어, 음성 인식, 심전도(ECG) 분석 및 지진학 데이터 분석과 같은 응용 분야에서 CWT가 자주 사용됩니다.  
{:style="opacity: 0.90"}


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이상으로, 이산 웨이블릿 변환과 연속 웨이블릿 변환의 개념과 파이썬을 사용한 구현 방법을 살펴보았습니다. 두 방법 모두 시간-주파수 영역에서 신호의 특성을 분석하는 데 도움이 되며, 해당 분야의 요구 사항에 따라 적절한 변환 방법을 선택하여 사용하면 됩니다.  
{:style="opacity: 0.90"}
