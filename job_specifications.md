# Consenz new Flows specifications
## 1. Project Overview
A platform for creating agreements. The platform lets a group of people create a document that reflacts an issue they agree upon and discuss the issues that are in dissagreement. The platform allows any group of people at any scale to formulate a text in a single, coherent and clear document in a transparent and democratic way. The platform enable it through a new kind of Internet discussion. Instead of spreading across countless responses, the discussion converges around a collaborative and democratic document by incorporating voting mechanisms with discussion tools. this allows to distinguish between agreed upon and controversial issues, and the process has a clear product - a text that reflects the consent of the participants.

### 1.1. Sitemap
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

## 3. Pages Description (mock ups)
This section contains the details and mock ups of the different views to be developed. Most of the pages have two different mock ups.

### 3.1. Entering Page View
This page welcomes the user into the app in the context of a specific Document (see [definition](#definitions) for Document above), with the user name and an explination of the Document's issues. This page also contains a navigation button to the [next page](#132).  

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


Mock up:    

          MOCKUP MISSING!

### 3.2. <a id="132"></a>Choose CNS_Topics Page View
This page contains the CNS_Topic (see [definition](#definitions)) list for the current Document. The list should be a multiple selection checkbox, where the user can select either none, some, or all of the options.  
The button leads to the voting page. If no option is selected the user will go through _all_ of the vote Suggestions ([definition](#definitions)) in the Document. Otherwise he'll go through vote suggestions _specific_ to the CNS_Topics selected.  

#### Page View Specifications:
__Goal__: Give the user an option to choose the topic that most relevant to her.  
__Variables__:
- topicsSelectedList
  - Type: List
  - Description: List of all CNS_Topics selected by the user
  

__Topics__
- CNS_Topics list
  - Type: List
  - Description: List of the topics of document. The list will be open when user clicks on the CNS_Topics list. The default state display and the first item of the list will be 'All Topics' clickable The User choose a Topic from CNS_Topic list and then clicks the "Proceed to Votes" clickable.
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

Mock up 1:

              MISSING!

Mock up 2:
![topics_list_mockup](https://user-images.githubusercontent.com/12394551/70518786-9c769f80-1b43-11ea-801d-035e9999adf8.png)


### 3.3. New Votes Page
This page presents all Suggestions of new issues to vote on one at a time. As mentioned above the Suggestions are displayed in two modes:  
1. __All CNS_Topic__ to navigate through _all_ of the Suggestions that are up for vote.
2. __Specific CNS_Topic__ to navigate _only_ through Suggestions _specific_ to the CNS_Toopics the user selected in the [previous page](#132).  

The Suggestions are sorted by the 'Most Agreed Upon' algorithm or by CNS_Topic depending on the [previous page](#132)'s selected state. If the mode is `Specific CNS_Topic` Suggestions are sorted by 'Most Agreed Upon' algorithm within each CNS_Topic.  

The Page includes a suggestion unit, which also has two modes, one for voting on new Sections and for voting on edited Sections.  
The suggstion unit displays the proposal to be voted upon, and if it is a Suggestion for an edit of the Section than it will also display the current state and change to be decided on. The proposal Sub-Section will also include the user avatar of the user who created the Suggestion and the publication timestamp.  
The suggestion unit will also include an acceptence threshold, a timer counting down the time left to vote, voting counters, voting buttons and an arguments block.   
Except for the suggestion unit the _New Votes Page_ also includes the CNS_Topic title, suggestion navigation buttons, get notification checkbox, a suggestions progress bar to display how many suggtions are left for voting, and a back button to go back to the previous pagw view.

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

Mock up 1:

            MISSING!

Mock Up 2 for New Suggestion:
![new_section_vote_mockup2](https://user-images.githubusercontent.com/12394551/70518785-9c769f80-1b43-11ea-9dc3-cc9796b94ddd.png)

Mock Up 2 for Editing Suggestion:
![edit_section_vote_mockup2](https://user-images.githubusercontent.com/12394551/70518788-9c769f80-1b43-11ea-9de3-e8746172a0b0.png)

### 3.4. Summary Page

## 4. Technologies Used:
  - Vue
  - Vue - TypesScript
  - VueX
  - VueX - TypesScript
  - Vuetify
  
## 5. Project State


## 6. Installation Guide
  - Clone your private repository
  - npm install
  - npm run serve

## 7. Workflow  


***

Issues
---
- Where does the user redirects after voting on all issues?  consenz_user_flow_specification.yaml Pages.newVotesPage.goal says draft page, but Pages.newVotesPage.modes says summary page.
- In Specific CNS_Topic mode there are actually two sort algorithms. First sort by CNS_Topic, but then also sort by most agreed upon relative to each CNS_Topic.
