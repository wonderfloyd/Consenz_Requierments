# <a id="top">Consenz Update Bell & Activity Feed specifications</a>
The details and mock ups of the different features that have to be developed

- [Update Bell](#update-bell)
- [Event Activity Page](#notifications-activity-page)
- [Event Types](#event-types)
- [Browser Push and Email Notifications](#browser-push-email-notifications)
- [Unsubscribe](#unsubscribe)
- [Pending Notifications Option](#pending_notifications_option)
- [Navigation Bar](#navigation_bar)

# 1. <a id="update-bell">Update Bell</a>
The goal is to inform the user about new changes in the document<br>
and give him a quick access to the Activity Page view with all recent changes

![Image20200708132620](https://user-images.githubusercontent.com/5900841/88152804-3be92e00-cc0d-11ea-9d35-1c5e90bb4a37.png)

## 1.1. Visual
- Location: Navigation Bar
- Image: Bell with a Counter at the left-top corner
## 1.2. Bell Counter
The amount of new notifications since the last time the user visited the [Notification Activity Page](#notifications-activity-page).
- After the user visits the activity page, the counter is reset to 0 for the user.
- for users that are not logged in, the counter will show the amount of all activity of the document.
## 1.3. Click Action
Clicking on the bell leads to the [Notification Activity Page](#notifications-activity-page).
# 2. <a id="notifications-activity-page">Event Activity Page</a>
The goal of this page is to show notifications of all recent change events in the document<br>
and let the user click on an event and see the its details.
![86748201-f6413880-c044-11ea-8a82-ae5a718300f3](https://user-images.githubusercontent.com/12394551/86937632-27566180-c148-11ea-8b95-de0e7145a4de.png)

## 2.1. Page Title
- Dictionary parameter: **activityPageTitle**
  - he: 'פעילות אחרונה בדיון'
  - en: 'Last Activity'
## 2.2. Events Feed
List of all document events. Each is represented with an Event Item Card consisting of the following:
### 2.2.1. Reacting User
[User Avatar](#user-avatar) (profile pic + user name) of the user that created the event 
### 2.2.2. Created At
The value is according to the event:
- New item added: ([argument](../data_model.md/#argument) / [comment](../data_model.md/#comment) / [section](../data_model.md/#section)).created_at
- Voting event: [section](../data_model.md/#section).updated_at
- Edit/New Suggestion Accepted event: [section](../data_model.md/#section).acceptedAt
### 2.2.3. Event Description Prefix
Prefix of event description based on the Notification type:
- [user voted for suggestion](#user-voted-for-suggestion-notification-text)
- [user added new argument](#user-added-new-argument-notification-text)
- [user added new comment](#user-added-new-comment-notification-text)
- [user added new section suggestion](#user-added-new-section-suggestion-notification-text)
- [user added new edit section suggestion](#user-added-new-edit-section-suggestion-notification-text)
- [new section suggestion was accepted](#new-section-suggestion-was-accepted-notification-text)
- [new edit section suggestion was accepted](#new-edit-section-suggestion-was-accepted-notification-text)
### 2.2.4. Read More Clickable
Clickable link that that allow the user to dive into the details of the change event.
- Label
  - he: 'קרא עוד'
  - eb: 'Read more'
- On Click: Show in activity page the full text of the section/argument/comment, without loading a new page.
### 2.2.5. Trash icon
  - Trash icon will displayed only on items that their reacting User is the logged in user (user can only delete his own activity event).
  - Clicking on the trash icon opens a popup to approve deletion.
    - he: 'למחוק פריט זה?'
      - yes: 'כן'
      - no: 'לא'
    - en: 'Delete this item?'
      - yes: 'Yes'
      - no: 'No'
  - If user click 'yes' the item will be removed from activity page display for all users. 
## 2.3. Sorting Dropdown
Sorting options for the events feed
### Options:
- created at: from late to early
  > by default
- event of the user - the reacting user of the event is the user that logged in.
   
![notificationsSorting](https://user-images.githubusercontent.com/12394551/87117850-48bb6880-c282-11ea-9c2d-ed1bde984e38.png)
# 3. <a id="event-types">Event Types</a>
## 3.1. User Voted For Suggestion
### 3.1.1. Trigger Flow:
- Welcome Page [(Entering Page View)](../VotingPage/pages_specifications.md/#entering-page-view) -> Proceed button click
- [Choose Topics Page](../VotingPage/pages_specifications.md/#choose-topics-page-view) -> Topic To Discussion button click
- Voting Page ([New Votes Page](../VotingPage/pages_specifications.md/#new-votes-page)) -> Vote Pro/Con button click
### 3.1.2. Data Model
When a user votes on a [section](../data_model.md/#section),<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: [section](../data_model.md/#section).updated_at
- type: "User Voted For Suggestion"
- subType: "voted pro" / "voted con"
- itemId: [section](../data_model.md/#section).id
- creator: Voting [User](../data_model.md/#user).id
### 3.1.3. <a id="user-voted-for-suggestion-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<suggestionTextPrefix>: <userName> סעיף של <eventType>
  - en:

        <eventType> on suggestion of <userName>: <suggestionTextPrefix>...
- eventType: [changeEvent](../data_model.md/#changeEvent).subType
  - voted pro
    - he: 'תמכ/ה ב'
    - en: 'voted pro'
  - voted con
    - he: 'הסתייג/ה מה'
    - en: 'voted con'
- userName: [changeEvent](../data_model.md/#changeEvent).creator (Voting User).
- suggestionTextPrefix: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of section data model.

## 3.2. User Added New Argument
### 3.2.1. Trigger Flow:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Add New Argument button click (see screenshot)
    Voting Page, New Argumant Text Box -> Enter Text and Publish button click
    
![image](https://user-images.githubusercontent.com/5900841/89333620-e77a8f80-d69d-11ea-8ca0-16a912305488.png)

### 3.2.2. Data Model
When a user adds an argument to a suggestion [section](../data_model.md/#section),<br>
For each of the section registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: [argument](../data_model.md/#argument).created_at
- type: "User Added New Argument"
- itemId: [argument](../data_model.md/#argument).id
- creator: [User](../data_model.md/#user).id of Logged user that added the argument
- registeredUser: id of registeredUser
### 3.2.3. <a id="user-added-new-argument-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<argumentTextPrefix>: <userName> הגיב/ה לסעיף של
  - en:

        added new argument on suggestion of <userName>: <argumentTextPrefix>...
- userName: [changeEvent](../data_model.md/#changeEvent).creator (Argumentative User).
- argumentTextPrefix: [argument](../data_model.md/#argument)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of argument data model.

## 3.3. User Added New Comment
A user adds an comment to a [section](../data_model.md/#section) or an [argument](../data_model.md/#argument)
### 3.3.1. Trigger Flow:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Add New Comment button click
    Voting Page, Add New comment Text Box -> Publish button click
    
### 3.3.2. Data Model
For each of the item(section or argument) registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent)
- created_at: [comment](../data_model.md/#comment).created_at
- type: "User Added New Comment"
- subType: "Section" / "Argument"
- itemId: [comment](../data_model.md/#comment).id
- creator: [User](../data_model.md/#user).id of Logged user that added the comment
- registeredUser: id of registeredUser
### 3.3.3. <a id="user-added-new-comment-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<commentTextPrefix>: <userName> של <item>הגיב/ה ל
  - en:

        commented on <item> of <userName>: <commentTextPrefix>...
- item: [changeEvent](../data_model.md/#changeEvent).subType -  Section or Argument.
  - Section
    - he: 'סעיף'
    - en: 'section'
  - Argument
    - he: 'תגובה'
    - en: 'argument'
- userName: [changeEvent](../data_model.md/#changeEvent).creator (Commenting User).
- commentTextPrefix: [comment](../data_model.md/#comment)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of comment data model.

## 3.4. User Added New Section Suggestion
A user added a Suggestion for a new [Section](../data_model.md/#section)
### 3.4.1. Trigger Flow:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Last Vote Page 
    Last Vote Page -> Add New Section button click
    Add New Section page -> Publilsh button click
or:

    Welcome Page (Entering Page View) / Summary Page -> Go to Draft button click
    Draft Page -> Add New Section button click
    Add New Section page -> Publilsh button click
### 3.4.2. Data Model
For each of the document registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: New [Suggestion](../data_model.md/#section).created_at
- type: "User Added New Section Suggestion"
- itemId: New [suggestion](../data_model.md/#section).id
- creator: [User](../data_model.md/#user).id of Logged user that added the suggestion
- registeredUser: id of registeredUser
### 3.4.3. <a id="user-added-new-section-suggestion-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<sectionTextPrefix>: <topic> פרסמ/ה הצעה לסעיף חדש בנושא
  - en:

        Added a new section suggestion on <topic> topic: <sectionTextPrefix>...
- topic: [suggestion](../data_model.md/#section).topic field
- sectionTextPrefix: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of the new suggestion.

## 3.5. User Added New Edit Section Suggestion
A user added a new Edit Section Suggestion to replace existing [Section](../data_model.md/#section)
### 3.5.1. Trigger Flow:
    First scenario:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Edit Section Suggestions tab title click
    Voting Page, Edit Section Suggestions tab mode -> Add New Edit Suggestion button click
    Second scenario:: 
    Voting Page (New Votes Page) -> Vote Con Button click
    Voting Page (New Votes Page) -> Add New Edit Suggestion button click
    Voting Page, New Edit Suggestion Text Box -> Publish button click
   
For each of the section registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: New Edit [Suggestion](../data_model.md/#section).created_at
- type: "User Added New Edit Section Suggestion"
- itemId: New [suggestion](../data_model.md/#section).id
- creator: [User](../data_model.md/#user).id of Logged user that added the suggestion
- registeredUser: id of registeredUser
### 3.5.3. <a id="user-added-new-edit-section-suggestion-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<suggestionTextPrefix>: <topic> פרסמ/ה הצעה לשינוי סעיף בנושא
  - en:

        Added a new edit section suggestion on <topic> topic: <suggestionTextPrefix>...
- topic: [suggestion](../data_model.md/#section).topic field
- suggestionTextPrefix: [suggestion](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of the new suggestion.

## 3.6. New Section Suggestion Was Accepted
A [Section](../data_model.md/#section) Suggestion was accepted due to user pro votes.
### 3.6.1. Trigger Flow:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Vote Pro button click
    Threshold was 1, and after this vote reach 0 and an acceptedAt field wes added to section data model (see screenshot for example)
    ![image](https://user-images.githubusercontent.com/5900841/89334615-7b992680-d69f-11ea-997d-f035d72ac9aa.png)

### 3.6.2. Data Model
For each of the section and document registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: [section](../data_model.md/#section).acceptedAt
- type: "New Section Suggestion Was Accepted"
- itemId: (../The accepted [section](../data_model.md/#section).id
- creator: [User](../data_model.md/#user).id of User that created the suggestion. ([section](../data_model.mdedit /#section).owner)
- registeredUser: id of registeredUser
### 3.6.3. <a id="new-section-suggestion-was-acceted">
- Format
  - he:

        ...<suggestionTextPrefix>: <userName> התקבלה הצעה לסעיף חדש של
  - en:

        A new section suggestion of <userName> was accepted: <suggestionTextPrefix>...
- userName: [changeEvent](../data_model.md/#changeEvent).creator (User that created the suggestion).
- suggestionTextPrefix: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of section data model.
- userName: [changeEvent](../data_model.md/#changeEvent).creator (User that created the suggestion).
- suggestionTextPrefix: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of section data model.

A [Section](../data_model.md/#section) Suggestion was accepted due to user pro votes.
## 3.7. New Edit Section Suggestion Was Accepted
An Edit [Section](../data_model.md/#section) Suggestion was accepted due to user pro votes.
### 3.7.1. Trigger Flow:
    First scenario:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Vote Pro button click
    Threshold reach 0 and an acceptedAt field wes added to section data model)
    Second scenario:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Edit Section Suggestions tab title click
    Edit Section Suggestion vote Pro button click
    Threshold was 1, and after this vote reach 0 and an acceptedAt field wes added to section data model (see screenshot for example)
    ![image](https://user-images.githubusercontent.com/5900841/89335011-1a258780-d6a0-11ea-8cc7-3b4a3aec1a22.png)

For each of the section registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: edit suggestion [section](../data_model.md/#section).acceptedAt
- type: "New Edit Section Suggestion Was Accepted"
- itemId: The accepted edit suggestion [section](../data_model.md/#section).id
- creator: [User](../data_model.md/#user).id of User that created the edit suggestion. ([section](../data_model.md/#section).owner)
- registeredUser: id of registeredUser
### 3.7.3. <a id="new-edit-section-suggestion-was-accepted-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<suggestionTextPrefix> :לעריכת סעיף <userName> התקבלה הצעה של
  - en:

        An edit section suggestion of <userName> was accepted: <suggestionTextPrefix>...
- userName: [changeEvent](../data_model.md/#changeEvent).creator (User that created the suggestion).
- suggestionTextPrefix: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of section data model.

# 4. <a id="browser-push-email-notifications">Browser Push and Email Notifications</a>
## 4.1. Section Notifications
User subscribes for a section change notification.
### 4.1.1. Subscription Trigger
- The user is owner (user ID is in "owner" field of the section data model).
- User mark notification checkbox of the section.
- User publish an argument on the section.
- User publish an edit suggestion for the section.
### 4.1.2. Data-Model
- Add section id as "true" to "notifications" -> "suggestionsNotifications" of user data model) (see screenshot for example)

![image](https://user-images.githubusercontent.com/5900841/89335396-a33cbe80-d6a0-11ea-9dd6-4f3f0d9a177c.png)

### 4.1.3. Notification Trigger and Message Text
- The section status changed to "approved"
  - en
    - Title: "A suggestion that you follow got accepted"
    - Body: "A suggestion that you follow got accepted and the document "[document Title]" had been updated accordingly.<br>The section that was added: "[section content]"<br>To watch current draft click here <+link to draft>"
  - he
    - Title: "הצעה לסעיף שעקבת אחריו התקבלה"'
    - Body: הצעה לסעיף שעקבת אחריה התקבלה, והמסמך "[document Title]" עודכן בהתאם<br>נוסח ההצעה:"[section content]"<br>לצפייה בטיוטת המסמך העדכנית לחצו כאן<+link to draft>"
- A new edit section is created<br>
  (a new field added in section data model "toEdit" field).
  - en
    - Title: "A new edit suggestion for section that you follow"
    - Body: "[section owner user name] published a new edit suggestion for a section that you follow.<br>The original text: [parent section content]<br>The edit suggestion: [edit section content].<br>To watch, comment or vote for the new suggestion<br>click here [link to section single page]"
  - he
    - Title: "פורסמה הצעה לשינוי סעיף שעקבת אחריו"
    - Body: "[section owner user name] פרסמ/ה הצעה לשינוי סעיף.  נוסח הסעיף המקורי: '[parent section content]'<br>    נוסח הצעת העריכה:  '[section content]'<br>  לתמיכה, הסתייגות או תגובה להצעה לחצו כאן [link to section single page]"  
- A new argument is created<br>
(an argument that the section id is in argument data model "sectionId" field).
  - en
    - Title: "A new comment in a discussion that you follow:
    - Body: "[comment / argument owner User Name] has publish a new comment:'[argument / comment content]'<br>To see new comment click here [+link to section page, view will scroll to the new argument/comment]"
  - he
    - Title: "תגובה חדשה לדיון בהשתתפותך:
    - Body: "[comment / argument owner User Name] הגיב/ה בדיון שהשתתפת בו: '[argument / comment content]'<br>  לדיון [+link to section page, view will scroll to the new argument/comment]"
- A new comment on an argument that the user comment on is created<br>
  (a comment that the section id is in comment data model "sectionId" field).
  - en
    - Title: "A new comment in a discussion that you follow:
    - Body: "[comment owner User Name] has publish a new comment:'[comment content]'<br>To see new comment click here [+link to section page, view will scroll to the new comment]"
  - he
    - Title: "תגובה חדשה לדיון בהשתתפותך:
    - Body: "[comment owner User Name] הגיב/ה בדיון שהשתתפת בו: '[comment content]'<br>  לדיון [+link to section page, view will scroll to the new comment]"
- A new comment on an argument that the user is it's owner is created<br>
  (a comment that it's argumentId field is an argument that the user is it's owner)
  - en
    - Title: "A new comment in a discussion that you follow:
    - Body: "[comment owner User Name] has publish a new comment:'[comment content]'<br>To see new comment click here [+link to section page, view will scroll to the new comment]"
  - he
    - Title: "תגובה חדשה לדיון בהשתתפותך:
    - Body: "[comment owner User Name] הגיב/ה בדיון שהשתתפת בו: '[comment content]'<br>  לדיון [+link to section page, view will scroll to the new comment]"

## 4.2. Document Notifications
User subscribes for a document change notification.

### 4.2.1. Subscription Configuration
- The user will get notification according to his subscription to notifications of the document.<br>
i.e. if the notification user configuraiton flag is set to true
- Data-Model Flags path: [User].updateObject.notifications.documents.[documentId]

| Event | Flag Parameter | 
| --- | :--- |
| New Argument is Added | newArgumentOrCommentNotification
| Section Status Changed to Approved | newDocumentVersionNotification
| New Edit Section is Created | newEditSuggestionNotification
| New Section is Created | newSectionSuggestionNotification

### 4.2.2. Action:
send an email/push notification

## 4.3. Push Notification Action
### 4.3.1. Offline Mode
Send an Email with Notification text and control buttons
- use Firebase to send mail
- Try to use code from functions/src/api/mailNotifications.ts
### 4.3.2. Web Mode
Use browser option (firefox and chrome) push notifications to show pop-up Window with Notification text and control buttons

# 5. <a id="unsubscribe">Unsubscribe</a>
## 5.1. Unsubscription method
2 unsubscribe buttons in all mail/push notifications
- Will show at the bottom of page
- on minimal font size - 8 or 9.
### Section unsubscribe:
Text on button:
- en : "Unsubscribe from updates of this section"
- he : "אל תשלחו לי עוד עדכונים מדיון על סעיף זה"
If user clicks section unsubscribe button, open section page, and remove check from notifications checkbox.
Text on button:
- he: "לבקשתך, לא יישלחו עוד עדכונים"
- en: "Unsubscribe from all updates"
### General unsubscribe:
Text on button:
- en: "Unsubscribe from all updates"
- he: "הסרה מרשימת התפוצה"
If user clicks section unsubscribe button, open section page, and remove check from notifications checkbox.
For document unsubscribe button, open summary page, and remove check from all notifications, and show 
Pop up wih text:
- en: "You have been unsubscribed"
- he: "לבקשתך, לא יישלחו עוד עדכונים"

# 6. <a id="pending_notifications_option">Pending Notifications Option</a>
With this option notifications are first sent to admin user in order to approve sending to all users.
## 6.1. Data Model
Add to [Document](../data_model.md/#document) a new field - "pendingNotification"
- Type: Boolean
- If true then all notifications will be sent first to admin
   - Email is sent to all editors of the document (User[editor].email)
## 6.2. Mail
- Notification Text
- "Send" button - when the admin user clicks the Send button it sends notifications to all users.

# 7. <a id="navigation_bar">Navigation Bar</a>
- [User Menu](../VotingPage/pages_specifications.md#user-menu)
- Document Title
  - Taken from [Document](../data_model.md#document).title
- [Updates Bell](../UpdateBelll/features_specifications.md)
- User Indication (Profile Pic or Sign-in button
  - User Signed-in: Show Profile Pifield/textc
    - Taken from [User](../data_model.md#user).photoURfield/textL
    - Clicking the profile pic opens sign-out optiofield/textn
      - he: "התנתקותfield/text"
      - en: "Sign outfield/text"
  - User is not Signed-in: Sign-in Buttofield/textn
    - he: "התחברות", en: "Sign infield/text"
    - Clicking the Sign-in button opens login pop upfield/text.field/text
      
## 7.1. Navigation Sub Panel
Below the navigation panel there is a transparent sub panel that shows the page name and the back button.
- Page Name - by field/text (as in current header panel of pages)
  - Welcome page: welcomeTitle (welcomeTitle taken from Document.documentWelcome.welcomeTitle)
  - Choose Topics page: document.documentTopics.documentTopicsTitle
  - Vote page / Single suggestion page
    - he: "דיון בהצעה"
    - en: "Suggestion Discussion"
  - Draft page
    - he: "טיוטת המסמך"
    - en: "Current Draft"
  - Edit suggestion feed page
    - he: "הצעות לעריכת סעיף X"
    - en: "Edit Suggestion for section X"
  - History page
    - he: "היסטוריית סעיף X"
    - en:"Section X History"
- Back Button
  
![image](https://user-images.githubusercontent.com/5900841/86739067-45d03600-c03e-11ea-8d6a-b18946728996.png)
