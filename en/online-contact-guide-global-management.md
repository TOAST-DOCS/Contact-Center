## Contact Center > Online Contact > Service Guide > Global Management
Global Management menu consists of the ability to add services managed by Online Contact and Organization Administrator, SSO Login, and Authority Log Management menu.

## Contract service status
### Contract status
![](http://static.toastoven.net/prod_contact_center/2.1.1-(1)_en.png)
Through **Contract status** tab, **①** add service to organization using Online Contact, **②** edit basic information/contents of contract, **③** set service usage state, **④** terminate service is available.

Online Contact offers two service types, **Consultation Management**, **Issue Management**.
-	**Consultation Management**: Consultation management service type allows you to talk directly to customers through channels such as chat, phone, and help center provided by Online Contact.
-	**Issue Management**: Issue management service type allows agent of service which type is consultation management to transfer and process inquiries that are difficult to resolve by oneself.

![](http://static.toastoven.net/prod_contact_center/2.1.1-(2)_en.png)
Click **① Add Service** button to view **② add service screen** for entering basic information for the service. The following items require input:
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

## Organization Adminstrator
![](http://static.toastoven.net/prod_contact_center/2.1.2-(1)_en.png)
**Organization Administrator** can manage the organization which uses Online Contact, can add and delete agents, and can add or delete organization administrators from among agents.
Since consulting and service management functions are not available only by the organization administrator's authority, adding administrator or agent authority from [Service Management → Agent](https://docs.toast.com/ko/Contact%20Center/ko/online-contact-guide-service-management/#_25) menu is needed to consult customers, or set service initially.
The user whom you want to grant organization administrator permission must be registered as an IAM member.

### Register as an IAM Member
-	Click **① Invite Members** button → Enter name, ID, email
-	TOAST CONSOLE → Manage Member → IAM Member tab → Click **Register IAM Member** button → Enter ID, name, mail, and mobile phone number
Select one of the above two methods to register IAM member. After registering, click **Add Organization Administrator** button → click **View Agent** button → Search registered IAM Member by entering name/account/email, and add IAM Member as organization administrator.
To newly registered IAM Members, password change mail will be sent by the registered email information. Logging in Online Contact becomes available after setting password through email.

## SSO Login
![](http://static.toastoven.net/prod_contact_center/2.1.3-(1)_en.png)
SSO Login menu allows you to set the authentication method for logging in to help center. After registering SSO Login, set the login method you registered from [Service Management → Authentication](https://docs.toast.com/ko/Contact%20Center/ko/online-contact-guide-service-management/#_2) menu. 

### SSO Login Adding Process
-	Click **① +Register** button → Enter SSO Login Name, Remote Login URL, Login Status URL → Click **Confirm** button
**API Key** is provided for authentication processing when SSO login is set up. The value of API Key can be changed through the **② Change API Key** button.

## Authority Log Management
![](http://static.toastoven.net/prod_contact_center/2.1.4-(1)_en.png)
**①** Logs are recorded when you change the permissions of agents inside the organization. This menu manages logs about change of permission by the organization administrator or administrator. You can **② search** by entering some of the information, including the date and time of operation, operated contents, name, IP, service, or ID.

## Privacy Settings
![](http://static.toastoven.net/prod_contact_center/2.1.5-(1)_en.png)
Through clicking **currently connected ① account name** displayed in the upper right corner of the screen, **② privacy settings** menu is showed. User’s personal settings could be accessed and edited through this menu. 
✔ **\[FAQ Shortcut]** [I want to edit or delete my privacy settings. (ID, Email, Name)](https://nhn-contact.oc.toast.com/oc/hc/article/33/)
✔ **\[FAQ Shortcut]** [I want to change my password.](https://nhn-contact.oc.toast.com/oc/hc/article/35/)

### Accessible Information
-	Account
-	Name
-	Nickname (Editable) : Displayed when communicating through chat, mail
-	Phone number
-	Email
-	Language (Editable) : Language in your environment, apart from service’s language setting
-	Assign ticket(Editable) : If consulting is not available due to vacation, etc., can set ticket allocation status
