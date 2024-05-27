임의의  부동  소수점으로  이루어진  이산  신호(discrete 
signal)와 부동 소수점으로 이루어져 있는 필터와의 합성곱(Convolution)을 진행하고, 
특정 결과를 메모리에 저장하는 코드를 작성한다.
1.   Introduction
프로젝트의 전체 동작은 임의의 부동 소수점으로 이루어진 이산 신호와 필터의 
합성 곱(그림 1)을 수행한 결과 중 특정 범위 내에 포함되는 값만 추출하여, 해당 
결과와 결과의 index 값을 저장한다.

![1](https://github.com/hbeooooooom/2022_Assembly_Termproject/blob/main/readmemdpng/1.png)

2.   System Overview
프로젝트의 전체 동작은 제공하는 부동 소수점 데이터를 활용하여, 제시되어있 
는 필터와 연산한 결과를 특정 메모리 주소에 저장하는 것을 목표로 작성한다.

![2](https://github.com/hbeooooooom/2022_Assembly_Termproject/blob/main/readmemdpng/2.png)

- Code 작성 시 유의사항
ü Co-Operation을 사용하지 말 것
ü AREA는 추가선언하지 말 것
ü 코드의 흐름을 알 수 있는 대략적인 주석을 작성할 것
다음은 코드 작성 시 필수로 사용되거나 작성되어야 하는 부분을 명시한다. 
- Discrete Convolution (이산 합성곱)

 본 과제에서는 1D-이산 합성곱을 사용하며, 다음과 같은 수식을 가진다.

![3](https://github.com/hbeooooooom/2022_Assembly_Termproject/blob/main/readmemdpng/3.png)

해당 수식에서 x는 연속된 데이터를 의미하여, y는 결과 값, n은 index, h는 
filter, M은 filter의 크기를 의미한다.
ü 본 과제에서 사용할 필터는 다음과 같이 정의된다.
h = [1.95, 1.72, -0.431, -1.278, -0.8022, -0.2115] (length-6 filter)
x는 Sampled_Data 함수를 통해서 제공되는 480개의 데이터(32-bit, Double 
Word)를 의미한다.
- Label: Sampled_Data
ü DCD 명령어를 이용하여 데이터가 선언되어 있음
ü 임의의 사인 합성파에서 샘플링한 데이터 480개가 명시되어 있음
ü 임의의 데이터는 –4 ~ 8 사이의 부동 소수점 값을 원소로 가짐
- Label: Result
ü Convolution의 결과 중 –4.7 이하의 모든 수와 해당 수의 인덱스를 저장
ü 저장 순서는 메모리를 기준으로 모든 수를 저장한 후, 인덱스를 저장한다.
ü 최종 결과는 소수 저장 시 부동 소수점 형태로 32bit(Double Word) 단위로 
저장, index는 word 단위로 저장한다.
ü 최종 결과 저장 주소의 시작점은 0xF0000000 번지부터 저장
