# 1. Start in Draft Page
John starts in Draft Page.<br>
The Users tab should show 34 users, since there are 34 users in the [users collection](https://github.com/wonderfloyd/Consenz_TE0/blob/master/database/consenz-test-environment-0/collections/users.json).

![Image20200802113658](https://user-images.githubusercontent.com/12394551/89119167-b2f7af80-d4b4-11ea-9eb1-f8794668e374.png)

# 2. <a id="document-users-list">Document Users List</a>
John press the Users tab.<br>
A [Document Users List](./features_specifications.md#document-users-list) with all users that are registered on the springfield document is presented to John.   
- The Navbar Title should change to 'משתתפים בדיון'
- John should be able to see all 34 users in a list of cards, ordered from latest to earliest.

# 3. <a id="comments-feed">Comments Feed</a>
John press the Back Button and shifts back to [Draft Page](#draft-page).<br>
The [Comments Feed](./features_specifications.md##comments_feed) tab should show 34 comments (there are 8 comments and 26 arguments)<br>
Then he press the Comments Feed tab.<br>
- The Comments Feed page should appear.
- The Navbar Title should change to	'תגובות לסעיפי המסמך'
- John should be able to see all sections with their comments in a list of cards, ordered from latest to earliest.

## 3.1. <a id="clicking-a-comment">Clicking a comment</a>
The first card in the list should be the argument with id="YFFv8YOuWrYX1VJW5THu" since its "created_at" time is the latest from all comments and arguments.<br>

    {
      "id": "YFFv8YOuWrYX1VJW5THu",
      "content": " פגיעה קשה בעיני בחופש הפרט ",
      "created_at": "2020-05-01T20:08:38.642Z",
      ...
      "sectionId": "BnfnRF9chmNaI9DBzNMM"
    },
John press this card and a section single page appears with the section details and the focus on the argument.

Section:

    {
      "id": "BnfnRF9chmNaI9DBzNMM",
      "content": "תושבי העיר ישמרו על אורח חיים בריא, יימנעו מאוכל מהיר ומשתיית אלכוהול. העיר תגביל את פעילות הברים ותוביל קמפיינים לעורר את המודעות לסכנה בשתיית בירה.",
      "created_at": "2019-06-13T07:44:04.202Z",
      ...
      "topic": "בריאות הציבור",
    },

- It should show the same view as if you go in this flow:
> Draft page -> Click on 'חזרה לדיון'<br>
> Topics page -> Click on בריאות הציבור לדיון בנושא<br>
> The argument is the first in the page ('פגיעה קשה בעיני בחופש הפרט')

## 3.2. Adding a comment to the section
John adds a comment to the second argument ("מה עם פתרון ביניים: חינוך כן, הגבלת הברים לא.") of the section<br>
he press the 'להגיב לתגובה' button and adds a comment.<br>
- The comment appears under the argument.

Then John press the back button and moves back to the [Comments Feed](./features_specifications.md##comments_feed) in the draft page.
- The comments counter is updated (incremented by 1)
- The comment he added is now the first in the list

# 4. <a id="restricted-document">Restricted Document</a>
If [Document](../data_model.md#document).allowedUsers exists<br>
then only users defined in this list should be allowed to participate in the document discussion.
- If list does not exist then anyone can view/edit the document. (current behaviour)
- If list exists and current user is not in the allowed users list
  - When user clicks on "go to discussion" button a login pop-up should appear.
    - he: "ההשתתפות מותרת למורשים בלבד. ליצירת קשר עם מנהלי התהליך..."
    - en: "Participation is restricted to allowed users"
  - welcome page and draft will be visible to all.



