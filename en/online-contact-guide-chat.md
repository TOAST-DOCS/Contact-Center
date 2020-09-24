## Contact Center > Online Contact > 서비스 가이드 > 채팅

### 기본 설정
헬프센터 내에 채팅 기능을 **활성화**시키거나, 사용 중인 서비스 웹 페이지에 인입 스크립트를 통해 **채팅 위젯**을 추가하여 채팅 상담을 통한 문의 처리가 가능합니다.
[서비스 관리 → 헬프센터 → 구성관리](https://github.com/TOAST-DOCS/Contact-Center/blob/alpha/ko/online-contact-guide-service-management.md#%EA%B5%AC%EC%84%B1%EA%B4%80%EB%A6%AC) 탭에서 채팅 기능을 활성화시키실 수 있으며, 채팅 기능 활성화 시 다음과 같은 기능들을 [서비스 관리 → 채팅](https://github.com/TOAST-DOCS/Contact-Center/blob/alpha/ko/online-contact-guide-service-management.md#%EC%B1%84%ED%8C%85) 메뉴에서 설정하실 수 있습니다.
-	기본 설정: 채팅 상담 시작 시 전송되는 **인사말** 및 평가 요청 시 전송되는 **만족도 안내 메시지** 설정
-	상담원 할당 설정: 채팅 상담 요청이 접수될 시, 해당 고객과의 최근 채팅기록이 있는 상담원에게 채팅 상담을 **우선으로 할당**하는 기능의 활성화 및 비활성화
-	채팅화면 삽입 코드: 사용 중인 서비스 페이지에 채팅 위젯을 삽입하여 Online Contact의 채팅 상담 서비스를 고객에게 제공하고 싶은 경우, 소스 코드에 삽입할 수 있도록 제공되는 **인입 스크립트** 확인
-	카테고리 관리: 채팅 상담 시 상담원이 해당 채팅 상담에 대해 입력하는 고객의 **처리유형**을 1~3 뎁스까지 설정 가능

### 문의 접수/처리
#### 채팅 접수
![](http://static.toastoven.net/prod_contact_center/5.2-(1).png)
헬프센터 내에 채팅 기능이 활성화된 상태에서 (채팅 기능 활성화: [서비스 관리 → 헬프센터 → 구성관리](https://github.com/TOAST-DOCS/Contact-Center/blob/alpha/ko/online-contact-guide-service-management.md#%EA%B5%AC%EC%84%B1%EA%B4%80%EB%A6%AC) 탭) 고객이 헬프센터에 접속하면, 홈페이지 우측 하단에 ① **채팅 아이콘**이 표시됩니다.

![](http://static.toastoven.net/prod_contact_center/5.2-(2).png)
채팅 아이콘을 클릭했을 때 온라인 상태의 상담원이 없을 경우 **상담원 부재중** 팝업이 뜨며, ① **문의하기**로 이동하여 1:1문의를 남길 수 있도록 안내됩니다.

![](http://static.toastoven.net/prod_contact_center/5.2-(3).png)
채팅 아이콘을 클릭했을 때 온라인 상태의 상담원이 있을 경우 채팅 대화창이 생성되며, ① **개인정보 수집 동의** 시 상담원과의 채팅을 시작할 수 있습니다. 상담원 상태 변경에 관련해서는 다음 단락인 채팅 처리에서 안내됩니다. 

#### 채팅 처리
![](http://static.toastoven.net/prod_contact_center/5.2-(4).png)
헬프센터 내에 채팅 기능이 활성화된 상태에서 (채팅 기능 활성화: [서비스 관리 → 헬프센터 → 구성관리](https://github.com/TOAST-DOCS/Contact-Center/blob/alpha/ko/online-contact-guide-service-management.md#%EA%B5%AC%EC%84%B1%EA%B4%80%EB%A6%AC) 탭) 상담원이 Online Contact에 접속하면, 홈페이지 우측 하단에 ① **채팅 아이콘**이 표시되며, 해당 아이콘 클릭 시 채팅 상담을 진행할 수 있는 화면이 표시됩니다.

![](http://static.toastoven.net/prod_contact_center/5.2-(5).png)
채팅 화면 좌측 상단의 ① **상태 창**에서는 고객의 채팅 문의를 처리하기 위한 상태 값을 변경하실 수 있습니다. 온라인, 휴식, 오프라인의 세 가지 값 중에서 하나를 선택하실 수 있으며, **온라인 상태일때만** 채팅 문의를 할당 받으실 수 있습니다.

고객의 문의가 접수되면 채팅 아이콘이 깜빡이며 채팅 상담이 요청되었음을 표시합니다. 채팅 아이콘을 클릭하여 채팅 화면으로 접속하시면 상태 창 아래 진행 중인 상담을 표시하는 ② **대화중** 카운트가 올라가면서 채팅 상담을 요청한 고객을 확인하실 수 있으며, 고객명을 클릭하면 고객과 채팅 상담을 진행할 수 있는 **채팅 창**, **고객정보**, **상담정보**, **티켓 만들기** 버튼이 표시됩니다. 

고객정보와 상담정보에서 확인 및 입력하실 수 있는 항목은 다음과 같습니다.

③ **고객정보**
-	이름
-	이메일
-	메모
-	IP주소
-	디바이스

④ **상담정보**
-	채널: 채팅 상담 요청 시 **접속한 경로**
-	처리유형: 상담원이 해당 고객과의 채팅 상담에 대해 입력하는 **처리유형**으로, [서비스 관리 → 채팅 → 카테고리 관리](https://github.com/TOAST-DOCS/Contact-Center/blob/alpha/ko/online-contact-guide-service-management.md#%EC%B9%B4%ED%85%8C%EA%B3%A0%EB%A6%AC-%EA%B4%80%EB%A6%AC) 탭에서 설정 가능

채팅 상담에 부가하여 고객의 요청 사항에 대해 처리되어야 할 내용이 있을 경우, ⑤ **티켓 만들기** 버튼을 통해 채팅에 대한 티켓을 생성하실 수 있습니다.

고객정보와 상담정보 입력 및 수정 후 저장 버튼을 누르지 않은 채로 대화가 종료되면 정보가 저장되지 않으므로, 대화 종료 전 ⑥ **저장** 버튼을 반드시 눌러주세요.

### 만족도 평가 및 대화 종료
![](http://static.toastoven.net/prod_contact_center/5.3-(1).png)
![](http://static.toastoven.net/prod_contact_center/5.3-(2).png)
채팅이 완료된 후 고객이 채팅 상담에 대한 만족도 평가를 직접 진행하거나, 또는 상담원이 평가 요청을 전송해 만족도 평가를 안내할 수 있습니다. 고객이 직접 채팅 화면 상단 ① **평가** 버튼을 클릭하면 바로 만족도 평가 화면이 표시되며, 상담원이 채팅 화면 상단 **평가** 버튼을 누를 경우 만족도 안내 메시지가 ([서비스 관리 → 채팅 → 기본설정](https://github.com/TOAST-DOCS/Contact-Center/blob/alpha/ko/online-contact-guide-service-management.md#%EA%B8%B0%EB%B3%B8-%EC%84%A4%EC%A0%95) 탭에서 설정) 전송됩니다.

채팅 상담이 종료되면 ② **대화 종료** 버튼을 통해 상담을 종료할 수 있습니다. 고객이 대화를 종료했을 경우 상담원이 대화 종료 버튼을 누르기 전까지 채팅 화면에서 고객정보 및 상담정보의 입력과 티켓 생성이 가능하지만, 상담원이 대화 종료 버튼을 눌렀을 경우 채팅 화면에서는 더이상 해당 채팅 상담을 확인하실 수 없으며, 대화 종료 이후의 정보 입력 및 수정, 티켓 생성은 [채팅 → 채팅기록](https://github.com/TOAST-DOCS/Contact-Center/blob/alpha/ko/online-contact-guide-chat.md#%EC%B1%84%ED%8C%85-%EA%B8%B0%EB%A1%9D) 메뉴에서만 가능하므로 대화를 종료하시기 전 유의해주세요. 

### 채팅 기록
![](http://static.toastoven.net/prod_contact_center/5.4-(1).png)
Online Contact에서 진행한 **채팅 상담 기록**을 확인하실 수 있습니다. 개별 채팅 기록을 클릭하면, ① 해당 채팅 상담에 대한 구체적인 정보를 확인하실 수 있는 창이 화면 오른쪽에 표시됩니다. **고객정보** 및 **상담정보**를 확인 및 입력하실 수 있으며, **티켓의 생성**, **채팅 대화 내역 확인**이 가능합니다.

채팅 기록 중 조건에 맞는 기록을 ② **검색**하실 수 있으며, **데이터 추출** 버튼을 통해 조건에 맞는 채팅 기록을 엑셀 파일로 추출할 수 있습니다.

채팅 기록에서 확인하실 수 있는 ③ **상태 값**은 다음과 같이 구분됩니다.
-	처리: 상담원이 대기 목록에서 고객의 상담 요청을 클릭한 후 **답변을 전송**했을 경우
-	미처리: 상담원이 대기 목록에서 고객의 상담 요청을 클릭하지 않았거나, 메시지에 대한 답변을 전송하지 않은 경우 ([통계](https://github.com/TOAST-DOCS/Contact-Center/blob/alpha/ko/online-contact-guide-report.md#contact-center--online-contact--%EC%84%9C%EB%B9%84%EC%8A%A4-%EA%B0%80%EC%9D%B4%EB%93%9C--%ED%86%B5%EA%B3%84) 메뉴에서의 **포기**와 동일)