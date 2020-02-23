# <a id="top">Consenz new Flows specifications</a>
The details and mock ups of the different pages that have to be developed
- [Notes](#notes)
  - [Topic Two Uses](#topic-two-uses)
  - [Site Language](#site-language)
  - [Design and Visual](#design-and-visual)
- [Pages](#pages-description)
  - [Entering Page View](#entering-page-view)
  - [Choose Topics Page View](#choose-topics-page-view)
  - [New Votes Page](#new-votes-page)
    - [Section Proposal](#section-proposal)
    - [Voting Buttons Section](#voting-buttons-section)
    - [Voting Counters](#voting-counters)
    - [Suggestion Navigation Buttons](#suggestion-navigation-buttons)
    - [Arguments Section](#arguments-section)
    - [Notifications Check Boxes](#get-notification).
  - [Summary Page](#summary-page)
- [Pages Topics](#topics)
  - [User Menu](#user-menu)
  - [Bread Crumbs](#bread-crumbs)
  - [User Avatar](#user-avatar)
  - [Timestamp](#timestamp)
- [Logics](#logics)
  - [Rules](#rules)
    - [User Connected Rule](#user-connected-rule)
  - [Algorithms](#algorithms)
    - [Most Agreed Upon](#most-agreed-upon)
# 1. <a id="notes">Notes</a>
## 1.1 <a id="topic-two-uses">Topic Two Uses</a>
The word 'Topic' confusingly appears is two different uses:
- A UI page high level element<br>
(each page is composed from a list of topics, each topic can be composed of other elements) 
- A Topic in the main Consenz Document<br>
(each section suggestion relates to a specific topic in the document discussion)
## 1.2 <a id="site-language">Site Language (Internationalization)</a>
- The current pages are coded with <b>Hebrew</b> labels hard-coded (very bad) in the vue html files
- The labels of the new pages should come from an app-dictionary key-value file, so it would be possible to support both English and Hebrew languages.
- The freelancer need to create only the English dictionary file that is used by the new pages.
- In the review step of each milestone, we may change the dictionary texts<br>
and add the Hebrew dictionary file based on the english dictionary, in order to check how it looks.<br>
- it should be easy to configure the application to work with any dictionary.

## 1.3 <a id="design-and-visual">Design and Visual</a>
- The specifications and page mock-ups do not go into design details but only define the logics and general looks of the pages.
- The freelancer has the flexability to design the pages as he sees fit, following the specification's technical requirements.
## 1.4 Admin Edited Text
- some of the elements take their text from data fields that the Admin edits. (like [Welcome Text](#welcome-text))
- There is No need to support Admin API for updating admin data.<br>
Just edit the json mock data and start the application with the mock data containing any needed fields.
# 2. <a id="pages-descriptions">Pages</a>
## 2.1. <a id="entering-page-view">Entering Page View</a>
The goal of the page is to introduce the user to document (see [Document](./project_overview.md/#document_definition) definition) discussion process,<br>
Explain the document issues and encourage her to sign up and participate.
### 2.1.1. Specification
#### 2.1.1.2. __Page Topics__
- <a id="welcome-text">Welcome Text</a> - Static text, Edited by Admin user, represents overview. May include discussion preview
- Proceed to choose Topic Clickable (Button, Link, ect.)
  - action: The user clicks on this element and the page view shifts to [Choose Topics Page View](#choose-topics-page-view)
- [_User Menu_](#user-menu)
- [_Bread Crumbs_](#bread-crumbs)
### 2.1.2. __Mockup__:
The mockups are presented in two languages: english and hebrew
![image](https://user-images.githubusercontent.com/12394551/71320184-873d3180-24b0-11ea-89ad-37513f589a34.png)
![entering_page_mockup](https://user-images.githubusercontent.com/42510547/70627786-80e8c300-1c2f-11ea-93f3-33f3a6ffe004.png)
 - This mockup is missing the User Menu and Bread Crumbs elements

## 2.2. <a id="choose-topics-page-view">Choose Topics Page View</a>
The goal is to give the user an option to choose the topics relevant to her.<br>
This page contains the topics list for the current [Document](./project_overview.md/#document_definition).<br>
The list should be a multiple selection checkbox,<br>
where the user can select either one, some, or all of the options.<br>
The default mode is that the "view all topics" option is marked.<br>
The [Proceed to Votes](#proceed_to_votes) button leads to the [New Votes Page](#new-votes-page).<br>
If no option is selected the user will go through _all_ of the vote Suggestions in the Document.<br>
Otherwise he'll go through vote suggestions _specific_ to the Topics selected.  
### 2.2.1. Specification
#### 2.2.1.1. __Variables__:
- topicsSelectedList - List of all Topics selected by the user
#### 2.2.1.2. __Page Topics__
- Topics list<br>
List of the topics in the document that are up for a vote. each one can be marked with a checkbox
  - Each item in the list is the topic string label and a checkbox that if marked then the topic is added to the topicsSelectedList list.
- <a id="proceed_to_votes">Proceed to Votes</a><br>
A button that leads to the [New Votes Page](#new-votes-page)
  - If the user selected some topic (topicsSelectedList Not Empty)<br>
  then the New Votes Page will be in [__Specific Topic__](#specific-topic-mode) mode.
  - If the user did not select any topic (topicSelectedList Empty)<br>
    then the New Votes Page will be in [__All Topics__](#all-topics-mode) mode.
- Mark All Checkbox
- [_User Menu_](#user-menu)
- [_Bread Crumbs_](#bread-crumbs)
### 2.2.2. __Mockups__:
#### 2.2.2.1. __Mock up 1__:  
![topics_list_mockup2](https://user-images.githubusercontent.com/42510547/70627781-7fb79600-1c2f-11ea-8b7b-912ab69e9484.png)
![image](https://user-images.githubusercontent.com/12394551/71320192-9623e400-24b0-11ea-93e9-a452181eaf3c.png)
- This mockup is missing the User Menu and Bread Crumbs elements
#### 2.2.2.2. __Mock up 2__:  
![topics_list_mockup2](https://user-images.githubusercontent.com/12394551/70518786-9c769f80-1b43-11ea-801d-035e9999adf8.png)
- This mockup contains also the User Menu and Bread Crumbs elements
## 2.3. <a id="new-votes-page">New Votes Page</a>
- This page presents all [Section](./data_model.md/#section) Suggestions that are up for voting.<br>
- Either of New Sections or Edit Suggestions of existing sections.<br>
- One suggestion in a page view.<br>
- The Suggestions are presented to the user according to the [Most Agreed Upon](#most-agreed-upon) sorting algorithm and the user selections in the Choose Topics page.<br>
- The user can navigate between the suggestions that stand for a vote.<br>
- When the user is finished voting on all open Suggestions he's redirected to the [Summary page](#summary-page).

The page displays the [Section Proposal](#section-proposal) to be voted upon,<br>
the creator [User Avatar](#user-avatar), publication [Timestamp](#timestamp),<br>
[Voting Buttons Section](#voting-buttons-section), [Voting Counters](#voting-counters), [Navigation Buttons](#suggestion-navigation-buttons),<br>
[Arguments Section](#arguments-section) and [Notifications Check Boxes](#get-notification).

![74644670-4f382f00-517f-11ea-9854-800b7502b5e9](https://user-images.githubusercontent.com/12394551/75106569-daee0780-5626-11ea-9ed3-669ff2ea52fe.png)
### 2.3.1. Topic Title
data-model: **Section**, field: **topic**
### 2.3.2. <a id="section-proposal">Section Proposal</a>
The proposed Section text, [User Avatar](#user-avatar) of proposing user and the published [Timestamp](#timestamp)
- Label: dictionary parameter: **newSectionSuggestion**
  - he:	'הצעה לסעיף חדש'
  - en:	'New Section Suggestion'
- Proposed Section text:	data-model: **Section**, field: **contentHtml**
- Timestamp: data-model: **Section**, field: **created_at**
- User Avatar should be as in existing **/document/springfield/section** implementation

The visual element is already implemented and can be seen [here](https://new-votes-page.netlify.com/#/document/springfield/section?sectionsByStatus=4&index=1&id=gErAFwNUsnlKwD2WOZAX).<br>
**The code should be reused**

![Image20200220185633](https://user-images.githubusercontent.com/12394551/74959235-e2d55e00-5412-11ea-998d-1de3fcdf3b71.png)

### 2.3.3. <a id="voting-buttons-section">Voting Buttons Section</a>
- Voting buttons of current suggestion.
- Float buttons, Shown regardless of scrolling page state.<br>
- All buttons actions follows the [User Connected Rule](https://github.com/wonderfloyd/Consenz_Requierments/blob/master/pages_specifications.md/#user-connected-rule)<br>
  
#### 2.3.3.1. Vote Button - Pro
- The user Press the Pro button.<br>
The Action executes the existing [Vote Pro](#vote-logic) logic. **The logic code should be reused**
    - data-model: **Section**, field: **pros** (Array), operation: Add current user id
  - Label: dictionary parameter: 'proButton'
    - he:	'בעד'
    - en:	'Pro'
#### 2.3.3.2. Vote Button - Con
  - The user Press the Con button.<br>
  the Action executes the existing [Vote Con](#vote-logic) logic. **The logic code should be reused**
    - data-model: **Section**, field: **cons** (Array), operation: Add current user id
  - Label: dictionary parameter: 'conButton'
    - he:	'נגד'
    - en:	'Con'

![Image20200220190800](https://user-images.githubusercontent.com/12394551/74960280-b6224600-5414-11ea-9e60-018c22dd42f1.png)
##### <a id="vote-logic">Vote Logic</a>
Voting Pro/Con logic is already implemented.
see example in [here](https://new-votes-page.netlify.com/#/document/springfield/section?sectionById=wLl23iX4gZCoQl11JqEV&index=1)
![Image20200219172555](https://user-images.githubusercontent.com/12394551/74848127-0e3b4880-5340-11ea-963c-e9ac62777799.png)
![Image20200219173119](https://user-images.githubusercontent.com/12394551/74848141-12676600-5340-11ea-8141-b1692dab499d.png)
#### 2.3.3.3. Vote Con Argument Text Area
- Text Area and a publish button that let the user, following his Con Vote, add his argument about his Con Vote.
- This element appears only if the user voted Con (clicked the Vote Con button)
 
![74987735-8be87c80-5444-11ea-837e-5e08436fc2b5](https://user-images.githubusercontent.com/12394551/75015850-4e124500-5492-11ea-9f7d-28e09c95630f.png)
- When the user press the 'Publish' button, a new Con Argument is added to the suggestion section.
  - The new argument should appear first in the arguments section
- Labels:
  - Title
    - dictionary parameter: **voteConArgumentTitle**
    - he:	'הוספת הסתייגות'
    - en:	'Add Con Argument'
  - Publish Button
    - dictionary parameter: **voteConArgumentButton**
    - he:	'פרסום והצבעה'
    - en:	'Publish Con Argument'

 - **The text area elements and Publish logic should reuse the existing Add Con Argument logic**
- In the existing logic when the user adds a Pro/Con argument, it is automatically counted as a Pro/Con voting respectively
- The requirement for the New Votes Page is to show the 'Add Argument' text box in the existing page under the vote buttons only in case the user voted Con. Then, if the user adds an argument, it is not needed to do the voting logic again as in the existing implementation, only the add argument logic.
##### Existing Add Con Argument Logic
Adding a Con/Pro Argument logic and elements are already implemented in other existing page.
see example in [here](https://new-votes-page.netlify.com/#/document/springfield/section?sectionById=wLl23iX4gZCoQl11JqEV&scrollId=k6ui5ilh&scrollTo=argument)

![Image20200220104254](https://user-images.githubusercontent.com/55399150/74917324-00cd9f00-53d0-11ea-905c-74559087969a.png)
![Image20200220104645](https://user-images.githubusercontent.com/55399150/74917358-0cb96100-53d0-11ea-816c-5c7b5325742d.png)
![Image20200220104506](https://user-images.githubusercontent.com/55399150/74917388-14790580-53d0-11ea-9718-4f36cd3e6fc6.png)
![Image20200220104851](https://user-images.githubusercontent.com/55399150/74917411-1cd14080-53d0-11ea-92b9-bf760f30ea7b.png)
#### 2.3.3.4. Add New Edit Suggestion
- A button that opens a box for adding edit section suggestion text.
- This element appears only if the user voted Con (clicked the Vote Con button)
- Position: under the Vote Con Argument Text Area element
- Label: dictionary parameter: **addNewEditSuggestionButton**
  - he:	'הוסף הצעה חדשה'
  - en:	'Add a new suggestion'

![Image20200216181121](https://user-images.githubusercontent.com/12394551/75021765-971bc680-549d-11ea-905e-8324e60bf055.png)

##### New Edit Suggestion Section
When the user click on the Add New Edit Suggestion button. these elements appear:
- Editable text box contains the text of the section content
- a "Publish" grayed un-active button

Labels:
  - Original Section Text
    - dictionary parameter: **originalSectionText**
    - he:	'נוסח הסעיף המקורי'
    - en:	'Original section text'
  - Original Section Text
    - dictionary parameter: **mySectionProposal**
    - he:	'נוסח ההצעה שלי'
    - en:	'My Section Proposal'
  - Add Button Label
    - dictionary parameter: **publishNewEditSuggestionButton**
    - he:	'הוספה'
    - en:	'Publish'

![Image20200216181121](https://user-images.githubusercontent.com/12394551/75033867-8b87ca00-54b4-11ea-820b-92b93d5f8142.png)

- The user can change text, then the "publish" button becomes active and colored
- After clicking "publish" the text will be added as a New Edit Suggestion
- The page renders to show the new suggestion, with 1 Pro vote, of the creating user
- A Section data-model document is created:


    {
      "id": "[Generated]",
      "parentSectionId": "[id of original section]",
      "createdAt": "[Current Date]",
      "created_at": [Current Date],
      "cons": [],
      "pros": [
        "[id of current user]"
      ],
      "created_by": "[id of current user]",
      "owner": "[id of current user]",
      "content": "[New Text Suggesiton]",
      "status": 4, (Change existing section, on vote)
      "threshold": [Document.threshold} (according documentId)
      "documentId": [Document.id],
      "topic": [Document.topic],
    }
##### Existing implementation
- The 'Add New Edit Suggestion' logic and elements are already implemented in other existing page and **the code should be reused**<br>
- see example in [here](https://new-votes-page.netlify.com/#/document/springfield/section?sectionsByStatus=4&index=1&id=J11Yn1UkNDQcpxtaKyh6)

- Press the + button

![Image20200220131613](https://user-images.githubusercontent.com/55399150/74929430-1fd62c00-53e4-11ea-9ede-949f8af1efcd.png)
![Image20200220131353](https://user-images.githubusercontent.com/55399150/74929457-2e244800-53e4-11ea-98ef-3dbd9e713128.png)

- Change the original section text and press the Add button

![Image20200220131723](https://user-images.githubusercontent.com/55399150/74929529-5f047d00-53e4-11ea-98eb-0394dc5b3c88.png)
![Image20200220131825](https://user-images.githubusercontent.com/55399150/74929573-75123d80-53e4-11ea-9304-e6e631831703.png)

- Press the 'Add without an Argument' button

![Image20200220131851](https://user-images.githubusercontent.com/55399150/74929606-8ce9c180-53e4-11ea-9110-18b1d02380e3.png)
![Image20200220131948](https://user-images.githubusercontent.com/55399150/74929676-adb21700-53e4-11ea-90cd-bd42054e97ce.png)
- The new suggestion appears in the suggestions page

![Image20200220132045](https://user-images.githubusercontent.com/55399150/74929733-c6bac800-53e4-11ea-8452-412caf3f8789.png)
### 2.3.4. <a id="voting-counters">Voting Counters</a>
Pro and Con Counters of current suggestion<br>
The Counters are displayed on the Voting buttons and show current state of voting counters
- Pro Counter: data-model: **Section**, field: **pros**, operation: count (length)
- Con Counter: data-model: **Section**, field: **cons**, operation: count (length)
### 2.3.5. <a id="suggestion-navigation-buttons">Suggestion Navigation Buttons</a>
Navigation buttons that allow the user to navigate between suggestions up for a vote according to the [Most Agreed Upon](#most-agreed-upon) sorting algorithm and the user selections in the Choose Topics page.<br>
There are 2 buttons:
### 2.3.5.1. Next Suggestion Button
- Label: dictionary parameter: **nextSuggestion**
  - he:	'הבא >>'
  - en:	'Next >>'
- Starting with greyed out button.<br>
The user can still press the button and navigate to the next suggestion.
- After the user votes the button is highlighted to indicate the user should press it and move to next suggestion
- When the user press the 'Next Suggestion' button the page renders to the next suggestion for voting
- The next suggestion is according to the [Most Agreed Upon](#most-agreed-upon) sorting.
- If current shown suggestion is the last suggestion, then the user is transferred to the [Summary Page](#summary-page).
### 2.3.5.2. Back Button
Change page view back to previous suggestion<br>
If the user is in the first suggestion and press the Back Button then it shifts back to Select Topics Page View.

**The Back Button visual element is already implemented and should be reused**

![Image20200220131613](https://user-images.githubusercontent.com/12394551/74960880-cab30e00-5415-11ea-93a3-ba584c36da2f.png)
- Label: dictionary parameter: **backButton**
  - he:	'->'
  - en:	'->'
### 2.3.6. <a id="arguments-section">Arguments Section</a>
- List of all suggestion arguments
- Sorted by creation time. Newer comes first according to the Argument.created_at field.
- Each argument has 1 of 2 modes: Pro, Con according to the Argument.type field:
  - true - Pro (The pro argument should appear on green background)
  - false - Con (The con argument should appear on red background)

![Image20200216181121](https://user-images.githubusercontent.com/12394551/74990813-f4d3f280-544c-11ea-894a-2c3f48c6ef52.png)

Each argument is composed from 4 elements:
1. Argument Text	data-model: Argument	field: 'contentHtml'
2. User Avatar		corresponds to	data-model: Argument	field: 'owner'
3. Timestamp (published)	data-model: Argument	field: 'created_at'
4. Comments List. Each comment is composed of 3 elements:
	1. Comment Text	data-model: Comment	field: 'contentHtml'
	2. User Avatar	corresponds to	data-model: Comment	field: 'owner'
	3. Timestamp (published)	data-model: Comment	field: 'created_at'

- The Arguments Section logic and elements are already implemented in other existing page and **the code should be reused**<br>
- see example in [here](https://new-votes-page.netlify.com/#/document/springfield/section?sectionById=269KTx7D1eVrbM0gTUM7&index=2)

![Image20200221013334](https://user-images.githubusercontent.com/12394551/74990051-cfde8000-544a-11ea-8cd5-bb909db89874.png)
#### 2.3.6.1. Overview:
- An argument corresponds to the Argument data-model.
  - its 'sectionId' field links to the the section the argument relates to.
  - A section may have multiple arguments.
- A comment corresponds to the Comment data-model.
  - its 'argumentId' field links to the the argument the comment relates to.
  - its 'sectionId' field links to the the section the argument of the comment relates to.
  - An argument may have multiple comments.
### 2.3.7. <a id="get-notification">Get Notifications Check Boxes</a>
'New Argument Or Comment' and 'New Edit Suggestion' Check boxes that allow the user to register for email notifications regards the current suggestion in the page.
- The user checks the Notification check boxes that he's interested getting email notifications.
- The check box becomes marked/unmarked.
- The corresponding Section data-model notifications field is updated.
- Notification Types:
  - New Argument Or Comment
    - data-model: Section
      - field: notifications.newArgumentOrComment (Array)
      - operation: Add/Remove current user id
    - dictionary parameter: **newArgumentOrCommentNotification**
      - he:	'ברצוני לקבל עדכון כאשר מתווספים טיעון או הערה'
      - en:	'Get notification on new argument or comment'
  - New Edit Suggestion
    - data-model: Section
      - field: notifications.newEditSuggestion (Array)
      - operation: Add/Remove current user id
    - dictionary parameter: **newEditSuggestionNotification**
      - he:	'ברצוני לקבל עדכון כאשר מתווספת הצעה חדשה לשינוי הסעיף'
      - en:	'Get notification on new argument or comment'

![Image20200216181121](https://user-images.githubusercontent.com/12394551/75096605-eea75880-55a9-11ea-967d-1ead088dbd6f.png)
### 2.3.8. [_User Menu_](#user-menu)
### 2.3.9. [_Bread Crumbs_](#bread-crumbs)

## 2.4. <a id="summary-page"></a>Summary Page
This page is displayed once the user have finished voting on all Sections open for a vote.<br>
It gives the user feedback that she finished the task of voting,<br>
 explain how she could continue participate in the process and encourage her to register for e-mail notifications for her choice.  
### 2.4.1. Specification
#### 2.4.1.1. __Page Topics__
- End Text - Static text, Edited by Admin user
- Notifications Panel - Displays all the notifications the user can register for:
    - [Get Notification](#get-notification) for new document versions
    - [Get Notification](#get-notification) for new edit suggestions
    - [Get Notification](#get-notification) for new section suggestions
    - [Get Notification](#get-notification) for new argument and comment
- [_User Menu_](#user-menu)
- [_Bread Crumbs_](#bread-crumbs)
### 2.4.2. __Mockup__:
![summary_page_mockup](https://user-images.githubusercontent.com/42510547/70627790-8219f000-1c2f-11ea-8b98-862679decad7.png)
![image](https://user-images.githubusercontent.com/12394551/71320197-a3d96980-24b0-11ea-9402-dbab60ab71b0.png)

# 3. <a id="topics">Pages Topics</a>
Simple or Compound elements that are used in the different pages as page topics
## 3.1. <a id="user-menu">__User Menu__</a>
High level User Navigation Panel composed of these items:
  - Sign Out
  - About Consenz
  - About This Document
  - Name: Go to Draft Page Clickable that directs the user to the [Draft Page]()

The User Menu is already implemented in existing code. Need to integrate it also in new pages
## 3.2. <a id="bread-crumbs">__Bread Crumbs__</a>
Breadcrumbs Navigation title that shows the relation to other pages in user flow for orientation.<br>
Bread Crumbs should consist from:<br>
`[document.id] - [section.topic] - [suggestionRelativePosition]`<br>
- suggestionRelativePosition : dictionary parameter: **suggestionRelativePosition**
  - he:	'הצעה X מתוך Y'
  - en:	'suggestion X of Y'

for example, If the document id is **springfield**,<br>
the section topic is **אנרגיה**,<br>
the total suggestions is **12**<br>
and the current suggestion index is **2**<br>
then the Bread Crumbs should be:<br>
- English:  `springfield -> אנרגיה -> suggestion 2 of 12`
- Hebrew:   `אנרגיה   ->  הצעה 2 מתוך 12  <-  springfield`

 **Breadcrumbs structure is already implemented. it should be integrated in new page**
## 3.3. <a id="user-avatar">__User Avatar__</a><br>
User presentation (Name and icon).<br>
This presentation should also differ between a _regular_ user and _editor_ user.<br>
It is composed from 2 elements:
  - User Name - String
  - User Pic - Image
## 3.4. <a id="timestamp">__Timestamp__</a>
Date of corresponding event (argument, comment, ect.),<br>
The Timestamp element should present in 3 modes: _Published_, _Accepted_, _Declined_
# 4. <a id="logics">Logics</a>
The logical specifications that are used in the pages flows
## 4.1 <a id="rules">Rules</a>
### 4.1.1 <a id="user-connected-rule">__User Connected Rule__</a>
When the user tries to perform an action that only a Logged-In (Connected) user can perform.<br>
- If the user is connected than the action executes according to the action logic.<br>
- If the user is not connected, then he is directed to login page.<br>
After the user logs in, he is directed back to the page where the action he wanted to perform<br>
and the action continue to execute according to the action logic (feedback, to, ...)  
## 4.2<a id="algorithms"></a> Algorithms:
### 4.2.1. <a id="most-agreed-upon">__Most Agreed Upon__</a> Sorting
Sorting Algorithm that prefers suggestions that are closer to be accepted.<br>
I.e. Their threshold distance is closer to 0
- threshold: data-model: Section, field: 'threshold'
- prosConsDelta: Section.pros.length() - Section.cons.length()
- thresholdDistance: threshold - prosConsDelta    =   threshold + Section.cons - Section.pros
##### Variables:
- suggestionsList: List of all [Suggestions](./project_overview.md/#suggestion_definition) for voting according to user selection in the Choose Topics page. The list should consist of all [Section](./data_model.md/#section) instances which their [status](./data_model.md/#status) field is 0 or 4 and that their 'topic' field belongs to a topic that the user selected in the Choose Topics page.
- x, y: Suggestion items in suggestionsList for voting
##### Logic:
    For x, y in suggestionsList:
    x before y if thresholdDistance of x is smaller than thresholdDistance of y.
    I.e. x before y if (x.threshold - (x.pros - x.cons)) < (y.threshold - (y.pros - y.cons))
    I.e. x before y if (x.threshold + x.cons - x.pros) < (y.threshold + y.cons - y.pros)
    
    * If 2 or more suggestions have the same thresholdDistance, than the sorting
    would prefer (show first) the newer suggestion according to the Section.created_at field.
