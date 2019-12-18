# <a id="top"></a> Data Model
This is the Applications Data Model. It consist of four objects:  
- [User](#user)
- [Document](#document)
- [Section](#section)
- [Argument](#argument)

## <a id="user">User</a>
- displayName: String
- created_at: Date
- documents:<br>
  all the documents that the user assign to
  - ref: Document
- notifications:
  - isOn: Boolean<br>
    determine if mail notifications will be sent to he user (will be on "false" if user unsubscribed)
  - mailAddress: String<br>
    email address of the user, for sending notifications and for identification in log in.
- photoURL: String<br>
  URL link to profile photo of user
## <a id="document">Document</a>
- about: String<br>
  Static text to descibe the porpuse of the discussion.
  Can be edited for now only from firebase, in th future will be edited from admin interface.
- conditionalSupport: Boolean
- cons:
  - ref: Argument
- pros:
  - ref: Argument
- consensus_meter: String<br>
  A number between 0 to 1 that reflect the level of support that the users gave to the current draft by voting to the sections that has been accepted.
  a consensus_meter of a document in an average of all "consenuses" (see next) and is updated every time a new consensus_meter is generated.
- consensuses:
  - Number
- createdAt: Date<br>
  An array of the specifics consensus_meters for every accepted section.
  When the delta pro-voters of a suggestions reach it's threshold (see next)
  a new consensus_meter is generated according to this formula:
  new consensus_meter = (1 - (con votes / pro votes)) * ((pro voters) / users of draft)
- divisionOfTopics: Boolean<br>
  Determine if the document draft can be divided to different topics.
- documentTopics:
  - String
- editors:
  - ref: User<br>
    Users that have admin authorization and can accept or reject suggestion by choosing to use their veto right.
    In UI editors user will see, below voting buttons, a checkbox "use editor privilege".
    If this checkbox is marked then editor user vote will determine the suggestion fate:
    If voted pro the suggestion will be accepted, if voted con it will be denied,
    Without considering the threshold, other voting and timer.
- sendNotifications: Boolean<br>
  Determine if mail notifications will be sent to all users of the document or not.
- threshold: Number<br>
  A number of pro voters minus con voters that require for accepting suggestion.
  The threshold of all existing and new suggestions is set every time that a suggestions is accepted
  and a new consensus_meter is generated.
  Threshold = consensus_meter * number of users of the document
- timer: Number<br>
  A time that set the deadline of suggestions from it's ceatedDate.
- title: String<br>
  The name of the document.
- updated_at: Date
- updated_by:
  - ref: User
- voteOnDocument: Boolean<br>
  A way for users to vote pro or con the current document draft as a general,
  without voting for a specific suggestion.
## <a id="section">Section</a>
- <a id="section-topic">topic</a>: String
- content: String
- created_by:
  - ref: User<br>
  The user that publish the first suggestion of the section
- owner:
  - ref: User
- updated_by:
  - ref: User
- documentId:
  - ref: Document
- parentSectionId:
  - ref: Section<br>
  If the section is an edit suggestion,
  when accepted it's text will replace the section that parentSectionId refer to.
- accepted_at: Date
- created_at: Date
- deadline: Date
- updated_at: Date
- cons:
  - ref: Argument<br>
  argument can be pro or con.
  when user publish new argument his vote will be considered according to the argument mode.
  here are argument that connected to the votes.
- pros:
  - ref: Argument
- contentHtml: String
- deleted:
- edited:<br>
  previous versions of the section.
  will be shown in the section history page view.
- <a id="status">status</a>: Number<br>
  The voting status of the Suggestion<br>
  0 = in a vote<br>
  1 = accepted<br>
  2 = declined<br>
  3 = deleted (by voting)<br>
  4 = edit section suggestion on a vote<br>
  5 = edit section suggestion accepted<br>
  6 = edit section suggestion declined
- threshold: Number<br>
A number of pro voters minus con voters that require for accepting suggestion.<br>
The threshold of all existing and new suggestions<br>
is set every time that a suggestions is accepted and a new consensus_meter is generated.<br>
Threshold = consensus_meter * number of users of the document
- timer: Number
- tag: String
- toDelete:<br>
If there is a suggestion to delete this section, its id will be shown here.
- <a id="to-edit">toEdit</a>: List<br>
If there is a suggestions to edit this section, its ids will be shown here.
## <a id="argument">Argument</a>
- content: String
  - convinced:
    - ref: User<br>
    "convinced" button is a way for users to express support of other users argument.
    if user push "convinced" button of argument his vote will be the same as the argument mode - pro/con
  - created_at: Date
  - created_by:
    - ref: User
  - documentId:
    - ref: Document
  - owner:
    - ref: User
  - sectionId:
    - ref: Section
  - type: Boolean
  - updated_at: Date
  - updated_by:
    - ref: User
