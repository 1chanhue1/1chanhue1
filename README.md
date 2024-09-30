
# [Cosmic Detox] 스마트폰에서 벗어나볼까요?



# ![image](https://github.com/user-attachments/assets/381b14c1-ca31-46fc-b8c5-18f6a6098e2f)







## 1. 프로젝트 소개
  
**현대인이라면 누구나 도파민 중독?**
**코스믹 디톡스와 함께 우주여행 하며 디지털 디톡스 해보세요!**

**휴대폰을 놓지 못하는 현대인들, 이제는 디지털도 다이어트를 해보는 건 어떨까요?**

**쉽지 않은 도전을 코스믹 디톡스가 도와줄게요.**





## 2. 기술 스택

<br>

| 범위 | 기술 이름 |
| --- | --- |
| Architecture | Clean Architecture |
| Design Pattern | MVVM , Repository |
| DI | Hilt |
| Async Task | Coroutine , Flow |
| Firebase | Authentication, Firestore, Functions, Storage |
| Local DB | SharedPreferences |
| Component |	Service , Broadcast Receiver | 
| UI | Jetpack Navigation, XML |
| Image | Glide |
| 외부 API |  |

</br>





## 3. 주요 기능 
![image](https://github.com/user-attachments/assets/3b3ccd67-29ff-40e4-a867-061dac4ac63a)
회원가입 및 로그인을 할 수 있습니다.
카카오 로그인 구글 로그인 X 로그인 총 3개의 소셜 로그인을 지원합니다.


![image](https://github.com/user-attachments/assets/52b57024-6eda-4f5d-83a2-5da4d3589196)

홈 화면에서는 나의 디지털 디톡스 이력을 한 눈에 조회할 수 있습니다.
 총 누적 시간과 누적 조회수에 따라 커지는 행성을 통해 직관적으로 알 수 있으며 오늘 누적 시간 또한 별도로 표시하고 있습니다.

![image](https://github.com/user-attachments/assets/9d95b5f7-8ad6-483b-bf57-a71b4cf57722)

 레이스 화면에서는 모든 유저의 누적시간을 1위부터 100위까지 조회할 수 있습니다.
 내 순위는 하단에 고정되어 있습니다

![image](https://github.com/user-attachments/assets/bd175b89-b85f-4001-8aec-4ee5dc83ba02)

내정보 화면에서는 앱 이용기간과 총 누적 시간, 트로피의 유무를 볼 수 있으며, 나의 전체 앱 사용량을 조회할 수 있습니다.

 또한 디지털 디톡스 중에 사용할 **`허용 앱`**을 설정할 수 있습니다. **`허용 앱`** 을 설정해야 디톡스 중에서 다른 앱을 이용할 수 있으며, 기본 고정 시간은 30분입니다. **`앱 사용시간 제한`** 기능을 통해 **`허용 앱`** 들의 사용 시간을 커스텀 할 수 있습니다.

![image](https://github.com/user-attachments/assets/34aa20ef-7eb0-4592-96e5-e4a79cf5bb32)

![image](https://github.com/user-attachments/assets/1229d9a3-3c9d-49b7-9313-a2f2dae1ea54)

 타이머를 시작하면 디지털 디톡스를 시작하는 것과 같고 측정된 시간은 총 누적 시간과 오늘 하루 디톡스 시간에 쌓이게 됩니다.
 타이머가 돌아가는 동안엔 뒤로가기나 홈버튼, 메뉴 버튼 등은 동작하지 않으며 화면을 벗어나려고 하면 OverlayView 가 나오며 동작을 제한합니다.
 하지만 앱 사용 중에 다른 앱을 사용하고 싶으면 잠깐 쉬기 기능을 통해 설정해두었던 허용 앱 에 접근하여 제한 시간 만큼만 쉴 수 있습니다. 하지만 이미 제한 시간을 모두 소모한 경우엔 더 이상 해당 앱을 사용할 수 없습니다.

## 4. 기술적 의사결정

<details>
  <summary>
    ❓ 허용 앱 리스트의 경우 왜 로컬 DB가 아닌 FireStore를 사용했나요?  </summary> 
1. 다중 기기 사용 가능성
→ 디톡스 앱 사용자 중에는 공부나 일에 집중하기 위해 사용하는 사람들이 많습니다. 특히 학생이나 공시생의 경우, 스마트폰과 함께 태블릿으로 인터넷 강의를 듣는 경우가 많습니다.
→ 여러 기기에서 앱을 사용할 수 있게 하려면 동일한 계정으로 로그인했을 때, 기기마다 동일한 허용 앱 리스트가 있어야 합니다. 이를 위해 로컬 DB 대신 Firestore를 사용하여 서버에서 데이터를 관리하는 방식을 선택했습니다.

2. 시간 초기화 기능
→ 자정 마다 허용 앱 사용 시간을 초기화하려면 각 앱에 지정된 제한 시간을 서버가 알고 있어야 하기 때문에, Firestore에서 데이터를 관리하는 것이 더 적합하다고 판단했습니다.

3. 앱 삭제 시 데이터 초기화
→ 사용자가 앱을 삭제하고 다시 설치하면 로컬 DB의 데이터는 삭제되지만, Firestore를 사용하면 기존 허용 앱 리스트가 서버에 저장되어 유지됩니다. 이를 통해 사용자는 앱을 다시 설치해도 동일한 허용 앱 리스트를 복원할 수 있어, 데이터를 안전하게 관리할 수 있습니다.</details>


## 5. 트러블 슈팅

## 6. 구성원




