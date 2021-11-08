## Contact Center > Online Contact > API 가이드 > 헬프센터
### 헬프센터 지정 데이터 추가
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com/{serviceId}/hc/openapi/v1/addition.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com/{serviceId}/hc/openapi/v1/addition.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|헬프센터에 지정 데이터 추가|HTTPS  |POST    |UTF-8|JSON    |추가로 필요한 고객정보를 DB에 저장|

#### 요청 파라미터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|서비스 ID	    |serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|추가 고객정보  |content	  |String	|O	|추가 고객정보. request body 형식으로 전송, token 생성 시 인코딩 필요없음|
|노출 여부      |visible    |int    |X  |문의 내용에 노출 여부. 1: 노출, 0: 노출하지 않음. 기본 값: 0|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|----|----|
|result.content	|additionId	|String	|O	|생성된 ID|

#### Response Body
```
{
  "header": {
    "resultCode": 200,
    "resultMessage": "",
    "isSuccessful": true
  },
  "result": {
    "content": "ef1bd9560xxxxx"      // 해당 값은 additionId, 문의 페이지 호출 시 해당 값을 파라미터 - additionId 값으로 지정
  }
}
```
#### 문의 페이지 URL 예시
https://nhn-cs.alpha-oc.toast.com/hangame/hc/ticket/?additionId=ef1bd9560xxxxx

### APP 내 모바일 헬프센터 첨부 권한 체크
App에서 WebView로 헬프센터 호출 시 App 측에서 필요한 작업은 하기와 같습니다.

(1) App에서 Online Contact 헬프센터의 문의하기 페이지 호출 시, URL에 \[from=app] 파라미터 추가하여 호출
(2) Online Contact \[서비스 관리 → 헬프센터 → 구성관리] 메뉴에서 '모바일 첨부 권한' 활성화
(3) Online Contact 문의하기 화면에서 '첨부' 버튼 클릭 시 노출되는 팝업창에서 '카메라, 앨범, 저장소' 버튼 클릭 시 App 측으로 scheme URL 전송

#### Scheme URL
**IOS**
- 카메라 : 「iosapp://clickFile?fn=openFile&param=camera」
- 앨범 : 「iosapp://clickFile?fn=openFile&param=photo」
- 저장소 : 「iosapp://clickFile?fn=openFile&param=file」

**AOS**
- 카메라 : 「aosapp://clickFile:1314?fn=openFile&param=camera」
- 앨범 : 「aosapp://clickFile:1314?fn=openFile&param=photo」
- 저장소 : 「aosapp://clickFile:1314?fn=openFile&param=file」

(4) 접속 권한이 있을 경우 :
Online Contact에서 제공하는 [OPEN API](https://docs.toast.com/ko/Contact%20Center/ko/online-contact-api-guide-openapi-ticket/#_29)를 호출하여 첨부 성공 후, Online Contact 측 callback 함수 (openFile) 호출
```
openFile (0,count,fileNames[],attachmentIds[])
    count - 파일 갯수(int）
    fileNames - 파일 명(array)
    attachmentIds - 파일 ID(array)
```

(5) 접속 권한이 없을 경우 :
Online Contact 측 callback 함수 (openFile) 호출, App 측에서 권한 관련 알럿 메시지 노출 및 권한 설정 안내
```
openFile (1)
```
