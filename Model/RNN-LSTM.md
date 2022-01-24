# RNN-LSTM

![Untitled](https://user-images.githubusercontent.com/98019312/150756436-f66be216-3c5b-46bc-b1c9-2ab284632a6b.png)

![Untitled 1](https://user-images.githubusercontent.com/98019312/150756465-87637962-8630-4608-966b-63f1c3a1f915.png)


현 t시점에서 은닉상태 ht라 할때

![Untitled 2](https://user-images.githubusercontent.com/98019312/150756565-855afeff-dab0-4987-82b3-146020949b56.png)
#
![Untitled 3](https://user-images.githubusercontent.com/98019312/150756563-43b64f25-50cc-47c9-a3b7-8fac344fa456.png)
#
![Untitled 4](https://user-images.githubusercontent.com/98019312/150756552-97f47ab8-892f-4a5b-906a-bdf01d9cf57b.png)


RNN 모델은 어떤 문제를 해결하느냐에 따라 입력과 출력의 길이를 조절할 수 있다.

many-to-one  

ex> 메일이 스팸인지 아닌지, 감성 이진 분류 ..

one-to-many

한장의 이미지를 입력 받아 이미지를 설명하는 텍스트를 출력

many-to-many

한국어 → 영어 등의 번역기, 개체명 인식기 .. 

![Untitled 5](https://user-images.githubusercontent.com/98019312/150757030-e706e608-1cab-41ab-aeb2-76c406fc3019.png)

![Untitled 6](https://user-images.githubusercontent.com/98019312/150757024-db185196-d247-4fca-b32b-2c49d3f978e8.png)

![Untitled 7](https://user-images.githubusercontent.com/98019312/150757014-ff4717b4-abf5-4559-897b-654165f1ed55.png)


**LSTM(long short term memory)**

모델 입력 시퀀스의 시점이 길어질수록 앞쪽의 데이터가 뒤로 잘 전달 되지 않아 학습 능력이 떨어진다. 

또한  RNN을 다층 구조로 쌓으면 입력과 출력 데이터 사이 연관 관계가 줄어 장기 의존성(Long term dependency) 문제가 발생한다.

LSTM 은 input, forgot(삭제), output 게이트로 구성되어 있다.


**forgot gate**

![Untitled 8](https://user-images.githubusercontent.com/98019312/150757134-77aacf04-8817-400e-8b0e-52132b44174a.png)


cell state로부터 어떤 정보를 버릴 것인지 정하는 것으로

ht-1과 xt를 받아 가중치를 곱하고 바아스를 더해 시그모이드 함수에 넣어 0 ~ 1 사이 앖을 Ct-1에 보내준다. 값이 1이면 모든 정보를 보존하는 것이고, 0이면 모두 버리는 것이다. 
#

**input gate**

![Untitled 9](https://user-images.githubusercontent.com/98019312/150757163-ee42cdf9-bd6f-47eb-bbdd-aab0b2453ac5.png)


앞으로  들어오는 새로운 정보 중 어떤 정보를 cell sate에 저장할 것인지 정하는 게이트다.

두단계에서 나온 정보를 합쳐 state를 업데이트 할 재료를 만든다.

forgot gate에서 기존 주어의 성별을 잊어버리기로 했고 대신에 새로운 주어의 성별 정보를 더하는 과정이다. 


![Untitled 10](https://user-images.githubusercontent.com/98019312/150757202-28991a79-142f-487a-8102-fe4909834639.png)


이제 과거 state인 ct-1을 업데이트 해 Ct를 만들 것이다.

우선 첫번째 항은 과거 잊어버리기로 했던 정보들의 정도 ft와 Ct를 곱해 잊어버리고 it와 현재 정보를 곱해 현재 t시점의 상태 값을 구한다.
#

**output gate**

![Untitled 11](https://user-images.githubusercontent.com/98019312/150757243-1d993e17-8dfe-496a-a469-0acdaa0ed71c.png)


output은 우선 sigmoid 에 input 데이터를 태워서 cell state의 어느 부분을 output으로 내보낼 지를 정한다. 그리고 tanh를 씌우고 -1 ~ 1 사이 값을 받은 뒤 sigmoid 씌워 만든 값과 곱해준다. 

#

**양방향 LSTM**

LSTM, RNN은 과거 정보만을 가지고 다음 단어를 예측한다는 점에서 정보가 부족하다. 예문에 따라 문장의 앞부분보다 뒷부분이 더 중요할 수도 있다. 자연어 처리에 있어 입력데이터의 정방향 처리만큼 역방향 처리 역시 중요하다. 양방향 LSTM은 LSTM 계층에 역방향으로 처리하는 LSTM 계층을 하나 더 추가해 양방향에서 문장의 패턴을 분석할 수 있도록 구성되어 있다.

![Untitled 12](https://user-images.githubusercontent.com/98019312/150757261-9f5a6b68-7467-4ae9-8363-f4301c188525.png)


참고 : [https://dgkim5360.tistory.com/entry/understanding-long-short-term-memory-lstm-kr](https://dgkim5360.tistory.com/entry/understanding-long-short-term-memory-lstm-kr)
