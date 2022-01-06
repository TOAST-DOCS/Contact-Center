## Contact Center > Online Contact > Service Guide (Consultation) > Ticket Management

## Ticket
Tickets which were submitted/created by help center · mail · external channel · call · chat (**Consultation Management**), or escalated from consultation management type (**Issue Management**) could be assigned and processed by trigger conditions (can set in Service Management → Ticket → Trigger) or could be manually assigned if unassigned.

![](http://static.toastoven.net/prod_contact_center/4.1.1-(1)_en.png)
From **① All Tickets** Menu, you could check overall current situation of tickets regardless of ticket’s status and assigned agent. And from other **detailed menus**, you could check current situation of tickets displayed by **detailed conditions** such as group, ticket status. The color of each ticket is **given by each inflow channel**, so it could be used to classify tickets. Please refer to the image below for the type of inflow channel represented by each color.

![](http://static.toastoven.net/prod_contact_center/4.1.1-(1)a_2_en.png)
 
Information which you could check by each **detailed menu** is as follows:

-	**②** All Unassigned Tickets: You can view all **unassigned tickets**. 
-	**③** All Tickets in Group: You can view the **entire ticket within the group** you belong to.
-	**④** My Tickets in Progress: Assigned tickets’ status will be changed to **processing**. In this menu, you can view tickets assigned to you.
-	**⑤** My Tickets in Pending: If additional checking is needed when processing, you could set the ticket status to **pending**. In this menu, you can view tickets which you processed as ‘pending’. Pended tickets could be reprocessed to be resolved. 
-	**⑥** My Resolved Tickets: If you process assigned tickets as ‘**resolved**’, the ticket status would be changed to ‘resolved’ and could be viewed at this menu. If the customer resubmits inquiries through the answer mail, it can be processed again.
-	**⑦** My Completed Tickets: Ticket status will be changed to ‘**completed**’ if the administrator processed the ticket to be ‘**completed**’, or if **two weeks past** after the ticket was processed as ‘resolved’. Completed tickets can be viewed in this menu, and ‘completed’ tickets could not be processed again.
-	**⑧** Spam Box: Tickets would be moved to spam box if processed **'Resolve Internally → Spam’. Spam tickets could be restored or deleted, and could not be answered or forwarded before they are restored.

## Ticket Processing
### Keep Tickets
![](http://static.toastoven.net/prod_contact_center/4.1.2-(1)_en.png)
If submitted tickets are **unassigned**, tickets could be distributed through ‘**keep**’ function. Click **① Keep** button, which is displayed in unassigned tickets, and select group if groups which you belong is plural. The ticket would be processed as ‘kept’, and you would be able to process the ticket.

If ticket assigning is set through trigger, tickets would be assigned according to the conditions without using ‘keep’ function. In this case, to replace automatically assigned agents, tickets could be **forwarded** by **administrator**’s authority. Click **② Forward** button, and select group, agent.


### Process Tickets
If submitted (Consultation Management) or escalated (Issue Management) tickets were assigned, ticket status will be changed to ‘**processing**’, and you can handle customer inquiries in that state.

If you click tickets, you could utilize **Ticket Information**, **Ticket History**, **Event** tabs. (If the ticket was created through chat function, you could utilize chat consultation history when processing tickets through displayed **Chat History** tab.)

![](http://static.toastoven.net/prod_contact_center/4.1.2-(2)_en.png)

-	**① Ticket Information**: View information related to customer inquiry 
    - **②** Ticket ID: Automatically created when ticket created
    - **③** Group (the group which the assigned agent belongs to)
    - **④** Agent
    - **⑤** Status
    - **⑥** Channel: Channel which the inquiry was submitted
    - **⑦** Information which the customer entered when submitting inquriy
    - **⑧** Inquiry Contents

![](http://static.toastoven.net/prod_contact_center/4.1.2-(3)_en.png)

-	**① Ticket History**: Check previous inquiry history of the customer

![](http://static.toastoven.net/prod_contact_center/4.1.2-(4)_en.png)

-	**① Event**: Check events occurred related to the ticket (Assign, Change of agent, forward, etc.)

![](http://static.toastoven.net/prod_contact_center/4.1.2-(5)_en.png)
**Processing status** which you can select for each ticket is as follows:

- **①** Resolved: Select to send **final mail** to customer
- **②** Pending: Select to send **intermediate answer mail** before sending final mail
- **③** Add a Comment: Add **memo** to ticket. Used when forwarding ticket to another agent.
- **④** Resolve Internally: Situation when **you don’t need to send final mail** to customer. Detailed components are as follows:
    - Spam
    - Abuse
    - Test
    - Duplicate
    - Resolved via Chat: Mail replying unneeded because inquiry was resolved by chat
    - Resolved via Call: Mail replying unneeded because inquiry was resolved by call
    - Others

  
You could use **Ticket Batching** to make a batch of answers to tickets with similar inquiries, or to change the agent or group of tickets collectively. **⑤ Ticket Batching** button is in the upper side of ticket list.

✔ **\[FAQ]** [How can I use answer templates?](https://nhn-contact.oc.toast.com/oceng/hc/article/122/)
✔ **\[FAQ]** [Can I process tickets with the same inquiry all at once?](https://nhn-contact.oc.toast.com/oceng/hc/article/121/)

### Create Tickets
![](http://static.toastoven.net/prod_contact_center/4.1.2-(6)_en.png)
You could create new tickets through **① Create Ticket** button. This can be used if you need to create additional tickets in the process of handling customer inquiries, or if you need an email response to a telephone inquiry.

The following items are required to enter when creating a ticket:

-	**②** Group
-	**③** Agent
-	**④** Submission Type
-	**⑤** Template
-	**⑥** Title, **⑦** Contents

### Escalate Tickets
Inquiries **difficult to resolve** in **consultation management** service could be **escalated** to **issue management** service created in organization. 

![](http://static.toastoven.net/prod_contact_center/4.1.2-(7)_en.png)
![](http://static.toastoven.net/prod_contact_center/4.1.2-(8)_en.png)

If you click **① Escalation** button, screen which you could select service to escalate would be displayed. Only services which type is issue management will be displayed in the drop box. After **② selecting service**, click **confirm**, and escalation screen would be displayed in the bottom of the ticket. 

If you select submission type, **③ Customer Fields** which were set in Service Management → Ticket → Field menu of issue management service would be displayed according to the selected submission type. Fill in the customer fields, title, contents, and click **④ Escalation** button to process escalation.

After escalated, ticket status will be changed to **⑤ Escalation in Progress**, and if the ticket was processed as **resolved**, **pending**, **resolve internally** in issue management service, the status will be changed into **Escalation resolved**.

## Search Tickets
![](http://static.toastoven.net/prod_contact_center/4.1.3-(1)_en.png)
If you click **① Search Ticket** button in top of the ticket list, search conditions would be displayed. The conditions are specific as follows.

-	**Created Time**: he ticket’s created time
-	**Priority**: Priority which the processor entered when processing the ticket
-	**Ticket ID**: Ticket ID which was automatically created when the ticket was created
-	**Title**: Title which the customer entered when submitting ticket
-	**Group**: Select all or each group
-	**Agent**: Agent which processed the ticket
-	**Status**: Current status of the ticket
-	**Channel**: Channel which the ticket was submitted
-	**Submission Type**: Type which customer selected when submitting ticket
-	**Processing Type**: Type which agent selected when processing ticket
-	**Email (Account)**: Email address of the ticket
-	**Name**: Name of enquirer

