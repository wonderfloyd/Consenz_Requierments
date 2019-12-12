# <a id="top"></a> Logics
This file contains the logical specifications of the views to be developed. They consist of:
- [Rules](#rules)
  - [User Connected Rule](#user-connected-rule)
- [Algorithms](#algorithms)
  - [Most Agreed Upon](#most-agreed-upon)
  - [Specific CNS_Topic Suggestions](#specific-cns-topic-suggestions)
  - [Sort by CNS_Topic](#sort-by-cns-topic)   

   

### <a id="top"></a> Rules:
- __User Connected Rule__<a id="user-connected-rule"></a>
  - Description: The user tries to perform an action that only a Logged-In (Connected) user can perform. If the user is connected than he can do the action and proceed to the next page state. If the user is not connected, he moves to login page and after he's logged in the action is performed.
  - States:
    - state:
        - user_connected: true
      - feedback: The action the user performs executes according to the action logic (feedback, to, ...)
    - state:
      - user_connected: false
    - to: Login Page
    - feedback: When trying to perform an action, the user is directed to Login Page. After the user logs in, he is directed back to the page where the action he wanted to perform and the action continue to execute according to the action logic (feedback, to, ...)  
    
### <a id="algorithms"></a> Algorithms:
- __Most Agreed Upon__<a id="most-agreed-upon"></a>
  - type: Sort
  - variables:
    - name: suggestionsList
      - description: List of all Suggestions for voting.
      - dataModel:
        - model: Section
        - condition:
          - toEdit: Not Empty
    - name: x, y
      - description: Suggestion items in suggestionsList for voting
  - logic:  For x, y in suggestionsList: x before y if (x.pros - x.cons) > (y.pros - y.cons)
- __Specific CNS_Topic Suggestions__<a id="specific-cns-topic-suggestions"></a>
  - type: Filter
  - variables:
    - name: specificTopic
      - type: String
    - name: topicSuggestionsList
      - description: List of all Suggestions for voting that belong to a specific topic
      - dataModel:
        - model: Section
        - condition:
          - edited: Not Empty
          - topic: Equal to specificTopic
- __Sort by CNS_Topic__<a id="sort-by-cns-topic"></a>
  - type: Sort
  - filter: Specific CNS_Topic Suggestions
  - variables:
    - name: specificTopic, topicSuggestionsList
      - ref: Specific CNS_Topic Suggestions
    - name: x, y
      - description: Suggestion items in topicSuggestionsList for voting
  - logic:
    - ref: Most Agreed Upon