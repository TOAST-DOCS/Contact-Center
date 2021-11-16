## Contact Center > Online Contact > Service Guide (Consultation) > Global Management
Global Management menu in Consultation Management service consists of Contract Service Status, Organization Administrator, CTI Management and Authority Log Management menu.

## Contract service status
### Contract status
![](http://static.toastoven.net/prod_contact_center/2.1.1-(1)_en.png)
Through **Contract status** tab, **①** add service to organization using Online Contact, **②** edit basic information/contents of contract, **③** set service usage state, **④** terminate service is available.

![](http://static.toastoven.net/prod_contact_center/2.1.1-(2)_en.png)
Click **① Add Service** button to view **② Add Service screen** for entering basic information for the service. The following items require input:

- Type: Type of service to use (Consultation management, Issue management)
- Service Name: Name of service to be used
- Service ID: ID used to identify the service (becomes included in URL of the service’s Online Contact, and help center). English only
- Time zone: Time zone set in the help center (selected accordingly when help center language becomes selected. Can be modified separately)
- Service Banner: Can attach and preview image. When uploaded, it becomes applied as the image of the service tab in Online Contact GNB and as a profile photo of the agent when chat consulting.

After entering all the basic information, press the next button to go to **③ Contract Details**. On the Contract Details screen, you can **activate functions** from the consultation functions provided by Online Contact for your service and calculate **Estimated Cost** that reflect your choice. After completing the contract details, press **Contract** button to complete the contract.

![](http://static.toastoven.net/prod_contact_center/2.1.1-(3)_en.png)
If you leave without going through all the steps of entering basic information and contract details when adding service, the status of service will be displayed inactivated, and the steps that were not progressed will be indicated by the button **Enrollment**. For services which contract steps are completed, you can edit basic and contract information through the **① Edit** button, activate or inactivate service through **② State** button, and terminate service through **③ Terminate** button. Please note that terminate button becomes active only when the status of the service is **inactivated**.

### Rate status
![](http://static.toastoven.net/prod_contact_center/2.1.1-(4)_en.png)
**Rate status** tab allows you to view monthly charges by type, individual service, and total through **①** Search button. **②** Service status will be displayed together if charges are set to be viewed based on individual services.

✔ **\[FAQ]** [I want to know about the charge criteria.](https://nhn-contact.oc.toast.com/oceng/hc/article/148/)
✔ **\[FAQ]** [When and how will the charge be paid?](https://nhn-contact.oc.toast.com/oceng/hc/article/147/)

### Organization Information
![](http://static.toastoven.net/prod_contact_center/2.1.1-(5)_en.png)
In **Organization Information** tab, **① NHN Cloud Organization Information**, **② OC Organization Information** is available.

#### NHN Cloud Organization Information
In the menu, users can check the information written below, and the same information could be checked and modified in **NHN Cloud Console → Organization Management → Default Organization Setting** tab.

- NHN Cloud Organization Name : The name set when the organization was created.
- NHN Cloud Organization ID : Unique ID given to each organization when the organization was created. Used to create authentication token required when using Open API.
- NHN Cloud Organization Domain : The name set when selecting a service after creating an organization.

#### OC Organization Information
In the menu, users can check the information written below. OC Organization Key could be changed by **Change API Key** button, and OC URL changes together when changing the NHN Cloud Organization Domain. 

- OC Organization Key : Key used in the authentication phase when trying to process actions performed for organizational management through API.
- OC URL : The access URL for Online Contact. Created in the following form : https://**Organization Domain**.oc.toast.com

## Organization Adminstrator
![](http://static.toastoven.net/prod_contact_center/2.1.2-(1)_en.png)
**Organization Administrator** can manage the organization which uses Online Contact, can add and delete agents, and can add or delete organization administrators from among agents.
Since consulting and service management functions are not available only by the organization administrator's authority, adding administrator or agent authority from [Service Management → Agent](https://docs.toast.com/en/Contact%20Center/en/online-contact-guide-service-management/#agent_1) menu is needed to consult customers, or set service initially.
The user whom you want to grant organization administrator permission must be registered as an IAM member.

✔ **\[FAQ]** [Types and difference between permissions](https://nhn-contact.oc.toast.com/oceng/hc/article/119/)

### Register as an IAM Member

-	Click **① Invite Members** button → Enter name, ID, email
-	NHN Cloud CONSOLE → Manage Member → IAM Member tab → Click **Register IAM Member** button → Enter ID, name, mail, and mobile phone number

Select one of the above two methods to register IAM member. After registering, click **② Add Organization Administrator** button → click **View Agent** button → Search registered IAM Member by entering name/account/email, and add IAM Member as organization administrator.
To newly registered IAM Members, password change mail will be sent by the registered email information. Logging in Online Contact becomes available after setting password through email.

## CTI Management
In CTI Management menu, you could set CTI information to connect with Online Contact, and manage CTI ID, CTI NO of each call consultation agent. 
This menu is only viewable in services which **Ticket Management →  Include call(using CTI)** function is **activated** in contract details.  

### CTI Setting
![](http://static.toastoven.net/prod_contact_center/2.1.2-(2)_1_en.png)
From CTI Setting menu, you could set CTI to connect with call consultation function of Online Contact.

The **① Versions of CTI** which is able to choose are as follows:

- IPCC (Private): Private service. Please **consult with us beforehand** from Online Contact help center if use is wanted.([Online Contact Help Center Shortcut](https://nhn-contact.oc.toast.com/oceng/hc/))
- Mobile Contact: Can choose after **Mobile Contact is activated** in NHN Cloud Console.

After choosing the version of CTI, please input **tenant ID, service name** which you received from IPCC or Mobile Contact administrator in the **② Tenant ID, ③ Tenant Name** input box.
If **④ CTI Log Monitoring** function is enabled, CTI log is recorded on a daily basis. The recorded log could be downloaded through **CTI Log Download** function which is accessible by clicking the account name at the top right of the screen.

### CTI Agent Management
![](http://static.toastoven.net/prod_contact_center/2.1.2-(3)_en.png)
You can assign CTI information to agents who will be conducting call consultation among the agents registered with your organization.

If you click **① Search** button without input in the name input box, the list of all agents registered in the organization would be viewed. If you click **① Search** button with input, the list of agents satisfying the search result would be viewed.

Agent ID, name, email address, CTI ID, CTI NO, service (which the agent is registered) of agents are shown in the list, and you could input or edit CTI ID, CTI NO through **② Modify** button.
Please input **CTI ID**, **CTI NO** received from IPCC or Mobile Contact administrator, and then click **③ Save** to save information.

After CTI information is correctly entered and saved, agent with call authority could proceed **CTI Login** in the call widget.

## Authority Log Management
![](http://static.toastoven.net/prod_contact_center/2.1.4-(1)_en.png)
**①** Logs are recorded when you change the permissions of agents inside the organization. This menu manages logs about change of permission by the organization administrator or administrator. You can **② search** by entering some of the information, including the date and time of operation, operated contents, name, IP, service, or ID.

## My Performance
![](http://static.toastoven.net/prod_contact_center/2.1.4-(2)_en.png)
Through clicking **currently connected ① account name** displayed in the upper right corner of the screen, you could access to **② My Performance** menu.
In this menu, detailed **real-time cumulative data** about ticket, call, chat consultation in **currently accessed service** is shown.

Detailed performance classifications for different types of consultations are as follows:

**③ Ticket Achievements**
- New 
- Open 
- Solved
- Closed

**④ Call Achievements**
- IB Call (number of calls/minute)
- OB Call (number of calls/minute)
- Ready
- Transfer
- Ticket Treatment
- Chat Treatment
- Rest
- Eat
- Education
- Report
- Meeting
- Monitor

**⑤ Chat Achievements**
- Ready
- Online
- Rest

## Privacy Settings
![](http://static.toastoven.net/prod_contact_center/2.1.5-(1)_en.png)
Through clicking **currently connected ① account name** displayed in the upper right corner of the screen, **② privacy settings** menu is showed. User’s personal settings could be accessed and edited through this menu. 

✔ **\[FAQ]** [How can I change or delete my ID, email, and name?](https://nhn-contact.oc.toast.com/oceng/hc/article/106/)
✔ **\[FAQ]** [How can I change my password?](https://nhn-contact.oc.toast.com/oceng/hc/article/108/)


### Accessible Information
-	Account
-	Name
-	Nickname (Editable) : Displayed when communicating through chat, mail
-	Phone number
-	Email
-	Language (Editable) : Language in your environment, apart from service’s language setting
-	Assign ticket(Editable) : If consulting is not available due to vacation, etc., can set ticket allocation status
