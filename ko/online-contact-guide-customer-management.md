## Contact Center > Online Contact > 서비스 가이드 > 고객정보관리

## 고객정보연동
### API정보 설정
![](http://static.toastoven.net/prod_contact_center/2.2.7-(1).png)
전화로 문의가 인입되었을 시, 해당 매체번호에 해당하는 고객사 측의 **고객 데이터**를 **API를 통해 조회**하여 Online Contact의 화면에 표시할 수 있도록 제공하는 기능입니다.
**① OPEN API를 활성화**하신 후 이용하실 수 있으며, 입력이 필요한 항목은 다음과 같습니다.

-	**②** OC IP정보 메일 발송: 사용자를 선택한 후 메일 발송 버튼을 누르시면, Online Contact 방화벽 오픈을 위한 IP주소가 메일로 전달됩니다.
-	**③** API 경로
-	**④** API 메서드: GET/POST 중 선택 가능
-	**⑤** 암호화 여부
-	**⑥** 암호화 방식
-	**⑦** 암호화 키: ApiKey 수정 버튼을 누르시면 새로운 API Key가 생성됩니다. 

정보 입력 후 **저장** 버튼을 누르시면 API 정보가 저장되며, 연동을 위해 필요한 API에 대한 가이드는 [API 가이드 → 고객정보 연동](https://docs.toast.com/ko/Contact%20Center/ko/online-contact-api-guide-openapi-customer-data/)에서 확인하실 수 있습니다.

### 고객정보 확인
![](http://static.toastoven.net/prod_contact_center/2.2.7-(2).png)
고객정보연동 API가 활성화되면, 인입경로가 **전화**인 티켓을 클릭했을 시 **① 고객관리** 탭이 표시됩니다.
연동된 API를 통해 조회된 고객 정보는 해당 탭에 표시되며, 전화 문의가 연결되었을 시 자동으로 **① 고객관리** 탭으로 페이지가 이동되어 전화 상담 중에 현재 상담을 진행하고 있는 고객의 고객정보를 참고하실 수 있습니다.  


