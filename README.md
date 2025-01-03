# AR-Manual🪑

### 프로젝트 기간
- 2023년 3월 ~ 2023년 11월
- 대학교 4학년 종합 설계

</br>

### 프로젝트 개요
-   AR Manual은 증강현실 AR을 이용하여 가구 조립을 보다 쉽게 설명해주도록 제작하였다. 본 프로젝트는 종이 설명서의 한계점을 보완하기 위해 제작되었다. 제품에 AR 콘텐츠 증강을 위한 마커를 붙이지 않고도 콘텐츠를 증강할 수 있도록 물체 자체를 인식하는 Vuforia의 Model Targeting 기술을 적용하여 물체의 위치와 각도, 기울기와 상관없이 제품을 인식할 수 있다. 앱을 실행하면 제품의 QR 코드를 인식하고 자동으로 해당 제품의 조립 설명서로 이동한다. 또한 각 조립 단계에 맞는 부품을 자동을 찾아주는 자동 부품 인식 기능과 3D 오브젝트를 이용한 시뮬레이션으로 누구나 쉽게 조립할 수 있도록 제작하였다. 

</br>

### 프로젝트 동기
- AR은 Augmented Reality의 약자로서 증강현실을 의미합니다.
  AR의 특징은 처음부터 새롭게 만들어내는 것이 아니라 현실세계의 정보와는 별개로 만들어진 정보를 덧붙여 현실에 증강하는 것입니다.
  이러한 특징을 가진 AR을 이용하여 다양한 제품 중 의자 조립 설명서를 제작하였습니다.
  
-   대부분의 제품에 동봉되어 있는 종이 설명서는 단순한 글과 그림으로만 표현되어 있어 조립에 어려움을 겪는 사람들이 많다.
    해외 직구 제품의 경우, 종이 설명서가 영어나 중국어 등 한국어가 아닌 언어로 되어있어 제품 조립을 시작조차 하기 힘들 때도 있다.
    또한,  제조사의 입장에서는 종이 자원의 낭비와 설명서 제작과 수정 등 관리에 필요한 지속적인 비용이 발생한다. 우리는 이러한 문제점을 해결하고자 AR을 이용한 사용 설명서를 제작하였다.
  
</br>

### 선행 연구
- AR manual에 대해 찾아보았을 때 제품을 구매한 소비자가 사용하도록 상용화된 설명서는 차량 설명서 정도였고 대부분 공장이나 기업에서 직원 교육용이나 설비 사용설명을 위한 것이었습니다.
  하지만 이런 ar manual은 적용된 제품이 모두 위치가 고정되어 있거나 움직이지 않았기 때문에 앞에 보이는 사진처럼 마커를 부착하여 ar 콘텐츠를 증강하는 방식을 사용하였습니다. 저희가 제작하려는 조립 설명서는 부품의 위치가 정해져 있지 않고 사용자가 어느 각도에서 촬영할지 모르기 때문에 마커를 이용하기 어렵습니다. 따라서 부품 전체를 하나의 마커로 인식하는 모델 타겟 기능을 사용하여 제작하였습니다. 

![image](https://github.com/user-attachments/assets/adaddc43-31e6-45f0-9ccd-a0ffc0538ee2)
<br/>=> 공장에서 사용하는 예시, 기계 앞에 마커가 부착되어 있음
  
</br>

---

### 개발 도구
- Unity
- polycam
- vuforia
- C#

---

### 프로젝트 수행 과정
#### 1.  3D 오브젝트 촬영
- polycam을 이용하여 모든 부품을 3D 오브젝트로 제작
- 부품을 가운데에 두고 카메라로 여러 각도에서 촬영한 후 3차원으로 구성
- FBX 파일과 OBJ 파일 2종류로 다운받아 사용

</br>

#### 2. Vuforia Model Target Generator에서 모델 제작

  ##### [generator 설정 과정]
  
    1) FBX 파일을 Vuforia의 Model Target Gernerator에서 불러옴

    2) Model Up Vector에서 모델의 방향을 조절하기 위해 기준이 되는 축 설정
    
    3) Model Unit : 모델 타겟의 크기는 실제 오브젝트의 크기와 일치해야 하므로 실제 크기와 가장 유사한 단위를 선택
    
    4) Coloring : 모델의 다양한 색은 추적 성능을 향상시킴, FBX 파일은 텍스처가 포함되어 있어서 따로 색칠하지 않아도 됨
    
    5) Complexity : 모델 권장 사항을 초과하는 복잡한 모델은 앱 성능에 해를 끼칠 수 있으므로 단순화 과정을 진행해야함,
                    하지만 이 프로젝트에서 제작한 모델은 모두 권장 사항을 초과하지 않아 단순화는 진행하지 않음
                    
    6) Optimize Tracking : 모델에 대한 추적 최적화 모드 선택
                           반사성이 있고 질감이 없는 표면이 매끄러운 물체나 자동차를 모델 -> Low feature object
                           대부분의 오브젝트 -> default 
                           
    7) Guide View :  이 프로젝트에서 제작된 모델은 모두 360°에서 추적할 수 있어야 하기에 Advanced View를 선택하였고, 그중 Full 360°를 선택


