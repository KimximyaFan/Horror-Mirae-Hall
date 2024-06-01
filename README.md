# 공포의 미래관
<br>
###사일런트 힐에서 영감을 받았습니다
<br>

[![Video Label](http://img.youtube.com/vi/7q0SYiYfO0U/0.jpg)](https://youtu.be/7q0SYiYfO0U)
<br> (사진 클릭하시면 유튜브 링크로 넘어갑니다)

<br>
###0. AR 영상 만들기

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
###1. 소벨 엣지 디텍팅
