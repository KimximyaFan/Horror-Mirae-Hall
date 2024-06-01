# 공포의 미래관

#### 사일런트 힐에서 영감을 받았습니다

<br>


[![Video Label](http://img.youtube.com/vi/7q0SYiYfO0U/0.jpg)](https://youtu.be/7q0SYiYfO0U)
<br> (사진 클릭하시면 유튜브 링크로 넘어갑니다)

<br>

### 0. AR 영상 만들기

꽤 많은 시행착오를 겪었습니다
<br>
Pose Estimation, Object Localization 등을 써볼려고 했으나,
<br>
이미 촬영한 영상에서 체크보드나, QR이미지 없이 AR을 적용하는건 꽤 어려운 작업임을 깨달았습니다
<br>
체크보드 같은 것을 프린트해서 바닥에 깔아서 AR을 구현할 바에는
<br>
차라리 Unity AR Foundation을 쓰는게 가성비가 좋다고 판단했습니다
<br>
<br>

<table>
  <tr>
    <td><img src="https://github.com/KimximyaFan/Horror-Mirae-Hall/assets/107273680/e2f5e73c-4c0c-4161-8662-e582204173b3" width="300"></td>
    <td><img src="https://github.com/KimximyaFan/Horror-Mirae-Hall/assets/107273680/e7e10853-17f5-4c59-909b-76e7d0f88bae" width="300"></td>
    <td><img src="https://github.com/KimximyaFan/Horror-Mirae-Hall/assets/107273680/9d926ade-2c3f-4ce2-88ee-032651fbc5a6" width="300"></td>
  </tr>
</table>

위와 같은 모델들을 다운받았습니다

<br>
<br>

<img src="https://github.com/KimximyaFan/Horror-Mirae-Hall/assets/107273680/6449c8bb-ad00-4b08-9358-78cccba23929">
<br>
Unity AR Foundation에 해당 모델들을 추가하고 약간의 세팅을 변경했습니다
<br>
<br>
<br>

<table>
  <tr>
    <td><img src="https://github.com/KimximyaFan/Horror-Mirae-Hall/assets/107273680/4486bb7d-81e6-4f10-bf83-e217f002d574" ></td>
    <td><img src="https://github.com/KimximyaFan/Horror-Mirae-Hall/assets/107273680/194ee371-334d-400d-bdc8-67c5be81d542" ></td>
  </tr>
</table>

위 그림과 같은 영상을 얻었습니다



<br>

### 1. 소벨 엣지 디텍팅

처음에는 텍스쳐 작업만 했었으나
<br>
경계 구분이 잘 안가서 전처리로 소벨 엣지 디텍팅을 추가해봤더니 생각보다 결과물이 좋았습니다
<br>
여러가지 쓰레쉬 홀드 값을 테스트해봤는데
<br>
표현하려는게 무서운 분위기이다 보니
<br>
쓰레쉬 홀드값을 낮게 주는게 연출이 좋았습니다
<br>
너무 낮게주면 오히려 역효과가 나타나고, 15~20 정도의 값이 괜찮았습니다

<br>

<img src="https://github.com/KimximyaFan/Horror-Mirae-Hall/assets/107273680/4435e051-fad6-4807-9829-1ec668a797d1" >

위 그림과 같은 영상을 얻었습니다

<br>

### 2. 텍스쳐 입히기

<table>
  <tr>
    <td><img src="https://github.com/KimximyaFan/Horror-Mirae-Hall/assets/107273680/96fd1d87-6794-4027-adfa-eda6bc337d0d" height="200" width="200"></td>
    <td><img src="https://github.com/KimximyaFan/Horror-Mirae-Hall/assets/107273680/595c54ee-8f70-427b-a12d-9a343c792c54" height="200" width="200"></td>
    <td><img src="https://github.com/KimximyaFan/Horror-Mirae-Hall/assets/107273680/4359ff23-e158-409c-833f-6d8b817db876" height="200" width="200"></td>
    <td><img src="https://github.com/KimximyaFan/Horror-Mirae-Hall/assets/107273680/3bf81816-d42e-46e5-8318-7ece3db14216" height="200" width="200"></td>
  </tr>
</table>

각 프레임에 대해서 그레이스케일을 적용해주고
<br>
adaptive binary threshold 를 적용합니다
<br>
영상이 흑과 백으로 나뉩니다
<br>
흰색 픽셀에 대해서 텍스쳐를 입히는데
<br>
처음에는 2가지 텍스쳐만 썼었으나
<br>
AR에 모델들이 명암효과를 받지 않다보니
<br>
표현이 별로 안좋게 나와서
<br>
텍스쳐를 4가지로 늘렸습니다
<br>
그리고 텍스쳐를 입힌다는 것에 대해서
<br>
여러 시행착오를 겪었었는데
<br>
결국 직접 픽셀단위로 하나하나 작업해야된다는 결론에 도달했습니다
<br>
그리고 2중 루프도, x y 순서냐, y x 순서냐에 따라서 표현 질감이 달라지고
<br>
텍스쳐로부터 랜덤샘플링을 하냐 아니면 순차적으로 따오냐에 따라 표현 질감이 달라지고
<br>
텍스쳐 순회 인덱스를 프레임마다 초기화 하냐 아니면 쭉 이어서 쓰냐에 따라 표현 질감이 달라집니다

### 3. 영상 속도 낮추기

원본 영상이 생각보다 빨라서 연출적으로 별로기에 속도를 조금 낮췄습니다


### 4. BGM과 발걸음 소리

영상에 어울리는 BGM과 발걸음 소리를 구합니다

파일에 배경 음악을 깔고,

영상을 보면서, 발걸음 소리가 어울리는 상황일 때
<br>
직접 space bar를 눌러서 해당 프레임에 발걸음 소리를 입힙니다

해당 작업은 4_Bgm and FootStep Sound.ipynb 코드를 통해 할 수 있습니다


### 5. 문여는 소리

적당한 문여는 소리를 구한다음

영상 마지막에 소리를 입힙니다

### 6. 페이드 아웃

영상 마지막에 페이드 아웃 처리를 합니다

### 7. 페이드 인

두번째 영상의 초반에 페이드 인 처리를 합니다

### 8. 두 영상 이어붙히기

두 영상을 이어주고, 영상 사이에 2초간의 공백을 둡니다


# Reference

발걸음 소리, 문여는 소리 <br>
https://www.youtube.com/watch?v=Hnwv1YxM4A0

배경음악 1 <br>
https://youtu.be/7Jr7xw3NLx0?si=ciSAYtw5GbHBXepb

배경음악 2 <br>
https://youtu.be/RFkCDt0Guq8?si=V_imv9URZlo0s2OC

텍스쳐2 <br>
https://www.craiyon.com/image/ALps8kbLQsuaIdSQRPNdGw

텍스쳐5 <br>
https://stock.adobe.com/kr/images/grunge-rusted-metal-texture-rust-background/173547344

텍스쳐6 <br>
https://silenthill.fandom.com/wiki/Wall_Scratches

텍스쳐8 <br>
https://alfelix99.artstation.com/projects/zOz6LL


피라미드헤드 모델 <br>
https://sketchfab.com/3d-models/pyramid-head-silent-hill-2-ba665f20056a41c98aa7cb6c56663105

라잉 피규어 모델 <br>
https://sketchfab.com/3d-models/lying-figure-silent-hill-d69cd1299cf84d258582e915a2085b0c

클로저 모델 <br>
https://sketchfab.com/3d-models/closer-silent-hill-3-de9807d714b9486383a1b83fe438dfc4


코드 <br>
강의자료, GPT-4o 참조
