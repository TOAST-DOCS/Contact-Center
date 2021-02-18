## Contact Center > Online Contact > Service Guide > Service Management

Service Management menu includes **detailed setting functions for accepting and processing inquiries** including SSO login settings, ticket settings, agent management, and help center template management.

You can check the detailed functions or configuration of the help center you set up at the help center for each service which is accessible in the following path.


### Help Center Access
-	**Help Center Link** in the bottom right of Online Contact web page
-	https:// **Domain Name**.oc.toast.com/ **Service ID** /hc

Domain name is the information which was created when you added your organization. Modifying is available in NHN Cloud Console → Set Organization → Set Domain. Service ID is the information which was entered when adding service from [Global Management → Contract Service Status](https://docs.toast.com/en/Contact%20Center/en/online-contact-guide-global-management/#contract-service-status) menu, and it cannot be modified after initial creation.

## Authentication
You can enable or disable **SSO Login** and **Open API** features which you registered in [Global Management → SSO Login](https://docs.toast.com/en/Contact%20Center/en/online-contact-guide-global-management/#sso-login) menu.

### SSO Login
![](http://static.toastoven.net/prod_contact_center/2.2.1-(1)_en.png)
If you want to enable SSO Login, click **Enable** and select, save the login method which you registered from [Global Management → SSO Login](https://docs.toast.com/en/Contact%20Center/en/online-contact-guide-global-management/#sso-login) menu. Once SSO login is activated, **Inquiry History** icon will be displayed on the main page of the service’s Help Center so that the customer can view their previous inquiries after logging in.

### Open API
![](http://static.toastoven.net/prod_contact_center/2.2.1-(2)_en.png)
In the Open API tab, **① OPEN API Activation** which allows access to data inside of Online Contact from outside, **② Change API Key**, managing **③ Accessible IP List** is available. Through Accessible IP List, Open API can be called only from the IP which is registered in the list. 

## Chat
Functions in this menu are related to chat consultation. Chat consultation could be enabled in [Service Management → Help Center → Default Settings](https://docs.toast.com/en/Contact%20Center/en/online-contact-guide-service-management/#default-settings_1), and could be accessed through **chat icon** which is displayed in the bottom right side after chat consultation is enabled.

![](http://static.toastoven.net/prod_contact_center/2.2.2-(1)_en.png)
After accessing through **chat icon**, click **status value** in the top left of the chat screen to set your status. (initially set to ‘offline’, can choose between online/break/offline). Responding to customer's chat request is only available when chat status is set to online.

### Default Settings
![](http://static.toastoven.net/prod_contact_center/2.2.2-(2)_en.png)
You can set **Greeting Message** which is sent automatically when chat consultation is connected, and **Satisfaction Guide Message** which is sent when requesting evaluation about the consultation to customer. Evaluation request could be sent through **Evaluation** button in the top of the chat screen.

### Agent Assignment Settings
![](http://static.toastoven.net/prod_contact_center/2.2.2-(3)_en.png)
**①** Could choose whether to **assign chat priority** to a counselor who has recent chat history with a customer who requested chat consultation, or to distribute **randomly**.

### Chat Screen Insertion Code
![](http://static.toastoven.net/prod_contact_center/2.2.2-(4)_en.png)
This code is provided if you want to provide Online Contact's chat service only on the service page you previously managed. **①** Please copy the script provided and insert it in front of the </body> tag of your website HTML source code.

### Manage Category
![](http://static.toastoven.net/prod_contact_center/2.2.2-(5)_en.png)
This menu allows you to manage the category of **Processing Type** among the consultation information which the agent inputs directly about the customer during chat consulting. You can set processing types 1 through 3 depth.

**①** When adding category in the lower depth after adding the upper category, click the upper category first, and then add the subcategory after checking whether the right category has been selected. Under the color-highlighted category, a new subcategory would be added.

Category name **duplicate is not possible** within the same depth. (Possible if the depth is different)


## Ticket
From the Ticket menu, you can manage category which you select to receive or process inquiries, use trigger features that can improve your business efficiency, configure the Help Center Inquiry field, Manage Templates, and Set up Email.

### Manage Category
![](http://static.toastoven.net/prod_contact_center/2.2.3-(1)_en.png)
Depending on the type of service, categories of ticket are used as follows.

#### Consultation Management
-	Submission Type: Selected by customer when making inquiries
-	Processing Type: Selected by agent when processing tickets

#### Issue Management
-	Submission Type: Selected by agents of Consultation Management service when escalating tickets
-	Processing Type: Selected by agents of Issue Management service when processing escalated tickets

**①** When adding category in the lower depth after adding the upper category, click the upper category first, and then add the subcategory after checking whether the right category has been selected. Under the color-highlighted category, a new subcategory would be added.

Category name **duplicate is not possible** within the same depth. (Possible if the depth is different)
In case of **Processing Type** categories, add **processing type** field (created by default) through Service Management → Ticket → Field → Agent Field → Add button to view processing type categories you set when ticket processing.

**② Copy** button in the top right allows you to copy the **Category ID** automatically assigned to each category, and **③ Download** button allows you to extract the entire category information into an **Excel file**. The following information is extracted:

#### Information extracted by Download button
-	Category ID
-	Category name
-	Depth 
-	Upper category ID
-	Modified Time
-	Created Time

### Trigger
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2)_en.png)
Triggers are designed to increase task productivity by **automating** repetitive tasks. By using triggers, resulting behaviors are automatically executed when certain conditions are met. You can also set up notification mails to be sent for results.

Example) If `Submission Type` of the ticket = `Billing`, `Assign` ticket to `test01` agent of `Billing` group `necessarily`

Click the **① Add Trigger** button, enter all the title, conditions, and results, and click the **Save** button to save and activate the trigger. Enabled triggers can be disabled via the **② Disable** button, and conditions or results can be modified via the **③ Edit** button.

#### Trigger Condition Types
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2)a_en.png)

#### Trigger Condition Details
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2)b_en.png)

#### Trigger Condition Details
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2)c_en.png)

#### Trigger Result Details
##### Ticket : Assign
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2)d_en.png)
If you select and save the agent group and the ticket distribution method within the group (random allocation, linear allocation, select agent), the assignment will be executed according to the results you selected when the trigger conditions are met. **Random allocation** means that the group’s agents are assigned tickets at **random**, and **linear Allocation** means the ticket would be assigned in the order in which agents are **added to the group.** If you have multiple triggers that specify results with different agents under the same conditions, all triggers, not randomly assigned to one of these agents, will be triggered sequentially, and tickets will continue to be assigned only to the person set for the last trigger, so if you intend to randomly assign tickets within the group, make sure to select ** random allocation**. 

##### Notification
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2)e_en.png)
Notification is the type of result that **notification mail is sent** to the specified recipient when the trigger condition is met. If you select this result type, you can set the subject and content of the notification mail to be sent via the **① Notification Settings** button.

