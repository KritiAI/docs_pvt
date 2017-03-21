# Abstracted Verbs for Kriti AI applications

Here are the currently documented abstracted verbs available for the chatbot logic. These can be chained by putting in an array. The order of execution is determined by the position in the array.

e.g. the following nodejs function shows the typing-on indicator for 2.5 seconds, then removes the typing indicator and moves the user to the element name called  "next\_step\_name" of the flow.

```
function first_step(req){
    var jsonobj = [];
    jsonobj.push({"action" : "typing_on"});
    jsonobj.push({"wait" : 2500});
    jsonobj.push({"action" : "typing_off"});
    jsonobj.push({"wait" : 500});
    jsonobj.push({"goto" : "next_step_name"}); 
    return {"actions" : jsonobj};
}
```

---

# goto

**Usage: **

`{"goto" : "step_name"}`

**Comments: **

Moves the conversation to a specified named element or step of the UX model

---

# wait

**Usage: **

`{"wait" : 2000}`

**Comments: **

Wait time in milliseconds. Good for providing some pause between multiple chained conversational steps.

---

# action

**Usage: **

`{"action" : "typing_on"}`

`{"action" : "typing_off"}`

**Comments: **

Sends the 'typing on' or 'typing off' indicators to the user.

---

# override\_{step\_name}

**Usage: **

`{override_step_name : overrideobj}`

**Comments: **

This overides the message object of the element.

e.g. to override the text of a normal text message in a step named "welcome\_txt", send:

`{"override_welcome_text": {"text" : "new text here"}}`

e.g. to override the text of the button template in a step named "welcomeoptions", send:

```
var overrideobj = {"attachment":{ "payload":{ "text":"What do you want to do next?"}}} ;
{"override_welcomeoptions": overrideobj}
```

Similarly, any type of user step element can be modified by overriding specific parts of its json object.

---

Note: all the verbs should be returned inside an object with the key "actions". Please see example projects and code examples.

-_more verbs will be added here as they are publicly released_-

