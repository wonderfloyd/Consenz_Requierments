# <a id="top"></a>Consenz new Flows specifications

- [Project Overview](#project-overview)
  - [Sitemap](#sitemap)
- [Definitions](#definitions)
- [Pages Description](#pages-description)
  - [Entering Page View](#entering-page-view)
  - [Choose CNS_Topics Page View](#choose-cns-topics-page-view)
  - [New Votes Page](#new-votes-page)
  - [Summary Page](#summary-page)
- [Technologies Overview](#technologies-overview)
- [Project State](#project-state)
- [Installation Guide](#installation-guide)
- [Workflow](#workflow)

## 1. <a id="project-overview"></a>Project Overview
A platform for creating agreements. The platform lets a group of people create a document that reflacts an issue they agree upon and discuss the issues that are in dissagreement. The platform allows any group of people at any scale to formulate a text in a single, coherent and clear document in a transparent and democratic way. The platform enable it through a new kind of Internet discussion. Instead of spreading across countless responses, the discussion converges around a collaborative and democratic document by incorporating voting mechanisms with discussion tools. this allows to distinguish between agreed upon and controversial issues, and the process has a clear product - a text that reflects the consent of the participants.

### 1.1. <a id="sitemap"></a>Sitemap
                     Sitemap MISSING!


## 2. <a id="definitions"></a>Definitions
Here you'll find terms and definitions for the app's structure and components.
- __Document__: An object that covers all the relevant issues that the users have disscused, voted and agreed upon. The Document is dynamic and change accourding to the actions of the users.
- __CNS_Topic__: Sub part of the document. A document may have multiple CNS_Topics.
- __Section__: One issue in the Topic. a Topic may have multiple Sections.
- __Sub-Section__: Sub part of a Section. A Sections may have multiple Sub-Sections.
- __Version__: Old stats of the Document. A Document may have multiple Versions.
- __Draft__: A state of a Document in a given time, i.e . the most updeted Version of the Document. A Document can have only one draft.
- __Suggestion__: A Section which is still in discussion and stand for a vote and disscusion
- __Edit Suggestion__: A Suggestion that stand to replace another Section. A Section may have multiple Edit Suggestions.
- __Argument__: A statement regards a Suggestion. An Argument can be either pro (for) or con (against) a Suggestion. A Suggestion may have multiple Arguments
- __Comment__: A note that represent an opinion of a user regarding an Argument. an Argument may have multiple Comments
- __Discussion__: The sum of all Arguments and Comments regards a Suggestion.
- __Vote__: A way for the users to express support or objection to a Suggestion without adding text. A Vote can be pro or con. A Suggestion may have multiple Votes.
- __User__: A member in the platform that may create a Section, vote in discussion, comment on an argument. ect
- __Discussion Process__: The purposes and intentions of the initiator(s) of the process, that include the issues that stand for discussion and the goals that the document that will be created by using the app should fulfill.

## 3. <a id="pages-descriptions"></a>Pages Description (mock ups)
This section contains the details and mock ups of the different views to be developed. Most of the pages have two different mock ups.

### 3.1. <a id="entering-page-view"></a>Entering Page View
This page welcomes the user into the app in the context of a specific Document (see [definition](#definitions) for Document above), with the user name and an explination of the Document's issues. This page also contains a navigation button,  "Proceed to choose CNS_Topic", to navigate to the [next page](#choose-cns-topics-page-view).  

#### Page View Specifications:
__Goal__: Introduce the user to the app and the process, encourage her to sign up and participate mainly by voting.  
__Topics__:  

- Welcome Text  
  - Type: Text
  - Description: Static text, Edited by Admin user, represents overview. May include discussion preview
- Proceed to choose CNS_Topic
  - Type: Clickable
  - Action:  
    - To: Choose CNS_Topics Page View
    - Feedback: Page view shifts to Choose CNS_Topics Page View
- _User Menu_
- _Bread Crumbs_


__Mock up__:      

![entering_page_mockup](https://user-images.githubusercontent.com/42510547/70627786-80e8c300-1c2f-11ea-93f3-33f3a6ffe004.png)

### 3.2. <a id="choose-cns-topics-page-view"></a>Choose CNS_Topics Page View
This page contains the CNS_Topic (see [definition](#definitions)) list for the current Document. The list should be a multiple selection checkbox, where the user can select either none, some, or all of the options.  
The "Proceed to Votes" button leads to the voting page. If no option is selected the user will go through _all_ of the vote Suggestions ([definition](#definitions)) in the Document. Otherwise he'll go through vote suggestions _specific_ to the CNS_Topics selected.  

#### Page View Specifications:
__Goal__: Give the user an option to choose the topic that most relevant to her.  
__Variables__:
- topicsSelectedList
  - Type: List
  - Description: List of all CNS_Topics selected by the user
  

__Topics__
- CNS_Topics list
  - Type: List
  - Description: List of the topics of document. The list will be open when user clicks on the CNS_Topics list. The default state display and the first item of the list will be 'All Topics' clickable. The User choose a Topic from CNS_Topic list and then clicks the "Proceed to Votes" clickable.
  - Item:
    - CNS_Topic_Checkbox
    - Type:
      - String
      - Checkbox
    - Action:
      - Feedback: A CNS_Topic is added to the topicsSelectedList list.
- Proceed to Votes
  - Type: Clickable
  - States:
    - topicsSelectedList Not Empty (User selected some CNS_Topics)
      - Action:
        - To: New Votes Page with `mode=Specific CNS_Topic`
        - Feedback: Page view shifts to New Votes Page with Specific CNS_Topic mode.
    - topicSelectedList Empty
      - Action:
        - To: New Votes Page with `mode=All CNS_Topic`
        - Feddback: Page view shifts to (All CNS_Topics) New Votes Page View.
- _User Menu_
- _Bread Crumbs_

__Mock up 1__:  

![topics_list_mockup2](https://user-images.githubusercontent.com/42510547/70627781-7fb79600-1c2f-11ea-8b7b-912ab69e9484.png)

__Mock up 2__:  

![topics_list_mockup2](https://user-images.githubusercontent.com/12394551/70518786-9c769f80-1b43-11ea-801d-035e9999adf8.png)


### 3.3. <a id="new-votes-page"></a>New Votes Page
This page presents all Suggestions of new issues to vote on one at a time. As mentioned above the Suggestions are displayed in two modes:  
1. __All CNS_Topic__ to navigate through _all_ of the Suggestions that are up for vote.
2. __Specific CNS_Topic__ to navigate _only_ through Suggestions _specific_ to the CNS_Toopics the user selected in the [previous page](#choose-cns-topics-page-view).  

The Suggestions are sorted by the 'Most Agreed Upon' algorithm or by CNS_Topic depending on the [previous page](#choose-cns-topics-page-view)'s selected mode. If the mode is `Specific CNS_Topic` Suggestions are sorted by 'Most Agreed Upon' algorithm _within_ each CNS_Topic. When the user is finished voting on all open Suggestions he's redirected to the [Summary page](#summary-page).  

This Page includes a suggestion unit, which also has two modes, one for voting on new Sections and one for voting on edited Sections.  
The suggstion unit displays the proposal to be voted upon, and if it is a Suggestion for an edit of the Section than it will also display the current state and changes to be decided on. The proposal Sub-Section will also include the user avatar of the user who created the Suggestion and the publication timestamp.  
The suggestion unit will also include an acceptence threshold, a timer counting down the time left to vote, voting counters, voting buttons and an arguments block.   
Except for the suggestion unit the _New Votes Page_ also includes the CNS_Topic title, suggestion navigation buttons, get notifications checkbox, a suggestions progress bar to display how many suggestions are left for voting, and a "back" button to go back to the previous page view.

#### Page View Specifications:
__Goal__: Show New Section suggestion or Edit suggestion that the user hasn't yet voted for, one suggestion in a page view. The user can use navigation buttons to navigate between the suggestions that stand for a vote. The progress bar shows how many suggestions the user haven't voted yet. When the user reach the last suggestion she will be transferred to draft page.  
__Modes__:
- All CNS_Topics
  - Goal: The page shows all un-voted CNS_Topics suggestions sorted by the 'Most Agreed Upon' algorithm: Suggestion that is closer to be accepted (threshold closest to 0) will be shown first. When the user reach the last suggestion she will be transferred to Summery page view.
  - Sort: Most Agreed Upon
- Specific CNS_Topic
  - Goal: The page shows un-voted suggestions that attributed to a specific CNS_Topic, sorted by the 'Sort by CNS_Topic' algorithm. When the user reach the last suggestion she will be transferred to Summery page view.
  - Filter: Specific CNS_Topic Suggestions
  - Sort: Sort by CNS_Topic  
    
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
- CNS_Topic Title
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


## 4. <a id="technologies-overview"></a>Technologies Overview:
- Vue
- Vue - TypesScript
- VueX
- VueX - TypesScript
- Vuetify
  
## 5. <a id="project-state"></a>Project State
This is a working application, and this assignment is meant to add a few new views described in [Pages Description](#pages-description). In production the application is connected to Firebase and Firestore for authentication and DB. In order to work on this assignment the app was decoupled from Firebase and is now a client side stand alone working with mock data that is inside the source code directory (i.e `/database`). 


## 6. <a id="installation-guide"></a>Installation Guide
- Clone your private repository
- npm install
- npm run serve

## 7. <a id="workflow"></a>Workflow  
In this repository you'll find all the information needed to get the job done.  
This file includes an overview of the project and the specifications of the new page views to be developed. Other files in this repository contains the rest of the information you need such as the data model, algorithms and the app's structure and component's heirarchy.  
Beside this repository you should get a link to a private repository containing the app's source code. You'll be the only one working on that fork of the repository, and it'll be merged into the original repository when the job is done.  
Please make sure to make commits regularly and push them to the repository for review.  

[Back to top](#top)
***

Issues
---
- Where does the user redirects after voting on all issues?  consenz_user_flow_specification.yaml Pages.newVotesPage.goal says draft page, but Pages.newVotesPage.modes says summary page.
- In Specific CNS_Topic mode there are actually two sort algorithms. First sort by CNS_Topic, but then also sort by most agreed upon relative to each CNS_Topic.
- Is there a suggestion draft page? What is Aharon's third New Votes Page mock up for?