##### Forward
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2)f_en.png)
Forward is the type of result that **ticket information being emailed** to the specified recipient when the trigger condition is met. You can check the information and inquiries of the ticket through the e-mail. If you click the **① Online Contact Shortcut** link at the bottom of the inquiry, **ticket screen would be popped-up**, and you can process the ticket directly on the screen. If you chose to **complete the ticket after forwarding**, the inquiry will be emailed and your ticket will be automatically processed as**completed**.

##### Callback url
Callback url is the type of result that the **entered callback address is called** when the trigger condition is met.

##### Dooray Notification
![](http://static.toastoven.net/prod_contact_center/2.2.3-(2)g_en.png)
If the trigger conditions are met, information of the ticket is sent via Dooray notification based on the template set by the **① Template Settings** button. For the link URL, see [Dooray Messenger Service Guide](https://docs.toast.com/en/Dooray/Messenger/en/service-guide/#receive-web-hookproject-notification) for instructions.

### Field
![](http://static.toastoven.net/prod_contact_center/2.2.3-(3)_en.png)
Fields are divided into **① Customer Field** and **① Agent Field**. Please select whether you want to manage before selecting field setting or field management.

Depending on the type of service, customer and agent fields are used as follows:

#### Consultation Management
-	Agent Field: fields that the agent enters directly about the ticket when processing ticket
-	Customer Field: fields shown to the customer in Help Center → Inquiry screen. Implemented on Help Center Inquiry screen as set in field setting menu.

#### Issue Management
-	Agent Field: fields entered directly by the agent of the Issue Management Type service for the ticket when processing the escalated ticket
-	Customer Field: fields entered and forwarded according to the specified category when a ticket is escalated

#### Field Setting
![](http://static.toastoven.net/prod_contact_center/2.2.3-(4)_en.png)
**①** Depending on the submission type you added earlier in [Service Management → Ticket → Manage Category](https://docs.toast.com/en/Contact%20Center/en/online-contact-guide-service-management/#manage-category_1), you can set the fields required for inquiry details differently. Click **Submission Type** to view the fields you have set up, and you can change the **②** order of fields except for personal information field. In the case of personal information field, it is always pinned to the bottom.

You can also **③ add** and **④ remove** the fields you previously added on the Field Management menu.

#### Field Management
![](http://static.toastoven.net/prod_contact_center/2.2.3-(5)_en.png)
Manage individual fields on the Field Management menu so that you can add fields for each submission type in Field Settings menu. Default fields can only be modified or initialized instead of deletion, and both modification and deletion is available for the fields you created.

![](http://static.toastoven.net/prod_contact_center/2.2.3-(6)_en.png)
For adding customer fields, items required to be filled are as follows:

-	**①** Field type: The **type of field**. If you select the field type, **Detailed Settings** and **Preview** will be displayed at the bottom of Basic Settings. Detailed settings allow you to set the values to be displayed for the field, and you can use preview to see what the field will look like on the customer's screen. 
-	**②** Field code: When developing inquiry feature with Open API, field code is used as a unique value to represent the field.
-	**③** Field Name: The name of the field, which appears with the field on the Inquiry screen.
-	**④** Notice: A guide phrase for the field, which appears with the field on the Inquiry screen.
-	**⑤** Required: When set, it is marked with a \*(star) to the right of the field name and must be filled before you move on to the next field. Among the default fields, type, email, title, contents, personal information must be set to ‘required’.
-	**⑥** Personal information (Encrypt or not)
-	**⑦** Destroy personal information

For agent fields, **Permission** (Administrator, Agent) item is additionally required to be filled.

### Manage Template
![](http://static.toastoven.net/prod_contact_center/2.2.3-(7)_en.png)
Template managing is a feature that allows you to quickly process tickets by **pre-adding answer templates** for frequently asked questions. You can choose templates when you process tickets in the Ticket Management menu, and it is only selectable when the submission type of the template is same as the submission type of the ticket.

**① Add Template** button allows you to add a template. The submission type you need to select is which you previously added in [Service Management → Ticket → Manage Category]( https://docs.toast.com/en/Contact%20Center/en/online-contact-guide-service-management/#manage-category_1). You can insert links, images, and tables when you right-click on the body of the content.

### Email Settings
![](http://static.toastoven.net/prod_contact_center/2.2.3-(8)_en.png)
You can create a **① representative account address** which domain is provided from Online Contact, or register a service representative account using one’s service domain by enrolling **② External account **.

**③** You can save the **sender's name** and **address** of the email sent through Online Contact and can set common **Mail Layout** for every sent mail. If you delete the replacement code (#{content}) of the body, the contents in the answer mail may not be displayed, so please be aware to not delete the replacement code when creating layout. Also note that this is a common layout which applies to all outgoing mail, including the templates you created earlier in Ticket → Manage Template menu, so make sure there are no conflicts between layout and templates.

## Call
In Call menu, you could register **IVR Route Code, Name** for managing callback, and register **Calling Number** which is displayed to the customer when making a outbound call. This menu is only viewable in services which **Ticket Management →  Include call(using CTI)** function is **activated** in contract details. 

When call function is activated, to call authorized agents **call widget** will be shown, which allows agents to access call consultation related features.

### IVR Route Management
![](http://static.toastoven.net/prod_contact_center/2.2.3-(8)-1_en.png)
In IVR Route Management menu, you could manage **IVR Route Code**, **IVR Route Name** for managing callback.

By clicking **① Add** button, screen for adding IVR route will be shown. Please input IVR route code and route name received by CTI administrator, and save the IVR information. If callback request is received through the added IVR route, you could **check the IVR route for the received callback request** in Additional Business Management → Callback Management → Callback List menu (To view this menu, additional work → callback function should be activated in contract details).

You could **② modify, delete** added IVR routes.

### Send No Management
![](http://static.toastoven.net/prod_contact_center/2.2.3-(9)_en.png)
In this menu, you could manage **calling number** which is displayed to the customer when making a outbound call.
It can be used by agents within an organization who conduct call consultations about multiple services when trying outbound calls by selecting the calling number appropriately for the purpose of the outbound call.

By clicking **① Add** button, screen for adding calling number would be shown. After entering name, number, and attaching certificate of use of communication service, click save, and the added calling number would be added to the calling number list as **New** status. **② Modifying** is only able when the status is **new**, and **③ deleting** is able regardless of the current status.

Once the verification with the certificate of use of communication service for the added calling number is completed, the status will be changed to **Confirm** or **Reject**. You can check the reason for the change of status.

**Confirmed** calling numbers are viewed in the calling number dropbox when the agent with the call authority of the service clicks **Dial Up** in the call widget.

### Call Consultation
When call function is activated, **call icon** is displayed to the call authorized agent. CTI screen will be displayed in the upper right side of Online Contact if call icon is clicked.

#### CTI Login, Base Status
![](http://static.toastoven.net/prod_contact_center/2.2.3-(10)_en.png)
Agent which CTI information is registered in Global Management → CTI Management → CTI Agent Management menu could login to the CTI through **① Login** button. After login is completed, the CTI screen is changed to **② default screen**, and the following functions are able to use.

- Logout
- Rest : Set agent status to rest, call request not allocated in this status.
- Ready : Set Agent status to ready, call request allocated when inbound call exists.
- Business : Can choose between Education, Report, Meeting, Ticket, Chat, Monitor. Call request not allocated in this status.
- Dial up: Can make outbound call after setting customer number, calling number. (Can set in Service Management → Call → Send No Management menu)

#### Inbound Call
![](http://static.toastoven.net/prod_contact_center/2.2.3-(11)_en.png)
If call is requested when agent status is set to ready, **① alert about inbound call** which notifies if call consultation is connected, current screen will be changed to the ticket processing screen of the service which call is requested is displayed.

Call would be connected by clicking **② Confirm** button, and ticket would be automatically created to the service which call is requested. When cancel button is clicked, the call goes back to the scenario to navigate agents in ready status, and if the agent status is changed to 'ready' again, the agent would be able to receive call again.

#### Outbound Call
![](http://static.toastoven.net/prod_contact_center/2.2.3-(12)_en.png)
When clicking **① Dial up** button in the CTI screen, screen for **② dial up** will be displayed.
After entering **customer number**, and selecting **sending number**, click **③ confirm** to make outbound call.
When calling is proceeded, the agent status would be changed to **Dialing**, and when call is connected, ticket would be automatically created to the service which call is made.

#### Process Call
![](http://static.toastoven.net/prod_contact_center/2.2.3-(13)_en.png)
In **Talking** status, you can use the following functions through the CTI screen.
- Transfer : You can **transfer** the currently connected call to other agent. After entering agent number or searching agent, you can discuss with the other agent through **transfer try** button, and can transfer the call through **transfer connect** button. 
- Disconnect: In the case of a situation where **normal consultation is difficult to take place due to the customer's strong attitude**, click disconnect to finish call with an ARS announcement.
- Hold: If you need a moment of confirmation or inquiry while consulting, select Hold. **Music will be transmissed** to the customer, and agent status will be changed to **holding**. Click **retrieve** to reconnect call.
- Hang up: Call will be finished.

#### Finish Call
![](http://static.toastoven.net/prod_contact_center/2.2.3-(14)_en.png)
When call is finished, **alert about change of agent status** will be displayed, and if **① Confirm** button is clicked, agent status will be changed to **ready**.

If **② Cancel** is selected, status will be changed to **Ticket**, and you could process ticket created for the proceeded call consultation. For call tickets, you could process through selecting the following items: **Resolved**, **Pending**, **Add a Comment**.

## Agent
In this menu, you can add and edit agents and groups for handling customer inquiries (ticket, chat, call consultations), and set up groups and permissions for each agent.

### Agent
![](http://static.toastoven.net/prod_contact_center/2.2.4-(1)_en.png)
User must be registered as **IAM Member** to be added as an agent.

#### Register IAM Member
-	Click ① Invite Members button → Enter name, ID, email
-	NHN Cloud CONSOLE → Manage Member → IAM Member tab → Click Register IAM Member button → Enter ID, name, mail, and mobile phone number 

Select one of the above two methods to register IAM member., and click **② Add Agent** → **View Agent** → search registered IAM Member by entering name/account/email, and add the IAM Member as your service’s agent.

Group assigning is mandatory when adding a counselor, so please add **group** first and proceed with adding a counselor.

The **permissions** you can set when adding an agent is as follows, and settings about organization administrator are available from [Global Management → Organization Administrator](https://docs.toast.com/en/Contact%20Center/en/online-contact-guide-global-management/#organization-adminstrator) menu.

-	Administrator: Permission which features related to **service settings** added to the permission of **agents**. (Ticket, chat permissions can be selected individually. When call is selected, ticket becomes automatically selected together.)
-	Agent: Permission for **ticket, call, chat consultation**. (Ticket, chat permissions can be selected individually. When call is selected, ticket becomes automatically selected together.)

### Group
![](http://static.toastoven.net/prod_contact_center/2.2.4-(2)_en.png)
In Group menu, you can **① add**, **② edit**, **③ delete** groups. When configuring agents into groups, you can assign type-specific inquiries to the appropriate group, or set up notification mail to be sent by Ticket → Trigger.

#### Add Group
![](http://static.toastoven.net/prod_contact_center/2.2.4-(3)_en.png)
Click **Add Group**, enter group name, choose agent to be assigned, and click **①** ‘**>** ‘button to move agent to ‘Assigned Agent’. Conversely, when you unassign a agent, click ‘**<**’ button to move agent to ‘Unassigned Agent’. After assigning agents, press **② Save** button to apply group settings. 

You can add a group without assigning agents, so when you add a group initially, you can proceed adding agents by simply entering the group name and pressing the **Save** button.

## Help Center
### Template Management
![](http://static.toastoven.net/prod_contact_center/2.2.5-(1)_en.png)
In this menu, you can **manage design themes** for your Help Center. Using the provided editor, you can modify the design for each service-specific detail area.

There are two basic templates available, and you can add new templates with the **① Add Template** button. The template you added can be **② edited** or **deleted**. The template in use cannot be deleted, so please enable another template to delete it.

![](http://static.toastoven.net/prod_contact_center/2.2.5-(2)_en.png)
When adding or editing templates, you can directly input **① CSS / HTML / JS scripts**, or upload appropriate file (script, font, image, etc.) and enter the path of the resource in the editor to change the configuration of the Help Center. Through **Preview** button you could see the edits being applied, and after **saving**, you could apply the template.  

**When modifying CSS**, the key elements you can refer are as follows:

##### main.css
| Element Name                                        | Details                                |
| --------------------------------------------------- | ---------------------------------- |
| .main_banner                                    | Upper banner area / main page                  |
| .main_banner img                                | Image of upper banner area / main page           |
| .carousel-caption .title_txt                    | Title of upper banner area / main page             |
| .carousel-caption .sub_txt                      | Subtitle of upper banner area / main page           |
| .search-box                                     | Search box of upper banner area / main page         |
| .search-box .icon-ic-search                     | Search icon of upper banner area / main page       |
| #supports .container-con                        | Contents area / main page          |
| #supports .support__item:nth-child(1):before    | Notice icon / main page                 |
| #supports .support__item:nth-child(2):before    | FAQ icon / main page                     |
| #supports .support__item:nth-child(3):before    | Inquiry icon / main page                 |
| #supports .support__item:nth-child(4):before    | Inquiry History icon / main page                 |
| #supports .support__item .card-title .btn       | Title of contents area / main page                   |
| #supports .support__item .card-title .btn:hover | Title of contents area / main page (Color changed when hovered)    |
| #supports .support__item .card-title .btn:after | Right arrow icon of contents area / main page |
| #supports .support__item .card-text             | Information text of contents area / main page |
| #sec_contact-news .textArea                     | Bottom banner area / main page |
| #sec_contact-news .textArea .text-item h3       | Title of bottom banner area / main page |
| #sec_contact-news .textArea .text-item .icon-more::after | See more icon of bottom banner area / main page |
| #sec_contact-news .textArea .text-item li       | Document list of bottom banner area / main page |
| #chat-offline                                   | Agent offline box |
| #chat-offline .title                            | Title of agent offline box |
| #chat-offline .text                             | Text of agent offline box |
| #chat-offline .close                            | Close icon of agent offline box |
| #chat-offline .btn                              | Contact us icon of agent offline box |

##### faq.css
| Element Name                          | Information                                |
| ---------------------------------- | ---------------------------------- |
| .lnb--fixed .lnb--fixed__nav       | Left LNB / details page                |
| .help-center-title                 | Title of left LNB / details page            |
| .lnb__nav                          | List of left LNB / details page          |
| .lnb__nav li a                     | Item of list of left LNB / details page     |
| .lnb__nav li.on a                  | Selected item of list of left LNB / details page     |
| .lnb--fixed__side-divider          | Dividing line of left LNB and contents     |
| .lnb--fixed__content               | Contents area / details page              |
| .tit_txt                           | Title of contents area / details page         |
| .data_info-box                     | Box of contents area / details page         |
| .tab_category                      | Category tab of contents area / details page   |
| .tab_category>li.on                | Selected category of contents area / details page |
| .tab_category>li                   | Category of contents area / details page |
| .tbl_wrap                          | List of contents area / details page        |
| .faqData th:nth-child(1)           | Category of FAQ table                  |
| .faqData th:nth-child(2)           | Title of FAQ table                     |
| .faqData th:nth-child(3)           | Registered date of FAQ table                    |
| .faqData tr.hot-text td            | Category of main-fixed document of FAQ table     |
| .faqData tr.hot-text td .title-info a | Title of main-fixed document of FAQ table     |
| .faqData td .title-info sup        | HOT icon of main-fixed document of FAQ table         |
| .gocont .search                    | FAQ search                           |
| .sel                               | Category in FAQ search                  |
| .search .inp                       | Search input in FAQ search                   |
| .search .btnArea                   | Search button in FAQ search                    |
| .faqData_info-con                  | Contents of FAQ document                |
| .faqData_info-con .dataTit         | Title of FAQ document              |
| .faqData_info-con .dataTime        | Registered date of FAQ document              |
| .faqData_info-con .dataTextBox     | Text of contents of FAQ document           |

##### notice.css
| Element Name                         | Details                                |
| ---------------------------------- | ---------------------------------- |
| .el-breadcrumb                     | Right-upper text area / details page   |
| .el-breadcrumb li                  | Item of right-upper text area / details page|
| .noticeData                        | Notice table                   |
| .noticeData th:nth-child(1)        | Number of notice table                |
| .noticeData th:nth-child(2)        | Title of notice table             |
| .noticeData th:nth-child(3)        | Heading of notice table               |
| .noticeData th:nth-child(4)        | Registered date of notice table               |
| .noticeData tr.hot-text            | Main-fixed document of notice table      |
| .noticeData tr.hot-text td         | Number of main-fixed document of notice table |
| .noticeData tr.hot-text td .title-info a | Title of main-fixed document of notice table |
| .noticeData td .title-info sup     | HOT icon of main-fixed document of notice table    |
| .icon-leavel-1                     | Heading of main-fixed document of notice table   |
| .noticeData tr                     | Item of notice table               |
| .noticeData td .title-info a       | Title of item of notice table             |
| .upload-text-memo                  | Text of attachments field of inquiry         |
| .faqData_info-con .dataTime .noticeType | Heading of item of notice table      |
| .faqData_info-con .dataTime .noticeType .icon-leavel-1 | Heading icon of item of notice table |

##### search.css
| Element Name                          | Details                                |
| ---------------------------------- | ---------------------------------- |
| .paginate                          | Pagination area                   |
| .paginate li                       | Item of pagination area                 |
| .paginate li.firstPage a           | << key of pagination area                |
| .paginate li.firstPage a.img       | Image of << key of pagination area            |
| .paginate li.prev a.               | < key of pagination area                   |
| .paginate li.prev a img            | Image of < key of pagination area      |
| .paginate li a                     | Each page of pagination area             |
| .paginate li.number.active a       | Current page of pagination area        |
| .paginate li.next a.               | > key of pagination area               |
| .paginate li.next a img            | Image of > key of pagination area           |
| .paginate li.lastPage a            | >> key of pagination area                  |
| .paginate li.lastPage a.img        | Image of >> key of pagination area            |
| .search-title                      | Title of search result                   |
| .search-title strong               | Search term (emphasized) of search result         |
| .search-text                       | Search result                        |
| .search-text .search-title_sub     | Subclass of search result                  |
| .search-text .search-text_lit      | Item of search result               |
| .search-text .search-text_lit dt a | Title of item of search result               |
| .search-text .search-text_lit dd .search-text_con | Preview of contents of item of search result |
| .search-text .search-text_lit dd .search-text_time | Registered date of contents of item of search result |

##### inquiry.css
| Element Name                   | Details                                |
| ---------------------------------- | ---------------------------------- |
| .selectStyle                       | Option of search                    |
| .inquiry-con                       | Contents area of inquiry                |
| .inquiry-con_table                 | Inquiry table                      |
| .inquiry-con_table th              | Field of inquiry table                 |
| .bl_ess                            | Required field of inquiry table         |
| .inquiry-con_table td              | Input of inquiry table                |
| .error_txt                         | Input of inquiry table (Error)     | 
| .inquiry-btn                       | Submit button of inquiry table                  |
| .layui-icon                        | Arrow button                        |
| .layui-icon-right                  | Left arrow button            |
| .layui-icon-up                     | Down arrow button            |
| .check_area_wrap .td-radio .layui-form-checkbox\[lay-skin="primary"] span | Checkbox text|
| .error_txt                         | Error text                       |

### Manage File Uploads
![](http://static.toastoven.net/prod_contact_center/2.2.5-(3)_en.png)
As a tool for managing the files used to create templates and layouts, you can upload the files through the **① Upload File** button and use **② File Path** of the resource without having to upload files every time. File names could not be duplicated.

### Default Settings
![](http://static.toastoven.net/prod_contact_center/2.2.5-(4)_en.png)
You can **Enable** functions you use in the Help Center and **Disable** functions you don't use. When disabled, the function becomes hidden from the Help Center page.

Functions you can manage are as follows:
-	Notice
-	FAQ
-	1:1 Inquiry & My Inquiries
-	Chat
-	Help center navigation

## External Channel
Inquiries received by external services could be switched to tickets in Online Contact. Twitter and KakaoTalk are currently supported services.

### Twitter
![](http://static.toastoven.net/prod_contact_center/2.2.6-(1)_en.png)
You can **① Enable** or **Disable** Twitter connection, and could register Twitter account by **② Register** button when Twitter connection is enabled.

![](http://static.toastoven.net/prod_contact_center/2.2.6-(2)_en.png)
When registering your account, you can set whether to switch tickets for **① Tweet(Mention)** and **② Direct message** respectively, and if you wish to convert direct messages to a ticket, please check the procedure below.

Access your Twitter account and check More → Settings and Privacy → Privacy and Safety → Direct Messages → **Receive message requests** must be enabled before a message to the linked account can be received as a ticket.

### Kakao Talk Plus Friend
![](http://static.toastoven.net/prod_contact_center/2.2.6-(3)_en.png)
You can **① Enable** or **Disable** KakaoTalk connection, and could register KakaoTalk ID and date to activate by **② Register** button when KakaoTalk connection is enabled. The connection takes up to 1~2 business days, and if the connection is rejected, the reason for rejection will be displayed. You must change Management → Detailed Settings → Channel Home → Enable Public Search to **ON** in the KakaoTalk channel manager center to connect with Online Contact.

![](http://static.toastoven.net/prod_contact_center/2.2.6-(4)_en.png)
Click on the **Account which is connected** to set up the details of the KakaoTalk function.

- **①** Consultation time
- **②** Days available for consultation
- **③** Auto comment
    - Out of business hours: Comment sent when chat request received **besides the consultation time**
    - First greeting: Comment sent when **chat consultation connected**
    - No agent: Comment sent when **all agents are offline**
    - Request for evaluation: Comment sent with the **evaluation request** from the agent
    - End of consultation: Comment sent when consultation **ended**

When KakaoTalk is connected and activated in Online Contact, the existing plus friend 1:1 chat will be stopped, and inquiries received through KakaoTalk will be showed in the chat screen, with ‘channel’ of the ticket marked as ‘KakaoTalk’.

## Security Management
![](http://static.toastoven.net/prod_contact_center/2.2.6-(5)_en.png)
If you have enabled the Service Management → Security Service feature in the contract information through prior consultation you can enable or disable **log linkage** in the  **Security Service** menu.
Please contact the Online Contact administrator for enabling/disabling of log interlocking services through **Online Contact Customer Center**. ([Online Contact Customer Center Shortcut](https://nhn-contact.oc.toast.com/oc/hc/))
