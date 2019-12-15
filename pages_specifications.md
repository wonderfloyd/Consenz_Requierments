# <a id="top">Consenz new Flows specifications</a>
The details and mock ups of the different pages that have to be developed
- [Notes](#notes)
- [Pages](#pages-description)
  - [Entering Page View](#entering-page-view)
  - [Choose Topics Page View](#choose-topics-page-view)
  - [New Votes Page](#new-votes-page)
  - [Summary Page](#summary-page)
- [Pages Topics](#topics)
  - [Vote Counters](#vote-counters)
  - [Vote Buttons](#vote-buttons)
  - [Add New Edit Suggesetion Clickable](#add-new-edit-suggestion-clickable)
  - [Arguments Section](#arguments-section)
  - [Arguments Block](#arguments_block)
  - [Suggestion Navigation Buttons](#suggestion-navigation-buttons)
  - [User Avatar](#user-avatar)
  - [User Menu](#user-menu)
  - [Bread Crumbs](#bread-crumbs)
- [Items](#items)
  - [Timestamp](#timestamp)
  - [Vote Counter](#vote-counter)
  - [Vote Button](#vote-button)
  - [Suggestions Progress Bar](#suggestions-progress-bar)
  - [Get Notification](#get-notification)
- [Logics](#logics)
  - [Rules](#rules)
    - [User Connected Rule](#user-connected-rule)
  - [Algorithms](#algorithms)
    - [Most Agreed Upon](#most-agreed-upon)
    - [Specific Topic Suggestions](#specific-topic-suggestions)
    - [Sort by Topic](#sort-by-topic)

## 1. <a id="notes">Notes</a>
- The word 'Topic' confusingly appears is two different uses:
  - A UI page high level element<br>
  (each page is composed from a list of topics, each topic can be composed of other elements) 
  - A Topic in the main Consenz Document<br>
  (each section suggestion relates to a specific topic in the document discussion)
  
## 2. <a id="pages-descriptions">Pages</a>
### 2.1. <a id="entering-page-view">Entering Page View</a>
The goal of the page is to introduce the user to document (see [Document](./project_overview.md/#document_definition) definition) discussion process,<br>
Explain the document issues and encourage her to sign up and participate.
#### 2.1.1. Specification
##### 2.1.1.2. __Page Topics__
- Welcome Text - Static text, Edited by Admin user, represents overview. May include discussion preview
- Proceed to choose Topic Clickable (Button, Link, ect.)
  - action: The user clicks on this element and the page view shifts to [Choose Topics Page View](#choose-topics-page-view)
- [_User Menu_](#user-menu)
- [_Bread Crumbs_](#bread-crumbs)
#### 2.1.2. __Mockup__:
![entering_page_mockup](https://user-images.githubusercontent.com/42510547/70627786-80e8c300-1c2f-11ea-93f3-33f3a6ffe004.png)
- This mockup is missing the User Menu and Bread Crumbs elements 

### 2.2. <a id="choose-topics-page-view">Choose Topics Page View</a>
The goal is to give the user an option to choose the topics relevant to her.<br>
This page contains the topics list for the current [Document](./project_overview.md/#document_definition).<br>
The list should be a multiple selection checkbox,<br>
where the user can select either one, some, or all of the options.<br>
The default mode is that the option of "view all topics" is marked.
The [Proceed to Votes](#proceed_to_votes) button leads to the [New Votes Page](#new-votes-page).<br>
If no option is selected the user will go through _all_ of the vote Suggestions in the Document.<br>
Otherwise he'll go through vote suggestions _specific_ to the Topics selected.  
#### 2.2.1. Specification
##### 2.2.1.1. __Variables__:
- topicsSelectedList - List of all Topics selected by the user
##### 2.2.1.2. __Page Topics__
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
#### 2.2.2. __Mockups__:
##### 2.2.2.1. __Mock up 1__:  
![topics_list_mockup2](https://user-images.githubusercontent.com/42510547/70627781-7fb79600-1c2f-11ea-8b7b-912ab69e9484.png)
- This mockup is missing the User Menu and Bread Crumbs elements
##### 2.2.2.2. __Mock up 2__:  
![topics_list_mockup2](https://user-images.githubusercontent.com/12394551/70518786-9c769f80-1b43-11ea-801d-035e9999adf8.png)
- This mockup contains also the User Menu and Bread Crumbs elements
### 2.3. <a id="new-votes-page">New Votes Page</a>
This page presents all Section Suggestions that are up for voting.<br>
Either of New Sections or Edit Suggestions of existing sections.<br>
One suggestion in a page view.<br>
The Suggestions are presented to the user in two modes: [All Topics](#all-topics-mode), [Specific Topic](#specific-topic-mode).<br>
The user can navigate between the suggestions that stand for a vote.<br>
When the user is finished voting on all open Suggestions he's redirected to the [Summary page](#summary-page).
#### 2.3.1. Specification
#### 2.3.1.1. <a id="page-mode">__Modes__</a>:
1. <a id="all-topics-mode">__All Topics__</a><br>
Navigate through __all__ of the suggestions that are up for vote.<br>
This mode is active when the user haven't selected any topic in the previous [Choose Topics Page View](#choose-topics-page-view).<br>
In this mode the suggestions are sorted by the [Most Agreed Upon](#most-agreed-upon) algorithm: Suggestion that is closer to be accepted (threshold closest to 0) is shown first.
2. <a id="specific-topic-mode">__Specific Topic__</a><br>
Navigate only through suggestions __specific__ to a topic that the user have selected in the previous [Choose Topics Page View](#choose-topics-page-view).<br>
In this mode the suggestions are filtered by the [Specific Topic Suggestions](#specific-topic-suggestions) filter and sorted by the [Sort by Topic](#sort-by-topic) algorithm.
#### 2.3.1.2. __Page Topics__:
- Suggestion Unit<br>
A compound element that displays the proposal to be voted upon,
the creator [User Avatar](#user-avatar),<br>
publication timestamp, acceptance threshold, a timer counting down the time left to vote,<br>voting counters, voting buttons and an arguments block.<br>
If it is a Suggestion for an edit of the Section than it will also display the current state and changes to be decided on.
  - modes:
    - New Section - Vote on new [Section](./project_overview.md/#section_definition)
    - Edit Section - Vote to edit an existing [Section](./project_overview.md/#section_definition).  
  - items:
    - Current Section - Displayed only in 'Edit Section' mode.<br>
    The text of the original section that is being voted for a change.
    - Section Proposal - The proposed Section text, [User Avatar](#user-avatar) of proposing user and the published [Timestamp](#timestamp)
    - Threshold (Number)
    - Timer (Countdown Clock)
    - [Vote Counters](#vote-counters)
    - [Vote Buttons](#vote-buttons) - float buttons, will showed without considering scrolling page state
    - [Arguments Section](#arguments-section)
    - [Add New Edit Suggestion Clickable](#Add-New-Edit-Suggestion-Clickable)
- Topic Title (String)
- [Suggestion Navigation Buttons](#suggestion-navigation-buttons)
- [Get Notification](#get-notification)
- [Suggestions Progress Bar](#suggestions-progress-bar) - display how many suggestions the user haven't voted yet.
- Back Buttonm (Clickable) - Change page view back to the last view seen
- [_User Menu_](#user-menu)
- [_Bread Crumbs_](#bread-crumbs)
#### 2.3.2. __Mockups__:
#### 2.2.2.1. __Mock up 1 for New Suggestion__:  
![new_section_vote_mockup1](https://user-images.githubusercontent.com/42510547/70627788-81815980-1c2f-11ea-970e-8a02f6a8940c.png)
#### 2.2.2.2. __Mock Up 2 for New Suggestion__:
![new_section_vote_mockup2](https://user-images.githubusercontent.com/12394551/70518785-9c769f80-1b43-11ea-9dc3-cc9796b94ddd.png)
#### 2.2.2.3. __Mock up 1 for Editing Suggestion__:
![edit_section_vote_mockup1](https://user-images.githubusercontent.com/42510547/70627782-7fb79600-1c2f-11ea-9978-fcd1a7963d15.png)
#### 2.2.2.4. __Mock Up 2 for Editing Suggestion__:
![edit_section_vote_mockup2](https://user-images.githubusercontent.com/12394551/70518788-9c769f80-1b43-11ea-9de3-e8746172a0b0.png)

### 2.4. <a id="summary-page"></a>Summary Page
This page is displayed once the user have finished voting on all Sections open for a vote.<br>
It gives the user feedback that she finished the task of voting,<br>
 explain how she could continue participate in the process and encourage her to register for e-mail notifications for her choice.  
#### 2.4.1. Specification
##### 2.4.1.1. __Page Topics__
- End Text - Static text, Edited by Admin user
- Notifications Panel - Displays all the notifications the user can register for:
    - [Get Notification](#get-notification) for new document versions
    - [Get Notification](#get-notification) for new edit suggestions
    - [Get Notification](#get-notification) for new section suggestions
    - [Get Notification](#get-notification) for new argument and comment
- [_User Menu_](#user-menu)
- [_Bread Crumbs_](#bread-crumbs)
#### 2.4.2. __Mockup__:
![summary_page_mockup](https://user-images.githubusercontent.com/42510547/70627790-8219f000-1c2f-11ea-8b98-862679decad7.png)

## 3. <a id="topics">Pages Topics</a>
Simple or Compound elements that are used in the different pages as page topics
## 3.1. <a id="vote-counters">__Vote Counters__</a>
Pro and Con Counters of current suggestion vote.<br>
It is composed from 2 elements:
  - [Vote Counter](#vote-counter) (pro)
  - [Vote Counter](#vote-counter) (con)
## 3.2. <a id="vote-buttons">__Vote Buttons__</a>
Pro and Con voting buttons of current suggestion.<br>
It is composed from 2 elements:
  - [Vote Button](#vote-button) (pro)
  - [Vote Button](#vote-button) (con)
## 3.3. <a id="arguments-section">__Arguments Section__</a><br>
3 [arguments](./project_overview.md/#argument_definition) blocks.<br>
Each one has a different mode: _Pro_, _Con_, _Neutral_
  - [Arguments Block](#arguments_block) (pro)
  - [Arguments Block](#arguments_block) (con)
  - [Arguments Block](#arguments_block) (neutral)
## 3.4. <a id="arguments_block">__Arguments Block__</a><br>
Each block presents all the arguments with a specific mode: _Pro_, _Con_, _Neutral_<br>
Each block is composed from 4 elements:  
  - Argument Text
  - [User Avatar](#user-avatar)
  - [Timestamp](#timestamp) (published)
  - Comments List. Each comment is composed of 3 elements: 
    - Comment Text
    - [User Avatar](#user-avatar)
    - [Timestamp](#timestamp) (published)
## 3.5. <a id="suggestion-navigation-buttons">__Suggestion Navigation Buttons__</a><br>
Navigation buttons that allow the user to navigate between suggestions up for a vote according to the [sorting algorithm](#algorithms).<br>
There are 2 buttons:
### 3.5.1. Next Suggestion Clickable
  - Comment: Starting with greyed out clickable.<br>
    After user votes the clickable will be highlight in some graphic way, but in any time he can press 'Next Suggestion' and move to the next voting section.
  - Action: User clicks "Next Suggestion"<br>
    (New Votes Page -> Suggestion Navigation Buttons -> Next Suggestion)<br>
    The action depends on the [page mode](#page-mode): _All Topics_ or _Specific Topic_
    - All Topics: The page shows the next suggestion according to the [Most Agreed Upon](#most-agreed-upon) sorting.<br>
      If current shown suggestion is the last suggestion in this sorting<br>
      then the user is transferred to the [Summary page](#summary-page).
    - Specific Topic: The Page shows the next suggestion according to the [Sort by Topic](#sort-by-topic) sorting.<br>
      If current shown suggestion is the last suggestion in this Topic<br>
      then the next Topic is shown.<br>
      If the current shown suggestion is the last suggestion in this Topic and the Topic is the last topic in the document<br>
      than the user is transferred to the [Summary page](#summary-page).
    - End of New Suggestions: User reach the end of new suggestions page view and navigates to [Summary page](#summary-page).
### 3.5.2. Previous View Clickable
  - Action: User clicks "Previous View"<br>
    (New Votes Page -> Suggestion Navigation Buttons -> Previous View)<br>
    Show the last page that the user visit.<br>
## 3.6. <a id="user-avatar">__User Avatar__</a><br>
User presentation (Name and icon).<br>
This presentation should also differ between a _regular_ user and _editor_ user.<br>
It is composed from 2 elements:
  - User Name - String
  - User Pic - Image
## 3.7. <a id="user-menu">__User Menu__</a>
High level User Navigation Panel composed of these items:
  - Sign Out
  - About Consenz
  - About This Document
  - Name: Go to Draft Page Clickable that directs the user to the [Draft Page]()
## 3.8. <a id="bread-crumbs">__Bread Crumbs__</a>
Breadcrumbs Navigation title that shows the relation to other pages in user flow for orientation.

# 4. <a id="items">Items</a>
Simple elements operating as building blocks in the different pages topics
## 4.1. <a id="timestamp">__Timestamp__</a>
Date of corresponding event (argument, comment, ect.),<br>
The Timestamp element should present in 3 modes: _Published_, _Accepted_, _Declined_
## 4.2. <a id="vote-counter">__Vote Counter__</a>
Counter Number of a [Vote](./project_overview.md/#vote_definition) with specific mode: _Pro_ or _Con_
## 4.3. <a id="vote-button">__Vote Button__</a>
Button for voting on suggestion<br>
The [Vote](./project_overview.md/#vote_definition) has a mode: _Pro_ or _Con_
  - Action: The user interacts with one of the "Vote Button" buttons (Pro or Con)<br>
  The action follows the [User Connected Rule](#user-connected-rule)<br>
  The action result depend on the mode:
    - Pro:
      - voteCount(pro) = voteCount(pro) + 1
      - threshold = threshold - 1
    - Con
      - voteCount(con) = voteCount(con) + 1
      - threshold = threshold + 1
## 4.4. <a id="suggestions-progress-bar">__Suggestions Progress Bar__</a>
A Progress Bar that shows how many suggestions the user already voted and how many are left to vote.
## 4.5. <a id="get-notification">__Get Notification__</a>
A Check box that allow the user to register for email notifications regards a specific block:<br>
a new argument for a suggestion, a new comment for a argument, a change in a suggestion state ect.
- Action: User checks the 'Get Notification' element and changes it's state.<br>
  The check box becomes marked/unmarked.<br>
  New event will create a mail notification that will be sent to the user.<br>
- Currently there are 4 notification types:
  - New Document Versions Notification
  - New Edit Suggestions Notification
  - New Section Suggestions Notification
  - New Argument And Comment Notification
## 4.6. <a id="add-new-edit-suggestion-clickable">__Add New Edit Suggestion Clickable__
A clickable that open a box for adding edit section suggestion text. After publishing the new text will be added to suggestions list.
  - Action: User click on Add New Edit Suggestion Clickable.<br>
    A text box and "publish" button shows. The button is grayed and not active.
    In box the text of the section which the user visited last. The text is editable.
    After user change the text the "publish" button will be active and colored. 
    After clicking "publish" the text will be add as a new edit suggestion and the user will be transfer to the new suggestion vote page.

# 5. <a id="logics">Logics</a>
The logical specifications that are used in the pages flows
## 5.1 <a id="rules">Rules</a>
### 5.1.1 <a id="user-connected-rule">__User Connected Rule__</a>
When the user tries to perform an action that only a Logged-In (Connected) user can perform.<br>
- If the user is connected than the action executes according to the action logic.<br>
- If the user is not connected, then he is directed to login page.<br>
After the user logs in, he is directed back to the page where the action he wanted to perform<br>
and the action continue to execute according to the action logic (feedback, to, ...)  
## 5.2<a id="algorithms"></a> Algorithms:
### 5.2.1. <a id="most-agreed-upon">__Most Agreed Upon__</a>
Sorting Algorithm that prefers suggestions that are closer to be accepted<br>
I.e. There threshold is closer 0
#### 5.2.1.1. variables:
- suggestionsList: List of all [Suggestions](./project_overview.md/#suggestion_definition) for voting.<br>
  The list should consist of all Data-Model [Section](./data_model.md/#section) instances which their [status](./data_model.md/#status) field is 0 or 4
- x, y: Suggestion items in suggestionsList for voting
#### 5.2.1.2. logic
For x, y in suggestionsList: x before y if (x.pros - x.cons) > (y.pros - y.cons)
### 5.2.2. <a id="specific-topic-suggestions">__Specific Topic Suggestions__</a>
Filter of suggestions that accepts only suggestions with specific topic
#### 5.2.2.1. <a id="specific-topic-suggestions-variables">variables</a>
- specificTopic: String
- topicSuggestionsList: List of all [Suggestions](./project_overview.md/#suggestion_definition) for voting that belong to the specific topic.<br>
The list should consist of all Data-Model [Section](./data_model.md/#section) instances which their [status](./data_model.md/#status) field is 0 or 4 and that their [topic](./data_model.md/#section-topic) field is the same as specificTopic
### 5.2.3. <a id="sort-by-topic">__Sort by Topic__</a>
Sorting Algorithm that work only on [Suggestions](./project_overview.md/#suggestion_definition) with [specific topic](#specific-topic-suggestions)<br>
and prefers suggestions that are closer to be accepted.
#### 5.2.3.1. variables
  - [specificTopic, topicSuggestionsList](#specific-topic-suggestions-variables)
  - x, y: Suggestion items in topicSuggestionsList for voting
#### 5.2.3.1. logic
- [Specific Topic Suggestions](#specific-topic-suggestions)
- [Most Agreed Upon](#most-agreed-upon)
