# capstone
빠른 결과 도출을 위해 C언어를 사용하였지만, 딥러닝 프레임워크 사용 및 gpu성능 확보를 위해, 본 학습은 google colab에서 진행하였습니다.

wavutils를 이용하여, wav파일들을 mono, 16000 sample rates, 16 bit의 pcm파일들로 변형하였습니다.

이후 학습데이터를 이용해 모델 제작후, 딥러닝 모델로 학습하였는데, 이때 사용한 모델이 RNN 기반 모델로,
innput에서 42개의 feature를 추출한 후, 3개의 다른 rnn(GRU)층을 통과 하는데, 각각 음성 탐색, 노이즈 탐색, 노이즈 제거를 담당합니다.

<img width="403" alt="topology" src="https://user-images.githubusercontent.com/113290798/205588694-574e0bbd-ade0-4c9b-80c1-191790c4d50a.png">

이렇게 학습된 parameter들을 rnn_data.c 파일에 옮겨 컴파일하여 denoise가 가능한 프로그램을 빌드합니다.

test를 위해서 noise와 clean voice를 임의로 합성하였으며, denoise를 통해 나온 결과와 비교하는 과정을 거쳤습니다.

noisy:

![noisy file](https://user-images.githubusercontent.com/113290798/205589092-1bbebf1b-3db9-44f0-9ec2-2a3ee21e5f44.png)

denoised:

![denoised file](https://user-images.githubusercontent.com/113290798/205589039-059c4fc0-2b5a-43a0-a6e4-dd8a5bb8ebde.png)

clean voice:

![voice file](https://user-images.githubusercontent.com/113290798/205588971-b0d7db0d-3a62-48a2-93d3-df9052903487.png)

noisy와는 다르게, clean voice와 denoised는 상당히 유사한 진폭과 진동수를 가지는 것을 확인했습니다.
