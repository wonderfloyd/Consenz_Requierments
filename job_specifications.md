# <a id="top"></a>Consenz new Flows specifications

- [Project State](#project-state)
- [Pages](#pages-description)
  - [Entering Page View](#entering-page-view)
  - [Choose Topics Page View](#choose-topics-page-view)
  - [New Votes Page](#new-votes-page)
  - [Summary Page](#summary-page)
- [Installation Guide](#installation-guide)
- [Workflow](#workflow)
  
## 5. <a id="project-state"></a>Project State
This is a working application, and this assignment is meant to add a few new views described in [Pages](#pages-description). In production the application is connected to Firebase and Firestore for authentication and DB. In order to work on this assignment the app was decoupled from Firebase and is now a client side stand alone working with mock data that is inside the source code directory (i.e `/database`). 
## 3. <a id="pages-descriptions">Pages</a>
This section contains the details and mock ups of the different pages that have to be developed

### 3.1. <a id="entering-page-view">Entering Page View</a>
The goal of the page is to introduce the user to document (see [Document](#document_definition) definition) discussion process,<br>
Explain the document issues and encourage her to sign up and participate.

#### Page Specification:  
__Topics__:  
- Welcome Text  
  - type: Text
  - description: Static text, Edited by Admin user, represents overview. May include discussion preview
- Proceed to choose Topic
  - type: Clickable (Button, Link, ect.)
  - action:  
    - to: [Choose Topics Page View](#choose-topics-page-view)
    - trigger: The user clicks on this element
    - feedback: Page view shifts to Choose Topics Page View
- [_User Menu_](./components.md/#user-menu)
- _Bread Crumbs_


__Mock up__:      

![entering_page_mockup](https://user-images.githubusercontent.com/42510547/70627786-80e8c300-1c2f-11ea-93f3-33f3a6ffe004.png)

### 3.2. <a id="choose-topics-page-view">Choose Topics Page View</a>
This page contains the Topic (see [definition](#definitions)) list for the current Document. The list should be a multiple selection checkbox, where the user can select either none, some, or all of the options.  
The "Proceed to Votes" button leads to the voting page. If no option is selected the user will go through _all_ of the vote Suggestions ([definition](#definitions)) in the Document. Otherwise he'll go through vote suggestions _specific_ to the Topics selected.  

#### Page View Specifications:
__Goal__: Give the user an option to choose the topic that most relevant to her.  
__Variables__:
- topicsSelectedList
  - Type: List
  - Description: List of all Topics selected by the user
  

__Topics__
- Topics list
  - Type: List
  - Description: List of the topics of document. The list will be open when user clicks on the Topics list. The default state display and the first item of the list will be 'All Topics' clickable. The User choose a Topic from Topic list and then clicks the "Proceed to Votes" clickable.
  - Item:
    - Topic_Checkbox
    - Type:
      - String
      - Checkbox
    - Action:
      - Feedback: A Topic is added to the topicsSelectedList list.
- Proceed to Votes
  - Type: Clickable
  - States:
    - topicsSelectedList Not Empty (User selected some Topics)
      - Action:
        - To: New Votes Page with `mode=Specific Topic`
        - Feedback: Page view shifts to New Votes Page with Specific Topic mode.
    - topicSelectedList Empty
      - Action:
        - To: New Votes Page with `mode=All Topic`
        - Feddback: Page view shifts to (All Topics) New Votes Page View.
- _User Menu_
- _Bread Crumbs_

__Mock up 1__:  

![topics_list_mockup2](https://user-images.githubusercontent.com/42510547/70627781-7fb79600-1c2f-11ea-8b7b-912ab69e9484.png)

__Mock up 2__:  

![topics_list_mockup2](https://user-images.githubusercontent.com/12394551/70518786-9c769f80-1b43-11ea-801d-035e9999adf8.png)


### 3.3. <a id="new-votes-page"></a>New Votes Page
This page presents all Suggestions of new issues to vote on one at a time. As mentioned above the Suggestions are displayed in two modes:  
1. __All Topic__ to navigate through _all_ of the Suggestions that are up for vote.
2. __Specific Topic__ to navigate _only_ through Suggestions _specific_ to the CNS_Toopics the user selected in the [previous page](#choose-topics-page-view).  

The Suggestions are sorted by the 'Most Agreed Upon' algorithm or by Topic depending on the [previous page](#choose-topics-page-view)'s selected mode. If the mode is `Specific Topic` Suggestions are sorted by 'Most Agreed Upon' algorithm _within_ each Topic. When the user is finished voting on all open Suggestions he's redirected to the [Summary page](#summary-page).  

This Page includes a suggestion unit, which also has two modes, one for voting on new Sections and one for voting on edited Sections.  
The suggstion unit displays the proposal to be voted upon, and if it is a Suggestion for an edit of the Section than it will also display the current state and changes to be decided on. The proposal Sub-Section will also include the user avatar of the user who created the Suggestion and the publication timestamp.  
The suggestion unit will also include an acceptence threshold, a timer counting down the time left to vote, voting counters, voting buttons and an arguments block.   
Except for the suggestion unit the _New Votes Page_ also includes the Topic title, suggestion navigation buttons, get notifications checkbox, a suggestions progress bar to display how many suggestions are left for voting, and a "back" button to go back to the previous page view.

#### Page View Specifications:
__Goal__: Show New Section suggestion or Edit suggestion that the user hasn't yet voted for, one suggestion in a page view. The user can use navigation buttons to navigate between the suggestions that stand for a vote. The progress bar shows how many suggestions the user haven't voted yet. When the user reach the last suggestion she will be transferred to draft page.  
__Modes__:
- All Topics
  - Goal: The page shows all un-voted Topics suggestions sorted by the 'Most Agreed Upon' algorithm: Suggestion that is closer to be accepted (threshold closest to 0) will be shown first. When the user reach the last suggestion she will be transferred to Summery page view.
  - Sort: Most Agreed Upon
- Specific Topic
  - Goal: The page shows un-voted suggestions that attributed to a specific Topic, sorted by the 'Sort by Topic' algorithm. When the user reach the last suggestion she will be transferred to Summery page view.
  - Filter: Specific Topic Suggestions
  - Sort: Sort by Topic  
    
__Topics__:
- Suggestion Unit
  - modes:
    - New Section
    - Edit
  - items:
    - Current Section
      - Type: String
      - State: On a vote
      - Condition:
        - Mode: Edit Section
    - Section Proposal
      - State: On a vote
      - Items:
        - Section Text
          - Type: String
        - User Avatar
        - Timestamp (published)
    - Threshold
      - Type: Number
    - Timer
      - Type: Countdown Clock
    - Vote Counters
    - Vote Buttons
    - Arguments Block
- Topic Title
  - Type: String
- Suggestion Navigation Buttons
- Get Notification
- Suggestions Progress Bar
- Back Button
  - Description: Change page view back to the last view seen
  - Type: Clickable
- _User Menu_
- _Bread Crumbs_  

__Mock up 1 for New Suggestion__:  

![new_section_vote_mockup1](https://user-images.githubusercontent.com/42510547/70627788-81815980-1c2f-11ea-970e-8a02f6a8940c.png)

__Mock Up 2 for New Suggestion__:  

![new_section_vote_mockup2](https://user-images.githubusercontent.com/12394551/70518785-9c769f80-1b43-11ea-9dc3-cc9796b94ddd.png)

__Mock up 1 for Editing Suggestion__:  

![edit_section_vote_mockup1](https://user-images.githubusercontent.com/42510547/70627782-7fb79600-1c2f-11ea-9978-fcd1a7963d15.png)

__Mock Up 2 for Editing Suggestion__:  

![edit_section_vote_mockup2](https://user-images.githubusercontent.com/12394551/70518788-9c769f80-1b43-11ea-9de3-e8746172a0b0.png)

### 3.4. <a id="summary-page"></a>Summary Page
This page is displayed once the user have finished voting on all Sections open for a vote. It displays a text edited by the Admin and asks the user to register for notifications regarding changes in the Document.

#### Page View Specifications:
__Goal__: Give the user feedback that she finished the task of voting, explain how she could continue participate in the process, encourage her to register for e-mail notifications for her choice.  
__Topics__:
- End Text
  - Type: Text
  - Description: Static text, Edited by Admin user
- Notifications Panel
  - Items:
    - Get Notification (for new document versions)
    - Get Notification (for new edit suggestions)
    - Get Notification (for new section suggestions)
    - Get Notification (for new argument and comment)
- User Menu
- Bread Crumbs  

__Mock Up__:

![summary_page_mockup](https://user-images.githubusercontent.com/42510547/70627790-8219f000-1c2f-11ea-8b98-862679decad7.png)
## 7. <a id="workflow"></a>Workflow  
In this repository you'll find all the information needed to get the job done.  
This file includes an overview of the project and the specifications of the new page views to be developed. Other files in this repository contains the rest of the information you need such as the data model, algorithms and the app's structure and component's heirarchy.  
Beside this repository you should get a link to a private repository containing the app's source code. You'll be the only one working on that fork of the repository, and it'll be merged into the original repository when the job is done.  
Please make sure to make commits regularly and push them to the repository for review.  

## 6. <a id="installation-guide"></a>Installation Guide
- Clone your private repository
- npm install
- npm run serve

[Back to top](#top)
***

Issues
---
- Is there a suggestion draft page? What is Aharon's third New Votes Page mock up for?
