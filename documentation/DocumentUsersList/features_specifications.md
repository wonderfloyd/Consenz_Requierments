- [Document Users List](#document-users-list)
- [Comments Feed](#comments_feed)
- [Versions Page](#versions_page)
- [Restricted Document](#restricted-document)

# 1. <a id="document-users-list">Document Users List</a>
A Page that shows all users that participate in a Document discussion.
## 1.1 Navigation
- In [Draft Page](#draft-page), The user clicks on the participants link.<br> 
  The Document Users List page should appear.

![image](https://user-images.githubusercontent.com/5900841/81645444-42e80900-9432-11ea-8100-260593524db4.png)
TODO Fix Mockup, Main Navbar should not contain the back button.

## 1.2. Topics
### 1.2.1. Navbar Title
The title in the purple navigation panel
- Label: dictionary parameter: **usersListNavbarTitle**
  - he:	'משתתפים בדיון'
  - en:	'Participants'
### 1.2.2. Users List
List of User info cards that are assigned to the document.
#### 1.2.2.1 User Criteria to be in the list
    return all Users that their User.documents contains document.id
#### 1.2.2.2 Order
By User.created_at, From Latest to Earliest.<br>
#### 1.2.2.3 User Card
- User Pic
- User Name
  - Font Size: 18
- User Joining Date
  - Data Model: User.created_at
  - Formatting: Only date, without hour and minutes
  - Text: dictionary parameter: **userJoinedAt**
    - he: '-הצטרפ/ה ב {joinDate}'
    - en: 'Joined At {joinDate}'
### 1.2.3. Navbar Back Button
- Navbar should contain a Back Button
- Clicking on the back button should shift the page back to [Draft Page](#draft-page)

In page: - Keep showing document info counters as at top of draft page. Below users counter add under-line to signal the user which page he sees now.- There should be a line separator between the user cards in the list

# 2. <a id="comments_feed">Comments Feed</a>
A Page that shows all sections that have comments and arguments.

![image](https://user-images.githubusercontent.com/5900841/81648122-d7546a80-9436-11ea-81f4-a4a5606e2c54.png)
## 2.1 Navigation
- In [Draft Page](#draft-page), The user clicks on the comments link.<br> 
  The Comments Feed page should appear.
## 2.2. Topics
### 2.2.1. Navbar Title
The title in the purple navigation panel
- Label: dictionary parameter: **commentsFeedNavbarTitle**
  - he:	'תגובות לסעיפי המסמך'
  - en:	'Comments on Document Sections'
### 2.2.2. Sections with comments List
List of Section cards that have comments and arguments.
#### 2.2.2.1. Filter
Need to iterate over all document comments and arguments,
check the sections they relate to (Comment.sectionId and arguments.sectionID)
and compose a list from all those sections.
#### 2.2.2.2. Order
By Comment.created_at/arguments.created_at, From Latest to Earliest<br>
I.e A section that have a comment or argument that was added lately will show first.

The section should retrieve its latest comment or argument creation time (a section may have multiple comments/arguments)
and in this page is calculated only by the order rule.
#### 2.2.2.3. Section Card
A Card that shows information related to a section. It includes:
- Topic title
- Section content
- Voting buttons
- Comments section
- Add new comment button

The components code and visuals are already implemented in Sections for vote list Page:<br>
https://consenz-te0.netlify.app/#/document/springfield/section?sectionsByStatus=0

**The code should be reused**
##### On Click
a section single page should appear (outside voting flow), and the page view should scroll to the relevant comment

# 3. <a id="versions_page">Versions Page</a>
A Page that shows all Document draft approved sections
## 3.1 Navigation
- In [Draft Page](#draft-page), The user clicks on the versions link.<br> 
  The Versions Page should appear.

Mockup for Versions Page:
![image](https://user-images.githubusercontent.com/5900841/81670107-cbc16d80-944f-11ea-8acf-beb112be520a.png)

## 3.2. Topics
### 3.2.1. Navbar Title
The title in the purple navigation panel
- Label: dictionary parameter: **versionsFeedNavbarTitle**
  - he:	'גרסאות קודמות למסמך'
  - en:	'Previous Document Verstions'

### 3.2.2. Approved Sections List
List of Section that were approved.
- There should be a line separator between the sections in the list
#### 3.2.2.1. Filter
All Sections that:
- Section.documentId is the id of the Draft document
- Section.status is 1 or 5
#### 3.2.2.2. Order
The sections will display by their order in draft,
i.e by their serial number, from first to last.
Serial number does not exist in data-model, need to find a way to take it from draft page:

To section show all versions (i.e, toEdit/parentSection of status 1 or 5) sort by accepted at time, as in history page, But - without voting and comments buttons.

A link for history page - https://consenz-master.netlify.app/#/document/springfield/section?sectionsByStatus=5&index=2&id=Aa8Ns7AxytAwoDnsV7Vd
#### 3.2.2.3. Section Card
A Card that shows information related a section in the list. It includes:
- Topic title
- Section content
- Title: dictionary parameter: **versionSection**
  - he:	'גרסה X לסעיף Y'
  - en:	'Version X to Section Y'
  
X = version number, Y = serial number of section in draft page.
Version number determine by the acceptedAt date of the section, from early to late (already implemented in history page)
##### Section Card Click Operation
When the user clicks on the section contect area<br>
page should shift to section history page.

### 3.2.3. Navbar Back Button
- Navbar should contain a Back Button
- Clicking on the back button should shift the page back to [Draft Page](#draft-page)

# 4. <a id="restricted-document">Restricted Document</a>
If [Document](./data_model.md#document).allowedUsers exists<br>
then only users defined in this list should be allowed to participate in the document discussion.
- If list does not exist then anyone can view/edit the document. (current behaviour)
- If list exists and current user is not in the allowed users list
  - When user clicks on "go to discussion" button a login pop-up should appear.
    - he: "[ההשתתפות מותרת למורשים בלבד. ליצירת קשר עם [מנהלי התהליך<mailto:info@consenz.co.il>"
    - en: "Participation is restricted to allowed users. Click [here]<mailto:info@consenz.co.il> to contact admin"
  - welcome page and draft will be visible to all.

