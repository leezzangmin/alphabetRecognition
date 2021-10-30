# alphabetRecognition


https://user-images.githubusercontent.com/64303390/139528629-77ee4be0-9898-4b45-b45a-7fb322691210.mp4

알파벳을 학습하고 인식하는 신경망으로 만들고 '실시간'으로 데이터를 업로드하는데 목적이 있습니다.

모델 입/출력으로는 우선 학습데이터를 통해 학습한 신경망을 가지고 제가 새로운 알파벳 이미지를 프로그램 내에서 upload해서 실시간으로 인식한 결과 출력이 나오게 됩니다.

프로그램 내에서 창을 띄워서 마우스로 데이터를 그리면 인식결과를 볼 수 있습니다

모델은 신경망 첫걸음 책의 챕터 21의 코드를 사용했습니다

데이터는 kaggle에서 mnist 숫자데이터와 유사한 전처리 된 알파벳손글씨 데이터를 가져왔습니다.
13만개의 알파벳으로 이루어진 파일인데, 약 가로 785, 세로 약 37만 cell 의 크기입니다
mnist숫자 데이터와 구성이 거의 비슷합니다. 각 행의 1열은 target값입니다. 만약 1열의 값이 1이면 알파벳 B를 의미합니다.
나머지 784열은 0~255사이의 값을 가지는 그림 데이터입니다.

방법은 output노드의 개수를 알파벳의 총 개수인 26개로 바꾸고 숫자 데이터와 동일하게 학습 진행했습니다.

그런데 숫자 데이터는 epoch이 10번만 되어도 괜찮은 performance를 보여주는데 알파벳은 그렇지 않았고 
최소 epoch이 200은 되어야 괜찮은 정확도가 나왔습니다.

파일이 약 700mb크기를 가져서 자원을 많이 소모해 epoch수를 많이 늘릴 순 없었고 600회씩 실험해보았습니다.

먼저 학습률 0.000003일때 최대 정확도는 54%였습니다. 낮은 수치가 나와서 학습률을 10배로 늘렸습니다
그랬더니 최대 정확도가 82%로 약 28%정도 증가한 것을 볼 수있습니다.

다음으로는 hiddenlayer의 노드수를 늘려보았습니다.
100개에서 150개로 늘리니까 83%의 정확도를 보였습니다.

한번 더 실험해서 150개에서 200개로 늘리니까 84%의 정확도를보였고, 
추가적으로 학습률을 조정하며 학습한 결과 최종 94%의 정확도를 가지는 모델 이 되었습니다.

그러나 94%의 모델을 가지고 실시간 인식을 해본결과 인식이 잘 이루어지지는 않았습니다. 
10개 입력하면 6개 정도만 정확히 인식하는 모습을 보였습니다 
제가 입력한 데이터와 kaggle에서 가져온 데이터의 필체, 굵기나 크기, 노이즈, 업로드 과정에서의 손실 등 여러 요인이 작용한 것으로 보입니다.
하지만 조금만 손을 본다면 단순히 한 글자만 인식하는 모델을 넘어 손글씨로 된 문장 단위의 데이터를 인식하는 모델도 만들어 볼 수 있을 것입니다.


# 결론

신경망 첫걸음의 파이썬 코드로는 최대 정확도가 약94% 정도 나오는 것으로 확인되었음, 데이터 rotate나 CNN, RNN 등 다른 기술을 적용하지 않은 상태에서의 정확도이므로 해당 기술들을 적용했을 때에 정확도도 주목할만함. 하지만, 실시간으로 데이터를 인식시켰을 때의 정확도는 이와는 대조되게 낮았음. 이는 확보한 dataset과 직접 생성한 data의 size는 같지만 필체, 노이즈, 글씨의 굵기와 크기, 업로드 하는 과정에서의 손실 등 여러 요인이 작용하여 낮은 인식률을 보이는 듯 함.  이를 극복할 해결방안이 필요해 보임. 또한 본 프로그램은 알파벳 한 글자만 인식하는 것에 국한되지만 조정을 거친다면 짧게는 단어에서 문장까지도 인식할 수 있을 것으로 기대됨.


# 참고한 문서 :

[1]	https://ohcoach.tistory.com/18 opencv를 이용한 MNIST숫자인식 확인하기#1
[2]	https://ohcoach.tistory.com/19
opencv를 이용한 MNIST숫자인식 확인하기#2
[3]	Tariq Rashid. 신경망 첫걸음, 2014. Chapter21 
[4]	https://www.kaggle.com/ashishguptajiit/handwritten-az  알파벳 손글씨 데이터
