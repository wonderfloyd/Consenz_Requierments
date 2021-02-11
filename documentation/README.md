- [Project Overview](#project-overview)
- [Data Model](#data-model)
- [Logics](#logics)
- [Features](#features)
- [Road Map](#road-map)

# 1. <a id="project-overview">Project Overview</a>
A platform for creating agreements.<br>
The platform lets a group of people create a document that reflects the issues they agree upon<br>
and discuss the issues that are in disagreement.

The platform allows any group of people at any scale to formulate a text<br>
in a single, coherent and clear document in a transparent and democratic way.<br>
The platform enable it through a new kind of Internet discussion.<br>
Instead of spreading across countless responses,<br>
the discussion converges around a collaborative and democratic document<br>
by incorporating voting mechanisms with discussion tools.<br>
This allows to distinguish between agreed upon and controversial issues,<br>
and the process has a clear product: A text that reflects the consent of the participants.
## 1.1. <a id="technologies-overview"></a>Technologies
- Vue - TypesScript
- VueX - TypesScript
- Vuetify
## 1.2. <a id="definitions">Definitions</a>
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
- <a id="draft_definition">__Draft__</a>: A state of a Document in a given time, i.e . the most updated Version of the Document.<br>
A Document can have only one draft.
- <a id="suggestion_definition">__Suggestion__</a>: A Section which is still in discussion and stand for a vote and discussion
- __Edit Suggestion__: A Suggestion that stands to replace another Section.<br>
A Section may have multiple Edit Suggestions.
- __Comment__: A note that represent an opinion of a user regarding an Suggestion.<br>
an Suggestion may have multiple Comments
- __Comment on a Comment__: A note that represent an opinion of a user regarding a Comment.<br>
a Comment may have multiple Comment on Comments
- __Discussion__: The sum of all Comments regards a Suggestion.
- <a id="vote_definition">__Vote__</a>: A way for the users to express support or objection to a Suggestion without adding text.<br>
A Vote can be pro or con.<br>
A Suggestion may have multiple Votes.
- <a id="threshold_definition">__Document Threshold__</a>: A number that represent how much support needed to approve a new suggestion. The threshold is always a percentage of the total sum of users in a document at given time.  
- <a id="threshold_definition">__Suggestion Threshold__</a>: A nember that calculate Document Threshold - Pro Voters{length} + Con Voters{length}. When Suggestion Threshold reach 0 Section status changes to "approved".  
- __User__: A member in the platform that may create a Section, vote in discussion, comment, ect
- __Discussion Process__: The purposes and intentions of the initiator(s) of the process<br>
that include the issues that stand for discussion and the goals that the created document should fulfill.
# <a id="data-model">Data Model</a>
- [User](./data_model.md#user)
- [Document](./data_model.md#document)
- [Section](./data_model.md#section)
- [Argument](./data_model.md#argument)
- [Comment](./data_model.md#comment)
- [ChangeEvent](./data_model.md#changeEvent)
# <a id="logics">Logics</a>
- [Suggestion Accepted](./logics.md#suggestionAccepted)
- [Section Changed](./logics.md#sectionchanged)
- [Section Removed](./logics.md#sectionRemoved)
- [Consensus Meter](./logics.md#consensusMeter)
- [Most Agreed Upon](./logics.md#most-agreed-upon)
- [User Connected Rule](./logics.md#user-connected-rule)
# <a id="features">Features</a>
- [Voting Page](VotingPage/README.md)
# <a id="road-map">Road Map</a>
- [Users List](DocumentUsersList/README.md)
- [Navigation Tree](NavigationTree/README.md)
- [Update Bell and Notifications](UpdateBell/README.md)
