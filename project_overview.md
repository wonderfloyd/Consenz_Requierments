# <a id="top"></a>Consenz new Flows specifications

- [Project Overview](#project-overview)
  - [Sitemap](#sitemap)
- [Definitions](#definitions)
- [Technologies Overview](#technologies-overview)
- [Project State](#project-state)
- [Installation Guide](#installation-guide)
- [Workflow](#workflow)

## 1. <a id="project-overview"></a>Project Overview
A platform for creating agreements.<br>
The platform lets a group of people create a document that reflects an issue they agree upon and discuss the issues that are in disagreement.<br>
The platform allows any group of people at any scale to formulate a text in a single, coherent and clear document in a transparent and democratic way.<br>
The platform enable it through a new kind of Internet discussion.<br>
Instead of spreading across countless responses,<br>
the discussion converges around a collaborative and democratic document by incorporating voting mechanisms with discussion tools.<br>
This allows to distinguish between agreed upon and controversial issues,<br>
and the process has a clear product:<br>
A text that reflects the consent of the participants.
### 1.1. <a id="sitemap">Sitemap</a>
                     Sitemap MISSING!
## 2. <a id="definitions">Definitions</a>
Here you'll find terms and definitions for the app's structure and components.
- <a id="document_definition">__Document__</a>: An object that covers all the relevant issues that the users have discussed, voted and agreed upon.<br>
The Document is dynamic and change according to the actions of the users.
- __Topic__: Sub part of the document.<br>
a document may have multiple Topics.
- <a id="section_definition">__Section__</a>: One issue in the Topic.<br>
a Topic may have multiple Sections.
- __Sub-Section__: Sub part of a Section.<br>
Sections may have multiple Sub-Sections.
- __Version__: Old stats of the Document.<br>
A Document may have multiple Versions.
- __Draft__: A state of a Document in a given time, i.e . the most updated Version of the Document.<br>
A Document can have only one draft.
- <a id="suggestion_definition">__Suggestion__</a>: A Section which is still in discussion and stand for a vote and discussion
- __Edit Suggestion__: A Suggestion that stands to replace another Section.<br>
A Section may have multiple Edit Suggestions.
- <a id="argument_definition">__Argument__</a>: A statement regards a Suggestion.<br>
An Argument can be either pro (for) or con (against) a Suggestion.<br>
A Suggestion may have multiple Arguments
- __Comment__: A note that represent an opinion of a user regarding an Argument.<br>
an Argument may have multiple Comments
- __Discussion__: The sum of all Arguments and Comments regards a Suggestion.
- <a id="vote_definition">__Vote__</a>: A way for the users to express support or objection to a Suggestion without adding text.<br>
A Vote can be pro or con.<br>
A Suggestion may have multiple Votes.
- __User__: A member in the platform that may create a Section, vote in discussion, comment on an argument. ect
- __Discussion Process__: The purposes and intentions of the initiator(s) of the process<br>
that include the issues that stand for discussion and the goals that the created document should fulfill.


## 3. <a id="sitemap">Live Demo</a>
[consenz.co.il](https://consenz.co.il/#/)
- The production demo uses Firebase for server side logic and Database operations (Firestore)<br>
The production code uses javascript vuex-easy-firestore and other firebase libs to sync vuex store models with Firestore
- The code for this requirement was decoupled from firebase code and all data that was originally retrieved from Firestore is now initialized on UI side from mock data objects

## 4. <a id="technologies-overview"></a>Technologies Overview:
- Vue
- Vue - TypesScript
- VueX
- VueX - TypesScript
- Vuetify
  

## 5. <a id="project-state"></a>Project State
This is a working application, and this assignment is meant to add a few new views described in [Pages](#pages-description). In production the application is connected to Firebase and Firestore for authentication and DB. In order to work on this assignment the app was decoupled from Firebase and is now a client side stand alone working with mock data that is inside the source code directory (i.e `/database`). 

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
- Is there a suggestion draft page? What is Aharon's third New Votes Page mock up for?