- 위의 과정을 완료 후 만들어진 DB를 학습시킨 후 unitypackage를 다운 받아 Unity에서 사용 <br/>
  (https://developer.vuforia.com/home => vuforia 사이트)

  ![image](https://github.com/user-attachments/assets/79a67189-3ce0-4898-8e39-056a3dc234be)<br>
  => Model Target Generator 화면

</br>

#### 3. Unity에서 UI 제작 및 오브젝트와 모델 배치
  - Unity에서 조립 화면의 UI 제작
  - 의자의 조립 단계를 총 11단계로 구성
  - 각 조립 단계별 scene을 만들어 관리함
</br>
![image](https://github.com/user-attachments/assets/520f5523-c859-4527-9a5f-6de8e826d419)

</br>  =>  Unity에서 제작한 2단계 화면

  - 화면의 상단 : 현재 단계 표시
  - 화면의 양 옆 : 단계를 이동할 수 있는 버튼 제작
  - 화면의 하단 : 현재 단계에 맞는 설명 첨부

<br/>

- 모델과 오브젝트 배치
  - 부품 인식 기능을 위해 Model Target Generator로 제작한 unitypackage와 Polycam에서 다운받은 OBJ 파일 Import
  - 각 단계에 맞는 모델을 Model Target으로 Scene에 추가함
  - 모델이 인식되면 부품의 색이 변하게 하려고 모델과 똑같은 오브젝트를 자식으로 추가하고 material 변경
  - 조립에 필요한 오브젝트가 중강하기 위해 증강해야 하는 부분에 부품 오브젝트를 자식으로 추가
</br>
![image](https://github.com/user-attachments/assets/61164b21-36e6-4148-9682-5ce7d585bb26)

<br/>

#### 4. C# 스크립트 작성
- 조립 화면에서 버튼을 통해 단계를 이동하기 위해 SceneManagement의 SceneManager.LoadScene을 이용하여 각 장면으로 이동할 수 있는 함수 작성
  ![image](https://github.com/user-attachments/assets/49a3c9cd-f0e8-48c6-a5c3-d7cb15c69a13) <br/>
  => 화면 전환 함수
  
</br>

- 조립 설명 기능에서 부품 오브젝트가 조립 방향에 맞게 움직이게 하기 위해 C# 스크립트 작성
- Start 함수 : 처음에 한번만 호출되는 함수
- Update 함수 : 프레임마다 호출되는 함수
</br>

- Start 함수가 호출되면 오브젝트의 현재 local 좌표를 minY 값으로 저장함
- minY 값에서 0.3f만큼 위를 maxY 값으로 설정
</br>

- Update에서는 오브젝트의 local 좌표값의 y축값을 일정한 거리 (적절한 속도를 정해 속도*시간을 하여 거리를 구함)를 sign 값에 곱해 더해줌
- sign 값이 +1이면 오브젝트가 위로 올라가고,
            -1이면 오브젝트가 밑으로 내려감
- 만약 현재 오브젝트의 local값이 minY보다 작거나 maxY보다 크다면 sign값에 -1을 곱해서 오브젝트의 이동 방향을 바꿔줌
  
![image](https://github.com/user-attachments/assets/b4310af8-e0da-4579-b984-8f900ddd0087)</br>
=> 오브젝트 이동 스크립트 
</br>

#### 5. QR 코드 인식 기능
- QR 코드에 설명서의 첫 scene의 이름인 chair_step1이라는 텍스트를 저장하여 생성함
- QR 코드 인식은 Vuforia에서 제공하는 Barcode 기능 사용
- Scene에 Vuforia Engine의 Barcode를 추가하고 C# 스크립트 작성
- 화면에 띄울 텍스트와 연결하기 위해 barcodeAsText 정의 (사진 참고)

- Start 함수가 호출되면 바코드에 저장된 정보를 읽어옴
- Update 함수에서 바코드가 인식되고 바코드에 저장된 데이터가 있다면
  barcodeAsText.text에 "설명서로 이동 중입니다. 잠시만 기다려주세요."라는 문구를 저장하고
  바코드에 저장되어 있던 텍스트를 장면 전환 함수에 넣어 알맞은 장면으로 이동
- 만약 바코드가 인식되지 않으면 barcodeAsText.text에 아무 텍스트도 저장하지 않아 텍스트가 뜨지 않도록 하였음
  
- 스크립트를 완성한 후 Scene에 barcodeAsText와 연결할 TextMeshPro를 만들어 연결

![image](https://github.com/user-attachments/assets/31b662a5-78ca-4c62-acac-e0ece01425ff) <br>
  => 바코드 인식 C# 스크립트

![image](https://github.com/user-attachments/assets/9515cc6a-c526-481a-95a5-f9afa1c295df) <br>
  => QR 코드 인식 화면 UI

</br>

---

### 프로젝트 수행 결과

1. QR 코드 인식 기능
- 앱을 실행하면 가장 먼저 QR 코드를 인식하는 장면이 나옴
- QR 코드가 화면에 비추게 되면 사진처럼 "설명서로 이동 중입니다." 라는 문구가 뜨고 제품에 맞는 해당 설명서로 자동으로 이동

2. 부품 인식 기능
-  부품 인식 기능은 부품을 찾을 때 사 용
-  화면에는 특정 부품을 찾는다는 설명 첨부
-  카메라에 해당 부품이 비치게 되면 부품이 색이 바뀌면서 표시되어 부품을 쉽게 찾을 수 있음

3. 조립 설명 기능
- 조립 설명 기능은 부품 인식 기능으로 찾은 부품을 조립하기 위해 사용


- 영상은 시트 플레이트와 시트 하단부를 조립하는 장면임
- 시트 하단부가 카메라에 비치게 되면 시트 플레이트와 나사들이 조립해야 할 위치에 증강
- 또한 나사들이 조립 방향에 맞게 움직이며 화면만 보고 쉽게 조립할 수 있음

---

### 프로젝트 효과
- 복잡한 가구 조립을 시뮬레이션을 통해 보다 쉽게 할 수 있음
- 조립 과정을 360도에서 관찰 가능
- 종이 설명서의 사용을 자제함으로써 비용적인 부담을 줄일 수 있음
- 설명서 수정이 필요한 경우 간단한 코드 수정으로 설명서를 폐기하고 재생산하는 비용을 아낄 수 있음

</br>

---

