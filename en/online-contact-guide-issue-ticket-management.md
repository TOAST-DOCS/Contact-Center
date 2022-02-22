## Contact Center > Online Contact > Service Guide (Issue) > Ticket Management

## Ticket
Escalated tickets could be assigned to groups or agents by trigger conditions (Can set in Service Management → Ticket → Trigger menu), or could be manually assigned.
Tickets can be **escalated** from consultation management service, or **created** by the agent of issue management service. 
Colors given to each inflow channel can be used to classify tickets.

## Ticket Processing
![](http://static.toastoven.net/prod_contact_center/4.1.1-(1)_im_en.png)
From **① All Tickets** Menu, you could check the **overall situation of tickets** regardless of status or agent in charge. And from other **detailed menus**, you could check the current situation of tickets categorized by **detailed conditions** such as group or ticket status.

Information which you could check by each **detailed menu** is as follows:

-	**③ All Tickets in Group**: You can view the **entire ticket within the group** you belong to.
-	**④ My Tickets in Progress**: When a ticket is assigned to an agent, the status changes to **processing**. In this menu, you can view tickets assigned to you.
-	**⑤ My Tickets in Pending**: If a ticket needs to be additionally checked, the agent can set the ticket status to **pending**. In this menu, you can view tickets which you processed as ‘pending’.
-	**⑥ My Resolved Tickets**: If an agent process a ticket as ‘**resolved**’, the status of the ticket changes to ‘resolved’ and could be viewed at this menu. If the customer resubmits inquiries to the answer mail, the ticket could be processed again.
-	**⑦ My Completed Tickets**: A ticket becomes ‘**completed**’ if the administrator processes the ticket to be ‘**completed**’, or if **two weeks has been past** after the ticket was resolved. Completed tickets cannot be processed.

### Keep Tickets
![](http://static.toastoven.net/prod_contact_center/4.1.2-(1)_im_en.png)
Agents could assign **unassigned** tickets to oneself through ‘**keep**’ button. Click **① Keep** button, and select agent group if you belong to more than one group. 

If ticket assign is set through trigger, tickets could be assigned according to the trigger conditions. In this case, to change automatically assigned agents, **administrator** of the service could **forward** the ticket to another agent. Click **② Forward** button, and select agent/group.

### Process Tickets
If a escalated/created ticket is assigned, the status of the ticket changes to ‘**processing**’. Customer inquiries could be processed in this state.

You could utilize **Ticket Information**, **Ticket History**, **Event** tabs when processing a ticket.

![](http://static.toastoven.net/prod_contact_center/4.1.2-(2)_im_1_en.png)

-	**① Ticket Information**: Information related to the escalated ticket

![](http://static.toastoven.net/prod_contact_center/4.1.2-(3)_im_en.png)

-	**① Ticket History**: Details of the customer's previous escalated inquiries

![](http://static.toastoven.net/prod_contact_center/4.1.2-(4)_im.png)

-	**① 이벤트**: 해당 문의에 관련하여 발생한 이벤트 (할당, 담당자 변경, 전달 등) 확인

![](http://static.toastoven.net/prod_contact_center/4.1.2-(5)_im.png)
문의에 대해서 선택할 수 있는 **처리 상태**는 다음과 같습니다. **해결**, **보류**, **내부해결** 처리 시 상담 관리 서비스에서의 티켓 상태는 **이관 답변완료**로 변경됩니다.

- **①** 해결: 고객에게 발송할 **최종 메일** 처리 
- **②** 보류: 고객에게 최종 메일 전달 전 **중간답변** 시 선택
- **③** 코멘트 추가: **메모**를 추가하는 것. 타 상담원에게 전달 시 활용됨
- **④** 내부해결: 고객에게 **최종메일을 발송하지 않아도 되는** 상황. 세부 구성 요소는 다음과 같습니다.
    - 채팅해결: 채팅을 통해 문의가 해결되어 메일로 답변을 드리지 않아도 됨
    - 전화해결: 전화를 통해 문의가 해결되어 메일로 답변을 드리지 않아도 됨
    - 기타
  
문의 내용이 유사한 티켓들에 대해 답변을 일괄적으로 작성하고자 하거나, 티켓들의 처리자 또는 그룹을 일괄적으로 변경하고자 할 때 **티켓 일괄 처리** 기능을 사용할 수 있습니다. **⑤ 티켓 일괄 처리** 버튼은 티켓 리스트 상단에 위치해 있습니다.

✔ **\[FAQ 바로가기]** [답변 템플릿은 어떻게 사용하나요?](https://nhn-contact.oc.toast.com/oc/hc/article/39/)
✔ **\[FAQ 바로가기]** [동일한 문의 내용을 한번에 일괄처리 할 수 있나요?](https://nhn-contact.oc.toast.com/oc/hc/article/38/)

### 티켓 생성
![](http://static.toastoven.net/prod_contact_center/4.1.2-(6)_im.png)
**① 티켓 생성** 버튼을 통해 새로운 티켓을 생성할 수 있습니다. 고객 문의 처리 과정에서 추가 티켓을 생성할 필요가 있거나, 전화 문의에 대한 메일 답변이 필요한 경우 사용될 수 있습니다.

티켓 생성 시 입력이 필요한 항목은 다음과 같습니다.
-	**②** 담당그룹
-	**③** 담당자
-	**④** 접수유형
-	**⑤** 제목, **⑥** 내용

### 개인정보 마스킹
서비스의 계약 정보에서 **보안 서비스** 기능이 **사용** 설정된 경우, 티켓 관리 화면에 **개인정보 마스킹** 버튼이 표시되어 상담 진행 시 전달되는 고객의 개인정보를 암호화하여 관리하실 수 있습니다.  

![](http://static.toastoven.net/prod_contact_center/masking_1.gif)
티켓 관리 시 개인정보 마스킹을 진행하실 수 있는 영역은 **고객 문의**, **상담원 답변** 영역입니다. 마스킹하고자 하시는 영역을 **드래그**하여 선택하신 후 **개인정보 마스킹** 버튼을 누르시면 화면 상의 개인정보가 별표(\*)로 치환되어 표시되며, 마스킹 처리된 데이터는 데이터베이스 상에도 마스킹된 상태로 저장되어 보관됩니다.

![](http://static.toastoven.net/prod_contact_center/masking_2.gif)
개인정보 마스킹을 **해제**하고자 하실 경우, **별표(\*)로 치환된 영역을 클릭**하시면 마스킹 해제 여부를 묻는 팝업 화면이 표시되며, **확인** 버튼을 누르시면 화면과 데이터베이스에서 개인정보 마스킹이 해제됩니다. 

## 티켓 검색
![](http://static.toastoven.net/prod_contact_center/4.1.3-(1)_1_im.png)
티켓 목록 상단에 위치한 **① 티켓검색** 버튼을 누르시면 티켓 검색에 활용할 수 있는 조건들이 표시됩니다. 조건들은 구체적으로 다음과 같습니다.

- 생성시간
- 우선순위
- 티켓ID
- 제목
- 담당그룹
- 담당자
- 티켓상태
- 채널
- 접수유형
- 처리유형
- 이름
- 아이디
- 이메일
- 전화번호

