# Kriti AI Programming Model

The main premise is the MVC model with a clear separation of UX flow design and the business logic of the app.

#### Visual: UX Model creation

The UX flow designer uses the visual interface to add the UX frontend elements of the chatbot into the UX model. The available elements are:

* Text message
* Image message
* Audio message
* Video message
* File message
* Button template message
* Generic template message
* List template message

All the relevant features for the UX elements e.g. buttons, quick replies etc are provided via the simple point-and-click interface.

These elements are filed under specific UX modules, which are just like folders holding relevant elements for a specific portion of the chatbot's functionality. 



#### Programming: Business Logic of the application

There are 2 steps to this:

1. Allocate a function name to the UX elements by clicking the "&lt;/&gt;" button. The function name now references this specific step of the flow. 
2. If you want to process user input on this element just enable the "Has Business Logic?" drop down to "yes". Any user input in response to this element is sent to your function to process
3. Your function with the specific name can do the backend logic and then affect the conversation flow using a set of abstracted verbs available to you. These are listed on the separate page here. 



