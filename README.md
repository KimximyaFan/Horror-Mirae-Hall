# 공포의 미래관
<br>

### 사일런트 힐에서 영감을 받았습니다

<br>


[![Video Label](http://img.youtube.com/vi/7q0SYiYfO0U/0.jpg)](https://youtu.be/7q0SYiYfO0U)
<br> (사진 클릭하시면 유튜브 링크로 넘어갑니다)

<br>

### 0. AR 영상 만들기

<br>
꽤 많은 시행착오를 겪었습니다
<br>
Pose Estimation, Object Localization 등을 써볼려고 했으나,
<br>
이미 촬영한 영상에서 체크보드나, QR이미지 없이 AR을 적용하는건 꽤 어려운 작업임을 깨달았습니다
<br>
체크보드 같은 것을 프린트해서 바닥에 깔아서 AR을 구현할 바에는 차라리 Unity AR Foundation을 쓰는게 가성비가 좋다고 판단했습니다
<br>
위와 같은 모델들을 다운받았습니다
<br>
Unity AR Foundation에 해당 모델들을 추가하고 약간의 세팅을 변경했습니다
<br>
위 그림과 같은 영상을 얻었습니다



<br>

### 1. 소벨 엣지 디텍팅

처음에는 텍스쳐 작업만 했었으나
경계 구분이 잘 안가서 전처리로 소벨 엣지 디텍팅을 추가해봤더니 생각보다 결과물이 좋았습니다
여러가지 쓰레쉬 홀드 값을 테스트해봤는데
표현하려는게 무서운 분위기이다 보니
쓰레쉬 홀드값을 낮게 주는게 연출이 좋습니다
너무 낮게주면 오히려 역효과가 나타나고, 15~20 정도의 값이 좋았습니다

위 그림과 같은 영상을 얻었습니다

<br>

### 2. 텍스쳐 입히기

각 프레임에 대해서 그레이스케일을 적용해주고

adaptive binary threshold 를 적용합니다

영상이 흑과 백으로 나뉩니다

흰색 픽셀에 대해서 텍스쳐를 입히는데

처음에는 2가지 텍스쳐만 썼었으나

AR에 모델들이 명암효과를 받지 않다보니

표현이 별로 안좋게 나와서

텍스쳐를 4가지로 늘렸습니다

그리고 텍스쳐를 입힌다는 것에 대해서
여러 시행착오를 겪었었는데
결국 직접 픽셀단위로 하나하나 작업해야된다는 결론에 도달했습니다

그리고 2중 루프도, x y 순서냐, y x 순서냐에 따라서 표현 질감이 달라지고
텍스쳐로부터 랜덤샘플링을 하냐 아니면 순차적으로 따오냐에 따라 표현 질감이 달라지고
텍스쳐 순회 인덱스를 프레임마다 초기화 하냐 아니면 쭉 이어서 쓰냐에 따라 표현 질감이 달라집니다


### 3. BGM과 발걸음 소리

영상에 어울리는 BGM과 발걸음 소리를 구합니다

파일에 배경 음악을 깔고,

영상을 보면서, 발걸음 소리가 어울리는 상황일 때
직접 space bar를 눌러서 해당 프레임에 발걸음 소리를 입히는 작업을 합니다


### 4. 문여는 소리

적당한 문여는 소리를 구한다음

영상 마지막에 소리를 입힙니다

### 5. 페이드 아웃

영상 마지막에 페이드 아웃 처리를 합니다

### 6. 페이드 인

두번째 영상의 초반에 페이드 인 처리를 합니다

### 7. 페이드 아웃

두 영상을 이어주고, 영상 사이에 2초간의 공백을 둡니다


# Reference

발걸음 소리, 문여는 소리
https://www.youtube.com/watch?v=Hnwv1YxM4A0

배경음악 1
https://youtu.be/7Jr7xw3NLx0?si=ciSAYtw5GbHBXepb

배경음악 2
https://youtu.be/RFkCDt0Guq8?si=V_imv9URZlo0s2OC

텍스쳐2
https://www.craiyon.com/image/ALps8kbLQsuaIdSQRPNdGw

텍스쳐5
https://stock.adobe.com/kr/images/grunge-rusted-metal-texture-rust-background/173547344

텍스쳐6
https://silenthill.fandom.com/wiki/Wall_Scratches

텍스쳐8
https://alfelix99.artstation.com/projects/zOz6LL


피라미드헤드 모델
https://sketchfab.com/3d-models/pyramid-head-silent-hill-2-ba665f20056a41c98aa7cb6c56663105

라잉 피규어 모델
https://sketchfab.com/3d-models/lying-figure-silent-hill-d69cd1299cf84d258582e915a2085b0c

클로저 모델
https://sketchfab.com/3d-models/closer-silent-hill-3-de9807d714b9486383a1b83fe438dfc4


코드 <br>
강의자료, GPT-4o 참조
