# MVC Programming Model

The main premise is the MVC model with a clear separation of UX flow design and the business logic of the app.

## Step 1: Create UX elements

**Visual: UX Model creation**

The UX flow designer uses the visual interface to add the UX frontend elements of the chatbot into the UX model. The available elements are: Text, Image, Audio, Video, File,  Button template, Generic template, List template

All the relevant features for the UX elements e.g. buttons, quick replies etc are provided via the simple point-and-click interface.

These elements are filed under specific UX modules, which are just like folders holding relevant elements for a specific portion of the chatbot's functionality. The designer and script writer is not expected to work with the logic or programming aspects of the chatbot. See the step 2 for details for programmers.

---

## Step 2: Create the chatbot logic

**Attaching Business Logic to a UX element**

There are 2 steps to this:

1. Allocate a function name to the UX elements by clicking the "&lt;/&gt;" button on the UX model. The function name now references this specific step of the flow. 
2. To process user input on this element just enable the "Has Business Logic?" drop down to "yes". Any user input in response to this element is sent to your function to process

**Programming using Abstracted verbs**

Your function with the specific name handles the backend processing/logic and then affect the conversation flow using a set of abstracted verbs available to all Kriti AI apps. This is the core of the actual conversational experience of the bot as all routing happens through these verbs.

```
function step_name(req)
{
    //do backend processing here
    var jsonobj = [];
    jsonobj.push({"goto" : "next_step"}); //move the user to the UX element called "next_step"
    return {"actions" : jsonobj};

}
```

**Programming: Pre-Process element**

There may be times when the logic may need to be run before an element is sent to the user. In those cases use the {step\_name}\_preprocess function to do any backend processing.

```
function step_name_preprocess(req)
{
//do backend processing here

return {"actions" : []};

}
```

**Programming language and Deployment**

Kriti AI apps can be written in any programming language. The actual interaction between the core Kriti AI SEAM engine and remote business logic happens using JSON data.  

For nodejs developers, there is a powerful native integration which converts the nodejs code pushed to github repo into AWS Lambda functions and provides real time continuous integration and continuous deployment. Each function is mapped to the UX element of the same name.



**Tip: Auto-Move-To-Element's name**

There may be some elements which are to be sent to the user in sequence without any backend processing. Enter the name of the next UX element in sequence to automatically send it, without needing to use the "goto" abstracted verb via remote code processing. There may be cases where both the features can be used in conjunction: "Has Business Logic?" and "Auto-Move-To-Element's name"



---

## Step 3: Testing the chatbot - WARP testing engine

WARP testing engine is a powerful buildout tool, which allows rapid testing of steps in the conversation flow. This works if at least 1 facebook page is attached to the UX model being tested. There are 2 steps to this:

1. Click on the "WARP ⚡" button on the top of the page. It will show a popup with two dropdowns. Select the facebook page and and your name from the two dropdowns
2. To test a specific step in the flow click on the "⚡" button in front of the flow. It will trigger that specific step in a contextually aware manner. Then you can provide your input in the messenger chat window to see how your custom backend logic processes the input. 

Thus with a single click on the WARP button of any element, the Kriti AI SEAM engine will automatically navigate the conversational flow, its various contexts and enable you to test that specific step in a contextually aware manner. 







