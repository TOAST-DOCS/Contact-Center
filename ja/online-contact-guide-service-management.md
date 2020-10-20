## Contact Center > Online Contact > 서비스 가이드 > 서비스 관리

서비스 관리 메뉴에는 SSO 로그인 설정, 티켓 설정, 상담원 관리, 헬프센터 템플릿 관리 등 **문의의 접수와 처리를 위한 상세 설정 기능**이 포함되어 있습니다.
해당 메뉴에서 설정하시는 헬프센터의 구성 또는 세부 기능들은, 아래와 같은 경로로 접근하실 수 있는 각 서비스별 헬프센터에서 적용과 동시에 바로 확인하실 수 있습니다.


### 헬프센터 접속
- Online Contact 우측 맨 하단 **헬프센터 바로가기**
- https:// **도메인명** .oc.toast.com/ **서비스ID** /hc

도메인명은 Online Contact 조직 생성 시 작성하신 정보로, TOAST CONSOLE → 조직 설정 → 도메인 설정에서 수정하실 수 있습니다. 서비스ID는 [전체 관리 → 서비스](https://alpha-docs.toast.com/ko/Contact%20Center/ko/online-contact-guide-global-management/#_1) 메뉴에서 서비스 추가 시 입력하셨던 정보로, 최초 생성 이후 수정이 불가합니다.


## 인증
[전체 관리 → SSO 로그인](https://github.com/TOAST-DOCS/Contact-Center/blob/alpha/ko/online-contact-guide-global-management.md#sso-%EB%A1%9C%EA%B7%B8%EC%9D%B8) 메뉴에서 등록하셨던 **SSO 로그인**과, **OPEN API** 기능을 활성화/비활성화할 수 있습니다.


### SSO 로그인
![](http://static.toastoven.net/prod_contact_center/2.2.1-(1).png)
SSO 로그인을 활성화하실 경우 **활성화** 버튼을 클릭하신 후, [전체 관리 → SSO 로그인](https://alpha-docs.toast.com/ko/Contact%20Center/ko/online-contact-guide-global-management/#sso) 메뉴에서 등록하셨던 SSO 로그인을 선택하시고 저장하시면 됩니다.


### OPEN API
![](http://static.toastoven.net/prod_contact_center/2.2.1-(2).png)
OPEN API 탭에서는 외부에서 Online Contact의 데이터에 접근할 수 있도록 하는 **① OPEN API 활성화**, **② API Key 변경**, **③ 접속 IP 제한 설정**이 가능하며, 접속 IP 제한을 설정할 시 설정한 IP에서만 OPEN API를 호출하실 수 있습니다.


## 채팅
채팅 기능에 관련된 항목들입니다. 채팅 기능은 [서비스 관리 → 헬프센터 → 구성관리](https://alpha-docs.toast.com/ko/Contact%20Center/ko/online-contact-guide-service-management/#_26)에서 활성화하실 수 있으며, 활성화된 이후에 노출되는 우측 하단 **채팅 아이콘**으로 접속 가능합니다. 

![](http://static.toastoven.net/prod_contact_center/2.2.2-(1).png)
**채팅 아이콘**을 통해 접속한 후 **①** 좌측 상단 **상태 값**을 클릭하시면 (초기 기본값 ‘오프라인’) 온라인/휴식/오프라인 중 하나로 상태를 설정하실 수 있으며, 온라인 상태일 경우에만 고객의 채팅 요청에 답변할 수 있습니다.


### 기본 설정
![](http://static.toastoven.net/prod_contact_center/2.2.2-(2).png)
**①** 채팅 연결 시 고객에게 자동으로 발송되는 **인사말**과, **②** 고객에게 평가 요청 시 발송되는 **만족도 안내 메시지**를 설정할 수 있습니다. 평가 요청은 채팅 화면 상단 **평가** 버튼을 통해 고객에게 전송할 수 있습니다.


### 상담원 할당 설정
![](http://static.toastoven.net/prod_contact_center/2.2.2-(3).png)
**①** 채팅을 요청한 고객과의 최근 채팅 기록이 있는 상담원에게 채팅을 **우선 할당**할 것인지, 또는 **임의로 배분**할 것인 지 선택이 가능합니다.


### 채팅화면 삽입 코드
![](http://static.toastoven.net/prod_contact_center/2.2.2-(4).png)
기존에 관리하시던 서비스 페이지에 Online Contact가 제공하는 채팅 서비스만 제공하고 싶은 경우 제공되는 코드입니다. **①** 제공되는 인입 스크립트를 복사하여 웹사이트 HTML 소스 코드의 </body> 태그 앞에 삽입해주세요.


### 카테고리 관리
![](http://static.toastoven.net/prod_contact_center/2.2.2-(5).png)
채팅 상담 시 상담 고객에 대해 상담원이 직접 입력하는 상담정보 항목 중 **처리유형의 카테고리**를 관리할 수 있는 메뉴입니다. 처리유형을 1~3 뎁스까지 설정하실 수 있습니다.

**①** 상위 카테고리를 먼저 추가하신 후, 하위 뎁스에 카테고리를 추가할 시 상위 카테고리를 먼저 클릭하셔서 선택된 것을 확인하신 후 하위 카테고리를 추가해주세요. 색으로 강조된 카테고리 아래에 새로운 하위 카테고리가 생성됩니다.

동일 뎁스 내에서 카테고리명 **중복은 불가능**합니다. (뎁스가 다를 경우는 가능)


## 티켓
티켓 메뉴에서는 고객의 문의 접수 또는 문의 처리 시 선택하는 카테고리 관리, 업무 효율화를 높일 수 있는 트리거 기능, 고객센터 문의 접수 화면 구성 필드, 템플릿 관리, 이메일 설정 메뉴를 사용할 수 있습니다.


### 카테고리 관리
![](http://static.toastoven.net/prod_contact_center/2.2.3-(1).png)
헬프센터에서 고객이 문의를 접수할 시 선택하는 유형인 **접수유형**과, 상담원이 티켓 처리 시 선택하는 **처리유형**을 1~5뎁스까지 설정할 수 있습니다.

**①** 상위 카테고리를 먼저 추가하신 후, 하위 뎁스에 카테고리를 추가할 시 상위 카테고리를 먼저 클릭하셔서 선택된 것을 확인한 후 추가해주세요. 색으로 강조된 카테고리 아래에 새로운 하위 카테고리가 생성됩니다. 동일 뎁스 내에서 카테고리명 **중복은 불가능**합니다. (뎁스가 다를 경우는 가능)

**②** 우측 상단 **복사** 버튼을 통해 추가된 카테고리에 자동으로 부여되는 **카테고리 ID**를 복사할 수 있으며, **③ 데이터 추출** 버튼을 통해 전체 카테고리 정보를 **엑셀 파일로 추출**할 수 있습니다. 추출되는 정보는 다음과 같습니다.


#### 데이터 추출 시 추출되는 정보
-	카테고리 ID
-	카테고리 명
-	뎁스
-	상위 카테고리 ID
-	수정시간
-	생성시간


### 트리거
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2).png)
트리거는 반복적인 업무를 **자동화**하여 업무 생산성을 높이기 위한 기능입니다. 특정 조건이 충족될 경우 조건에 따른 결과 행위를 자동으로 실행합니다. 또한 결과에 대한 알림 메일이 발송될 수 있도록 설정도 가능합니다.

예시) `티켓의 접수유형` = `무통장입금`일 경우 `필수`적으로 `결제` 그룹의 `예시01` 상담원에게 `티켓을 할당`

**① 트리거 추가** 버튼을 누르신 후 제목, 조건, 결과를 모두 입력하시고 **저장** 버튼을 누르시면 트리거가 자동으로 활성화됩니다. 활성화된 트리거는 **② 비활성화** 버튼을 통해 비활성화하실 수 있으며, **③ 수정** 버튼을 통해 조건 또는 결과를 수정하실 수 있습니다.

✔ **\[FAQ 바로가기]** [접수된 문의를 자동으로 외부 포워딩 하고 싶습니다.](https://nhn-contact.oc.toast.com/oc/hc/article/43/)
✔ **\[FAQ 바로가기]** [특정 조건에서 알림 메일을 보내고 싶습니다.](https://nhn-contact.oc.toast.com/oc/hc/article/42/)

#### 트리거 조건 유형
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2)a.png)

#### 트리거 조건 상세
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2)b.png)

#### 트리거 결과 유형
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2)c.png)


### 필드
필드 메뉴는 Help Center 내부 문의하기 기능을 사용할 시 기입하는 항목들의 유형을 설정할 수 있는 기능으로, **문의 접수/처리에 필요한 항목들**의 순서를 설정할 수 있습니다. 설정한 그대로 고객 문의하기 화면에 구현됩니다.

![](http://static.toastoven.net/prod_contact_center/2.2.3-(3).png)
필드는 **① 고객 필드**와 **② 상담원 필드**로 구분됩니다. 필드 설정 또는 관리 탭을 선택하시기 전에 상담원 필드를 관리하실 것인지, 고객 필드를 관리하실 것인지 먼저 선택해주세요.

-	상담원 필드: 티켓 상세 화면에 보이는 문의 항목
-	고객 필드: 헬프센터 → 문의하기 기능에서 고객에게 보이는 문의 항목


#### 필드 설정
![](http://static.toastoven.net/prod_contact_center/2.2.3-(4).png)
**①** 앞서 [티켓 → 카테고리 관리](https://alpha-docs.toast.com/ko/Contact%20Center/ko/online-contact-guide-service-management/#_9)에서 등록해두신 접수유형에 따라 문의내역에 필요한 필드를 다르게 설정하실 수 있습니다. **접수유형**을 클릭하시면 설정해두신 필드를 열람하실 수 있으며, 개인정보수집 항목을 제외한 필드들의 **②** 순서를 변경하실 수 있습니다. (개인정보수집 항목의 경우 항상 맨 아래 노출되도록 고정됨)

또한 필드 관리 탭에서 추가해두신 필드를 **③** 새롭게 **추가**하시거나, 이미 추가하신 필드를 **④ 제거**하실 수 있습니다.


#### 필드 관리
![](http://static.toastoven.net/prod_contact_center/2.2.3-(5).png)
**①** 필드 설정 탭에서 각 접수유형에 맞게 필드를 추가할 수 있도록 필드 관리 탭에서 개별 필드를 관리합니다. 기본 필드는 삭제 대신 **수정** 또는 필드 설정의 **초기화**만 가능하며, 직접 만드신 필드의 경우 **수정**과 **삭제** 모두 가능합니다.


![](http://static.toastoven.net/prod_contact_center/2.2.3-(6).png)
필드를 추가하실 때 입력해야 하는 항목은 다음과 같습니다.

-	**①** 항목 유형: 필드의 **항목 유형**입니다. 항목유형을 선택하시면 기본 설정 하단에 **상세 설정**과 **미리보기**가 표시됩니다. 상세설정을 통해 해당 항목에 표시될 값을 설정할 수 있으며, 
  미리보기를 통해 고객의 화면에서 해당 필드가 어떻게 보일지 확인할 수 있습니다.
-	**②** 항목 코드: Open API로 문의하기 기능을 개발할 시 해당 필드를 나타내는 고유한 값으로 사용됩니다.
-	**③** 항목 명: 필드의 이름으로, 문의하기 화면에 필드와 함께 표시됩니다.
-	**④** 안내 문구: 필드에 대한 안내 문구로, 문의하기 화면에 필드와 함께 표시됩니다.
-	**⑤** 필수 여부: 설정 시 항목 명 오른쪽에 \*(별표)로 표시되며, 반드시 입력되어야 다음 단계로 넘어갈 수 있습니다. 기본 필드 중 제목, 이메일, 유형, 내용, 개인정보수집 필드는 필수입력 항목에 대해 ‘아니오’ 설정이 불가합니다.
-	**⑥** 개인정보 (암호화 여부)
-	**⑦** 개인정보 파기 여부


### 템플릿 관리
![](http://static.toastoven.net/prod_contact_center/2.2.3-(7).png)
템플릿 관리 메뉴는 자주 접수되는 문의 유형에 대한 **답변 템플릿을 미리 추가**하여 티켓을 신속하게 처리할 수 있는 기능입니다. 티켓 관리 메뉴에서 티켓을 처리할 시 선택 가능하며, 템플릿을 제작할 시 설정된 접수유형과 티켓의 접수유형이 같을 경우 선택할 수 있습니다.

**①** 상단 좌측 **템플릿 추가** 버튼을 통해 템플릿을 추가하실 수 있으며, 템플릿 추가 시 선택하는 접수유형은 앞서 [티켓 → 카테고리 관리](https://alpha-docs.toast.com/ko/Contact%20Center/ko/online-contact-guide-service-management/#_9)에서 등록해두신 접수 유형입니다. 내용 본문 부분에서 마우스 우 클릭 시 링크, 이미지, 테이블을 삽입하실 수 있습니다.

✔ **\[FAQ 바로가기]** [답변 템플릿은 어떻게 사용하나요?](https://nhn-contact.oc.toast.com/oc/hc/article/39/)
✔ **\[FAQ 바로가기]** [티켓 답변 템플릿을 등록했는데, 답변 작성 시 조회되지 않아요.](https://nhn-contact.oc.toast.com/oc/hc/article/62/)


### 이메일 설정
![](http://static.toastoven.net/prod_contact_center/2.2.3-(8).png)
Online Contact에서 도메인을 제공하는 **① 대표 계정 주소**를 생성하실 수 있으며, **② 외부 계정 등록**을 통해 서비스 도메인을 사용하는 서비스 대표 계정을 등록하실 수도 있습니다. 

**③** Online Contact를 통해 발신되는 이메일의 **발신자 명**과 **발신자 주소**를 저장하실 수 있으며, **④** 모든 발송 메일에 대한 공통적인 **메일 레이아웃**을 설정하실 수 있습니다. 본문의 치환코드 (#{content})를 삭제할 경우 답변 메일에서 각 항목에 대한 내용이 보이지 않을 수 있으니 템플릿 작성 시 유의해주세요. 또한 앞서 티켓 → 템플릿 관리에서 작성하신 템플릿을 비롯하여 모든 발송 메일에 적용되는 공통적인 메일 레이아웃이므로, 템플릿 간 내용 충돌이 일어나지 않도록 유의해주세요.

✔ **\[FAQ 바로가기]** [현재 사용하고 있는 외부 이메일을 연결하여 문의를 접수 받고 싶습니다.](https://nhn-contact.oc.toast.com/oc/hc/article/44/)

## 상담원
상담원 메뉴에서는 고객 문의 처리 (티켓 및 채팅 상담)을 위해 상담원과 그룹을 추가 및 수정하고, 상담원 별로 그룹과 권한을 설정할 수 있습니다.

### 상담원
![](http://static.toastoven.net/prod_contact_center/2.2.4-(1).png)
상담원으로 추가할 사용자는 **IAM 회원**으로 등록되어 있어야 합니다.


#### IAM 회원 등록
-	화면 우측 상단 **① 회원 초대** 버튼 → 이름, ID, 이메일 입력
-	TOAST CONSOLE → 멤버 관리 → IAM 회원 탭 → IAM 회원 등록 버튼 → ID, 이름, 메일, 휴대폰 번호 입력

위 두 방법 중 한가지를 선택하셔서 IAM 회원을 등록하시고, **② 상담원 추가** 버튼 → **상담원 조회** 버튼 → 등록된 IAM 회원을 이름/계정/이메일 중 일부 정보 입력을 통해 조회하신 후 추가하실 수 있습니다.

상담원을 추가하실 때에는 반드시 그룹을 배정해야 하므로, 추가된 그룹이 없을 경우 **그룹을 먼저 추가**하신 후 상담원 추가를 진행해주세요.

상담원 추가 시 설정할 수 있는 **권한**은 다음과 같습니다.
-	슈퍼관리자: **관리자** 권한 + **전체 관리** 메뉴 기능
-	관리자: 일반 상담원 + **서비스 관리** 메뉴 기능
-	일반 상담원: **채팅** 및 **티켓** 상담
-	티켓 상담원: **티켓** 상담


### 그룹
![](http://static.toastoven.net/prod_contact_center/2.2.4-(2).png)
그룹 메뉴에서는 그룹의 **① 추가**, **② 수정**, **③ 삭제**가 가능합니다. 그룹별 상담원을 구성할 경우 티켓 → 트리거 상에서 해당 그룹에 유형별 문의를 할당하거나, 알림 메일이 전송되도록 설정할 수 있습니다. 

#### 그룹 추가
![](http://static.toastoven.net/prod_contact_center/2.2.4-(3).png)
상단 좌측 **그룹 추가** 버튼을 누르신 후, 그룹 명을 입력해주시고 할당될 상담원을 선택하신 뒤 **①** ‘ **>** ‘ 버튼을 통해 할당된 상담원으로 이동해주세요. 반대로 상담원을 할당 해제하실 때는 ‘ **<** ‘ 버튼을 통해 미할당 상담원으로 이동하실 수 있습니다. 상담원 할당을 마친 후 **②** **저장** 버튼을 눌러 주시면 그룹 설정이 적용됩니다.

상담원을 할당하시지 않고도 그룹을 추가하실 수 있으므로, 그룹의 최초 추가 시에는 그룹 명만 입력하신 다음 **저장** 버튼을 눌러 주시면 상담원 추가를 진행하실 수 있습니다.


## 헬프센터
### 템플릿 관리
![](http://static.toastoven.net/prod_contact_center/2.2.5-(1).png)
헬프센터 페이지 **디자인 테마 관리** 메뉴로, 각 서비스별 세부 영역에 대한 디자인을 수정할 수 있는 편집 editor를 PC/모바일 템플릿 관리 메뉴에서 제공합니다.

기본으로 두 가지의 템플릿이 제공되며, **① 템플릿 등록** 버튼을 통해 새로운 템플릿을 추가하실 수 있습니다. 추가하신 템플릿은 **② 수정** 또는 **삭제**하실 수 있으며, 활성화 중인 템플릿은 삭제가 불가하므로 다른 템플릿을 활성화하신 다음 삭제해주세요.


![](http://static.toastoven.net/prod_contact_center/2.2.5-(2).png)
템플릿 추가 및 수정 시 **① CSS / HTML / JS 스크립트**를 주어진 편집기에 직접 작성하시거나 [서비스 관리 → 헬프센터 → 파일업로드 관리](https://alpha-docs.toast.com/ko/Contact%20Center/ko/online-contact-guide-service-management/#_25) 메뉴에서 필요하신 파일(스크립트, 폰트, 이미지 등)을 업로드하신 후 리소스의 경로를 입력하심을 통해 헬프센터의 구성을 변경하실 수 있습니다. 편집 후 **미리보기** 버튼을 통하여 편집 내용이 헬프센터에 적용된 모습을 바로 보실 수 있으며, **저장**하신 후 적용이 가능합니다.

✔ **\[FAQ 바로가기]** [헬프센터 PC/모바일 템플릿 관리 기능의 구체적인 예시가 궁금해요.](https://nhn-contact.oc.toast.com/oc/hc/article/60/)

**CSS 수정 시** 활용하실 수 있는 주요한 요소들은 다음과 같습니다.

#### main.css
| 요소 이름                                                 | 설명                                |
| -------------------------------------------------------- | ----------------------------------- |
| .main_banner                                             | 메인 상단 배너 영역                  |
| .main_banner img                                         | 메인 상단 배너 영역 이미지            |
| .carousel-caption .title_txt                             | 메인 상단 배너 영역 제목              |
| .carousel-caption .sub_txt                               | 메인 상단 배너 영역 소제목            |
| .search-box                                              | 메인 상단 배너 영역 검색상자          |
| .search-box .icon-ic-search                              | 메인 상단 배너 영역 검색아이콘        |
| #supports .container-con                                 | 메인 고객센터 구성요소 영역           |
| #supports .support__item:nth-child(1):before             | 메인 공지사항 아이콘                 |
| #supports .support__item:nth-child(2):before             | 메인 FAQ 아이콘                      |
| #supports .support__item:nth-child(3):before             | 메인 문의하기 아이콘                  |
| #supports .support__item:nth-child(4):before             | 메인 문의내역 아이콘                  |
| #supports .support__item .card-title .btn                | 메인 구성요소 제목                    |
| #supports .support__item .card-title .btn:hover          | 메인 구성요소 제목 호버 시 색 변경     |
| #supports .support__item .card-title .btn:after          | 메인 구성요소 텍스트 우측 화살표 아이콘 |
| #supports .support__item .card-text                      | 메인 구성요소 설명 텍스트              |
| #sec_contact-news .textArea                              | 메인 하단 배너 영역                   |
| #sec_contact-news .textArea .text-item h3                | 메인 하단 배너 영역 제목               |
| #sec_contact-news .textArea .text-item .icon-more::after | 메인 하단 배너 영역 더보기 아이콘       |
| #sec_contact-news .textArea .text-item li                | 메인 하단 배너 영역 게시글 리스트       |
| #chat-offline                                            | 상담원 부재중 박스                     |
| #chat-offline .title                                     | 상담원 부재중 박스 제목                |
| #chat-offline .text                                      | 상담원 부재중 박스 텍스트              |
| #chat-offline .close                                     | 상담원 부재중 박스 닫기 아이콘          |
| #chat-offline .btn                                       | 상담원 부재중 박스 문의하기 아이콘      |


#### faq.css
| 요소 이름                              | 설명                                |
| ------------------------------------- | ----------------------------------- |
| .lnb--fixed .lnb--fixed__nav          | 세부 페이지 좌측 LNB                 |
| .help-center-title                    | 세부 페이지 좌측 LNB 제목             |
| .lnb__nav                             | 세부 페이지 좌측 LNB 리스트           |
| .lnb__nav li a                        | 세부 페이지 좌측 LNB 리스트 개별      |
| .lnb__nav li.on a                     | 세부 페이지 좌측 LNB 리스트 선택      |
| .lnb--fixed__side-divider             | 세부 페이지 LNB/contents 구분선      |
| .lnb--fixed__content                  | 세부 페이지 콘텐츠 영역               |
| .tit_txt                              | 세부 페이지 콘텐츠 영역 제목          |
| .data_info-box                        | 세부 페이지 콘텐츠 영역 박스          |
| .tab_category                         | 세부 페이지 콘텐츠 영역 카테고리 탭    |
| .tab_category>li.on                   | 세부 페이지 콘텐츠 영역 카테고리 선택  |
| .tab_category>li                      | 세부 페이지 콘텐츠 영역 카테고리 개별  |
| .tbl_wrap                             | 세부 페이지 콘텐츠 영역 리스트         |
| .faqData th:nth-child(1)              | FAQ 테이블 카테고리                   |
| .faqData th:nth-child(2)              | FAQ 테이블 제목                       |
| .faqData th:nth-child(3)              | FAQ 테이블 등록일                     |
| .faqData tr.hot-text td               | FAQ 테이블 개별 상단고정 카테고리      |
| .faqData tr.hot-text td .title-info a | FAQ 테이블 개별 상단고정 제목          |
| .faqData td .title-info sup           | FAQ 테이블 개별 상단고정 HOT          |
| .gocont .search                       | FAQ 검색                             |
| .sel                                  | FAQ 검색 말머리                      |
| .search .inp                          | FAQ 검색어 입력                      |
| .search .btnArea                      | FAQ 검색 버튼                        |
| .faqData_info-con                     | FAQ 세부 문서 콘텐츠                 |
| .faqData_info-con .dataTit            | FAQ 세부 문서 제목                   |
| .faqData_info-con .dataTime           | FAQ 세부 문서 등록일                 |
| .faqData_info-con .dataTextBox        | FAQ 세부 문서 내용 텍스트            |
 

#### notice.css
| 요소 이름                                               | 설명                                |
| ------------------------------------------------------ | ----------------------------------- |
| .el-breadcrumb                                         | 세부 페이지 우측 상단 텍스트 영역      |
| .el-breadcrumb li                                      | 세부 페이지 우측 상단 텍스트 영역 개별 |
| .noticeData                                            | 공지사항 테이블                       |
| .noticeData th:nth-child(1)                            | 공지사항 테이블 번호                  |
| .noticeData th:nth-child(2)                            | 공지사항 테이블 제목                  |
| .noticeData th:nth-child(3)                            | 공지사항 테이블 말머리                |
| .noticeData th:nth-child(4)                            | 공지사항 테이블 등록일                |
| .noticeData tr.hot-text                                | 공지사항 테이블 개별 상단고정          |
| .noticeData tr.hot-text td                             | 공지사항 테이블 개별 상단고정 번호     |
| .noticeData tr.hot-text td .title-info a               | 공지사항 테이블 개별 상단고정 제목     |
| .noticeData td .title-info sup                         | 공지사항 테이블 개별 상단고정 HOT      |
| .icon-leavel-1                                         | 공지사항 테이블 개별 상단고정 말머리   |
| .noticeData tr                                         | 공지사항 테이블 개별                  |
| .noticeData td .title-info a                           | 공지사항 테이블 개별 제목             |
| .upload-text-memo                                      | 문의하기 첨부파일 필드 텍스트          |
| .faqData_info-con .dataTime .noticeType                | 공지사항 세부 문서 카테고리            |
| .faqData_info-con .dataTime .noticeType .icon-leavel-1 | 공지사항 세부 문서 카테고리 아이콘      |


#### search.css-
| 요소 이름                                           | 설명                                |
| -------------------------------------------------- | ----------------------------------- |
| .paginate                                          | 페이지네이션 영역                    |
| .paginate li                                       | 페이지네이션 개별                    |
| .paginate li.firstPage a                           | 페이지네이션 << 키                   |
| .paginate li.firstPage a.img                       | 페이지네이션 << 키 이미지             |
| .paginate li.prev a.                               | 페이지네이션 < 키                    |
| .paginate li.prev a img                            | 페이지네이션 < 키 이미지              |
| .paginate li a                                     | 페이지네이션 개별 페이지              |
| .paginate li.number.active a                       | 페이지네이션 현재 페이지              |
| .paginate li.next a.                               | 페이지네이션 > 키                    |
| .paginate li.next a img                            | 페이지네이션 > 키 이미지              | 
| .paginate li.lastPage a                            | 페이지네이션 >> 키                   |
| .paginate li.lastPage a.img                        | 페이지네이션 >> 키 이미지             |
| .search-title                                      | 검색결과 제목                        |
| .search-title strong                               | 검색결과 제목 검색어 강조             |
| .search-text                                       | 검색결과                             |
| .search-text .search-title_sub                     | 검색결과 하위분류                     |
| .search-text .search-text_lit                      | 검색결과 개별                        | 
| .search-text .search-text_lit dt a                 | 검색결과 개별 제목                    |
| .search-text .search-text_lit dd .search-text_con  | 검색결과 개별 내용 미리보기            |
| .search-text .search-text_lit dd .search-text_time | 검색결과 개별 작성일                  |


#### inquiry.css
| 요소 이름                                                                  | 설명                                |
| ------------------------------------------------------------------------- | ----------------------------------- |
| .selectStyle                                                              | 검색 내부 옵션                       |
| .inquiry-con                                                              | 문의하기 콘텐츠 영역                  |
| .inquiry-con_table                                                        | 문의하기 테이블                       | 
| .inquiry-con_table th                                                     | 문의하기 테이블 필드                  |
| .bl_ess                                                                   | 문의하기 테이블 필드 필수 *           |
| .inquiry-con_table td                                                     | 문의하기 테이블 입력                  |
| .error_txt                                                                | 문의하기 테이블 입력 에러 텍스트       | 
| .inquiry-btn                                                              | 문의하기 접수 버튼                    |
| .layui-icon                                                               | 화살표 버튼                          |
| .layui-icon-right                                                         | > (좌측 방향) 화살표 버튼             |
| .layui-icon-up                                                            | V (아래 방향) 화살표 버튼             |
| .check_area_wrap .td-radio .layui-form-checkbox\[lay-skin="primary"] span | 체크박스 텍스트                       |
| .error_txt                                                                | 에러 텍스트                          |


### 파일업로드 관리
![](http://static.toastoven.net/prod_contact_center/2.2.5-(3).png)
답변 템플릿 및 레이아웃 작성에 사용될 파일을 관리하는 도구로, **① 파일 업로드** 버튼을 통해 사용할 파일을 직접 업로드하시면 매번 필요한 파일을 새롭게 업로드할 필요 없이 제공되는 해당 리소스의 **② 파일 경로**를 통해 사용하실 수 있습니다.

기존에 동일 파일명으로 업로드된 내역이 있을 경우 업로드가 불가하니, 파일명이 중복되지 않도록 유의해주세요.


### 구성관리
![](http://static.toastoven.net/prod_contact_center/2.2.5-(4).png)
헬프센터의 구성 항목 중 사용하는 기능은 **활성화**, 사용하지 않는 기능은 **비활성화** 처리하실 수 있습니다. 비활성화 시 헬프센터 화면에서 **숨김** 처리됩니다.

관리 가능한 기능은 다음과 같습니다.
-	공지사항
-	FAQ (자주 묻는 질문)
-	1:1 문의 & 문의 내역 (문의하기)
-	채팅


## 외부채널
**외부 SNS로 인입되는 문의**를 Online Contact에서 티켓으로 전환하여 처리할 수 있습니다. 현재 **트위터**와 **카카오 상담톡**을 지원하고 있습니다.


### 트위터
![](http://static.toastoven.net/prod_contact_center/2.2.6-(1).png)
트위터 채널 연동을 **① 활성화** 또는 **비활성화**하실 수 있으며, 활성화 시 우측 **② 등록** 버튼을 통해 트위터 계정을 등록하실 수 있습니다. 


![](http://static.toastoven.net/prod_contact_center/2.2.6-(2).png)
계정 등록 시 **① 트윗**(멘션)과 **② 메시지**에 대한 티켓 전환 여부를 각각 설정하실 수 있으며, 만약 메시지를 티켓으로 전환하여 받아 보기를 희망하시는 경우 아래 절차를 확인해주세요.

이용하고 계시는 트위터 계정 접속 → 더보기 → 설정 및 개인정보 → 개인정보 및 보안 → 쪽지 (Direct Messages) → **쪽지 요청 받기** 항목이 체크되어 있어야 연결된 계정으로 오는 쪽지가 티켓으로 접수될 수 있습니다.

✔ **\[FAQ 바로가기]** [외부채널 (트위터/카카오 상담톡) 연결을 활성화했을 때 문의의 인입/답변 과정은 어떻게 되나요?](https://nhn-contact.oc.toast.com/oc/hc/article/61/)

### 카카오 상담톡
![](http://static.toastoven.net/prod_contact_center/2.2.6-(3).png)
상담톡 연동을 ① **활성화** 또는 **비활성화**하실 수 있으며, 활성화 시 우측 **② 등록** 버튼을 통해 카카오 플러스친구 ID와 활성화 희망일을 입력해주세요. 연결은 영업일 기준 최대 1~2일 소요되며, 연결이 반려될 경우 반려 사유 메시지가 표시되므로 확인해주세요. 카카오톡채널 관리자센터에서 관리 → 상세설정 → 채널 홈 → 공개설정을 **ON**으로 변경해야 연결 가능합니다.


![](http://static.toastoven.net/prod_contact_center/2.2.6-(4).png)
연결이 완료된 **계정을 클릭**하시면 상담톡 기능의 세부 요소들을 설정할 수 있습니다.
- **①** 상담시간
- **②** 채팅가능 요일
- **③** 자동 멘트
    - 업무시간 외 자동 멘트: **설정한 상담시간 외**에 채팅이 접수되었을 경우 자동으로 발송되는 멘트
    - 첫 인사 자동 멘트: **채팅이 연결**되었을 시 자동으로 발송되는 멘트
    - 상담원 부재 자동 멘트: **온라인 상태**의 상담원이 **없을 시** 자동으로 발송되는 멘트
    - 평가 요청 자동 멘트: 상담원이 **평가 요청**을 전송했을 시 함께 발송되는 멘트
    - 상담종료 자동 멘트: **상담 종료** 시 자동으로 발송되는 멘트

상담톡 서비스가 활성화되면 기존 플러스친구 1:1 채팅은 중단되며, 카카오톡을 통해 접수되는 문의는 Online Contact에서 제공하는 채팅 기능에 유입 채널 ‘**카카오**’로 표시되어 접수됩니다.

✔ **\[FAQ 바로가기]** [외부채널 (트위터/카카오 상담톡) 연결을 활성화했을 때 문의의 인입/답변 과정은 어떻게 되나요?](https://nhn-contact.oc.toast.com/oc/hc/article/61/)
