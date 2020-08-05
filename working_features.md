
# <a id="top">Working Features</a>
Exiting Features, should work as described, straight after installation.

# 0. <a id="Side-Menu">Side-Menu</a>

Note: appear at all pages.

## Actions:

### 0.1 Login / Sign out
### 0.2 Go to "About Consenz" page
### 0.3 Go to "About Document" page
### 0.4 Go to ["Draft"](#draft) page

![image](https://user-images.githubusercontent.com/5900841/89282163-cee58780-d653-11ea-98ea-1f002a5485ed.png)

# 1. <a id="welcome">Welcome page</a>

## Actions:

### 1.0 Open [Side-Menu](#Side-Menu)
### 1.1 Go to [Draft](#draft) button
### 1.2 Go to [Choose-Topics button](#Choose-Topics)

![image](https://user-images.githubusercontent.com/5900841/89281968-8201b100-d653-11ea-86aa-299d96d4eb2d.png)

# 2. <a id="choose-topics">Choose-Topics page</a>

## Actions:

### 2.0 Open [Side-Menu](#Side-Menu)
### 2.1 Breadcrumbs - go to [Welcome](#welcome) page
### 2.2 Breadcrumbs - go to [Draft](#draft) page
### 2.3 Go to Topic [Vote-Pages](#Vote-Page)
### 2.4 Go to General [Vote-Pages](#Vote-Page)

![image](https://user-images.githubusercontent.com/5900841/89294064-9b145d00-d667-11ea-9f4d-c06a4fa78d05.png)

# 3. <a id="Vote-Page"> Vote page</a>

## 3.1 Default Mode

## Actions:

### 3.1.0 Open [Side-Menu](#Side-Menu)
### 3.1.1 Breadcrumbs - go to [Welcome](#welcome) page
### 3.1.2 Breadcrumbs - go to [Choose-topics](#Choose-Topics) page
### 3.1.3 Breadcrumbs - go to [Draft](#draft) page
### 3.1.4 Next button - Go to next [Vote-Page](#vote-page)
### 3.1.5 Back button - Go to last page visited

![image](https://user-images.githubusercontent.com/5900841/89295121-30fcb780-d669-11ea-9b78-ff2c1e07d5f5.png)

### 3.1.6 Vote pro
#### 3.1.6.1 pro voting button change color
#### 3.1.6.2 counter on button add 1
#### 3.1.6.3 counter on "supporters needed" reduce 1:
![image](https://user-images.githubusercontent.com/5900841/89380818-dd3dad00-d700-11ea-9691-c417f9978eb6.png)

### 3.1.7 Vote con
#### 3.1.7.1 con voting button change color
#### 3.1.7.2 counter on button add 1
#### 3.1.7.3 counter on "supporters needed" add 1
#### 3.1.7.4 ["add new edit suggestion"](#add-new-edit-suggestion) button appear
![image](https://user-images.githubusercontent.com/5900841/89381065-445b6180-d701-11ea-99d0-8fce2ceab7a4.png)

## 3.2 Section Edit Suggestions Tab Mode
## Actions
### 3.2.1 Click on Edit Section Suggestions Tab
Display edit section suggestions list
### 3.2.2 "Show Changes" switch
True by default, after click cancel diff view of text
### 3.2.3 Show Comments list

![image](https://user-images.githubusercontent.com/5900841/89383369-052f0f80-d705-11ea-9fc0-75f9fbd0409d.png)

### 3.2.4 <a id="Add-new-edit-section-suggestion"> Add new edit section suggestion</a> button
### 3.2.5 Insert section content
### 3.2.6 Click Publish
A new section will be added, and the new section page should be loaded.
In data model, the section.parentSection field should get sectionId of the section which the user visit when publish the new edit section.
In parens section counter on edit section suggestions tab will add 1.
Also the new section ID should add to section.toEdit field of the parent section.

![image](https://user-images.githubusercontent.com/5900841/89394244-817d1f00-d714-11ea-8bfa-c30195664ca7.png)

## 3.3 Add Comments Mode
## Actions
### 3.3.1 Add new comment button
Comment text box is open
### 3.3.2 Insert comment content
### 3.3.3 Click "publish" button
New comment is added to list, and the page view scroll to the new comment

![image](https://user-images.githubusercontent.com/5900841/89383719-a74ef780-d705-11ea-8b61-bb959c0ff5b7.png)

### 3.3.4 Add new comment on comment button
### 3.3.5 Insert comment on comment content
### 3.3.6 Click "publish" button
New comment on comment is added to list, and the page view scroll to the new comment on comment.

![image](https://user-images.githubusercontent.com/5900841/89393315-4f1ef200-d713-11ea-8bbc-7e713cdcb001.png)

## 3.4 Last Page Mode

## Actions:

### 3.4.1 [Add New Section](#Add-New-Section) Button
### 3.4.1 Go to [Summary](#Summary) Page

![image](https://user-images.githubusercontent.com/5900841/89295077-1aeef700-d669-11ea-8d44-f3a64b67e084.png)

# 4. <a id="Summary-Page"> Summary page</a>

## Actions:

### 4.0 Open [Side-Menu](#Side-Menu)
### 4.1 Breadcrumbs - go to [Welcome](#welcome) page
### 4.2 Breadcrumbs - go to [Draft](#draft) page
### 4.3 Notifications Check Box - 
Click mark check box
### 4.4 Go to [Choose-topics](#Choose-Topics) button
### 4.5 Go to [Draft](#draft) button

![image](https://user-images.githubusercontent.com/5900841/89333620-e77a8f80-d69d-11ea-8ca0-16a912305488.png)
# 5. <a id="Draft"> Draft Page</a>

## Actions:

### 5.0 Open [Side-Menu](#Side-Menu)
### 5.1 Go to Topic [Vote-Pages](#Vote-Page)
### 5.2 If there are edit suggestion for section: Go to [Section-Edit-Suggestions](#Section-Edit-Suggestions) Page
### 5.2 If there are no edit suggestion for section: Go to [Section-History](#Section-History) Page
### 5.3 Open [Section-Side-Menu](#Section-Side-Menu)
### 5.4 Go to [Choose-topics](#Choose-Topics) button
### 5.5 [Add New Section](#Add-New-Section) button


![image](https://user-images.githubusercontent.com/5900841/89296165-a4eb8f80-d66a-11ea-8dac-42ab70fd3b58.png)




