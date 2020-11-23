## Contact Center > Online Contact > API 가이드 > 고객정보 연동

**전화 문의**가 인입되었을 때 해당 매체번호에 해당하는 **고객사 측 고객 데이터를 API를 통해 조회**해서 가져올 수 있도록 제공하는 기능입니다.

Request URL: 고객사의 API URL
Response Type: JSON

### 요청 파라미터
|번호|변수|필수|데이터 타입|설명|
|----|----|----|---------|----|
|1   |telNo|O  |String   |인입된 콜의 매체번호|

### 결과 데이터
|번호|변수|데이터 타입|설명|
|----|---|-----------|---|
|1   |resultCode|String|성공:0, 실패:other|
|2   |resultMsg |String|결과 메시지|
|3   |resultData|Map   |결과 맵|

### resultData 파라미터
|번호|변수|데이터 타입|설명|
|----|----|----------|---|
|1  |custId|String   |   |
|2  |custName|String |   |
|...|...     |...    |...|

### Response Body
```
{
   "resultData":{
      "custId": "test",
      "custName": "테스트",
      ..
      ..
   },
   "resultCode": "0",
   "resultMsg": "success"
}
```

resultData 변수 내의 데이터는 고객사 측에서 원하시는 대로 설정하실 수 있으며, **API를 통해 리턴하시는 모든 데이터가 화면에 표시**됩니다.
만약 resultData 내의 변수가 Online Contact 티켓 필드로 추가되어 있다면, 해당 변수의 **변수명**과 [필드의 **항목 코드 값**](https://docs.toast.com/ko/Contact%20Center/ko/online-contact-guide-service-management/#_22)이 **일치**해야 알맞게 매핑될 수 있습니다.
