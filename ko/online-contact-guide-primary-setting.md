## Contact Center > Online Contact > 서비스 가이드 > 서비스 가입 및 기본 설정

## 회원 가입
### NHN Cloud 회원가입
![서비스가입_회원가입](https://static.toastoven.net/prod_contact_center/OC3.0/kr/online-contact-guide-primary-setting_img0010.png)

Online Contact는 NHN Cloud 회원가입 후 이용할 수 있습니다.

NHN Cloud 홈페이지 우측 상단의 **회원가입** 버튼을 클릭하여 회원 가입을 진행할 수 있으며, 사업자 회원의 경우 **사업자등록증**을 첨부해야 하므로 미리 준비해주십시오.

### 결제수단 등록
![서비스가입_결제수단등록](https://static.toastoven.net/prod_contact_center/OC3.0/kr/online-contact-guide-primary-setting_img0020.png)

NHN Cloud 서비스를 이용하기 위해서는 결제수단을 반드시 등록해야 합니다.

- 회원가입을 완료하면 로그인 시 **마이페이지 → 결제수단** 화면으로 이동됩니다.
- 페이지를 벗어났다면 **① 우측 상단 이메일 계정 클릭** → **② 결제수단**으로 접근할 수 있습니다.
- 해당 화면에서 **③ 결제 수단 추가** 버튼을 클릭하여 요금을 결제할 카드를 등록합니다.
- 결제 수단은 PAYCO에 등록된 신용카드 또는 소지중인 신용카드를 등록할 수 있으며 체크카드는 등록이 불가합니다.

## 조직 생성 및 서비스 선택

### 콘솔 실행
![서비스가입_콘솔실행](https://static.toastoven.net/prod_contact_center/OC3.0/kr/online-contact-guide-primary-setting_img0030.png)

결제수단 등록 후 NHN Cloud 홈페이지 상단 **CONSOLE** 버튼을 클릭하여 NHN Cloud CONSOLE로 이동합니다.

### 조직 생성
![서비스가입_조직생성](https://static.toastoven.net/prod_contact_center/OC3.0/kr/online-contact-guide-primary-setting_img0040.png)

NHN CLOUD의 서비스 사용을 위해서는 조직을 먼저 생성해야합니다.
기존 생성된 조직이 있을 경우 Online Contact을 사용할 조직을 선택한 후 다음 단계로 이동하십시오.

- 조직을 생성하려면 좌측 상단의 **조직을 생성해 주세요.** 영역을 클릭합니다.
- **조직 생성 대화상자**가 실행되며, 생성할 조직의 이름을 입력합니다.
- **확인** 버튼을 클릭하면 조직이 생성됩니다.

<!-- 여기까지-->

### 서비스 선택
![](http://static.toastoven.net/prod_contact_center/1.3.2-(3).png)

**①** Contact Center 분류 아래의 **Online Contact**를 클릭해주세요. 바로 조직/도메인 이름 설정 단계로 넘어갑니다.

### 조직/도메인 이름 설정
![](http://static.toastoven.net/prod_contact_center/1.3.2-(4).png)
**①** 조직 이름: 기존 조직 이름을 사용하거나 의미 있는 조직 이름으로 수정 또는 추가해주세요.
**②** 도메인: 영문, 숫자, 하이픈 사용(첫 글자 영문, 숫자만 가능/3~40자 이내)

`https://example.OC.toast.com/` 의 형식으로 도메인이 생성되며, 도메인은 Online Contact을 접속하는 **URL 주소**로 사용됩니다.
조직, 도메인 모두 중복 이름이 존재할 경우 사용이 불가하므로 수정해주세요. 작성 완료 후 우측 **저장** 버튼을 눌러주세요.

## IAM 회원
![](http://static.toastoven.net/prod_contact_center/1.3.3-(1).png)
**①** 조직 이름과 도메인 이름을 설정한 이후 IAM 회원을 등록합니다. **IAM 회원 등록** 버튼을 누르시면 회원 정보를 입력하실 수 있는 창이 표시됩니다.
Online Contact의 회원 구분은 두 가지입니다.

- NHN Cloud 회원: NHN Cloud 사이트에 가입되어 있는 회원으로 **조직을 관리하는 멤버**입니다.
- IAM 회원: 조직 내부 회원으로 **조직 내에서만 유효한 멤버입**니다. NHN Cloud 인증을 하지 않은 아이디로 생성되며, NHN Cloud CONSOLE 내부 멤버 관리 → IAM 회원 탭에서 추가 등록 가능합니다.

### IAM 회원 등록
![](http://static.toastoven.net/prod_contact_center/1.3.3-(2).png)
**①** ID와 이름, 메일주소를 입력하신 후 등록하실 수 있으며, 여러 명의 멤버를 등록하실 수 있습니다. 등록하신 후 OWNER 계정으로 사용하실 IAM 회원을 **OWNER로 체크**해주세요.

## 가입 완료 후 최초 접속
![](http://static.toastoven.net/prod_contact_center/1.3.4-(1).png)
Online Contact 서비스 가입이 완료되었습니다. 표시되는 가입완료 페이지에서
**① Online Contact 접속 URL**과, IAM 회원 중 **OWNER로 설정한 ID**를 확인해주세요. 추후 해당 정보를 사용해서 접속하실 수 있습니다.
**②** 로그인 보안 설정의 경우 [로그인 보안 설정 가이드](https://docs.nhncloud.com/ko/TOAST/ko/console-guide/#iam)를 참고해주세요.

가입완료 페이지에서 확인하신 URL에 접속하시거나, 또는 NHN Cloud CONSOLE 페이지 내부 조직 서비스 이용 현황 → Online Contact를 눌러서 접속하시면 로그인 페이지가 표시됩니다. 
마찬가지로 가입완료 페이지에서 확인하신 OWNER ID로 로그인해주세요. ID에 비밀번호가 설정되어 있지 않은 상태이므로 **비밀번호 찾기**를 먼저 진행해주신 후 로그인이 가능합니다.

### OWNER ID로 로그인
![](http://static.toastoven.net/prod_contact_center/1.3.4-(2).png)
**①** 비밀번호 찾기 시 인증 메일은 IAM 회원 등록 시 기재하신 이메일 계정으로 전송됩니다. 해당 메일을 통해 비밀번호를 새롭게 설정해주세요.
비밀번호는 영문, 숫자, 특수문자 조합의 8~15자리로 구성해주세요.

✔ **\[FAQ 바로가기]** [비밀번호를 변경하고 싶습니다.](https://nhn-contact.oc.toast.com/oc/hc/article/35/)
