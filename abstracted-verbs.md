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

This overrides the message object of the element.

e.g. to override the text of a normal text message in a step named "welcome\_txt", send:

`{"override_welcome_text": {"text" : "new text here"}}`

e.g. to override the text of the button template in a step named "welcomeoptions", send:

```
var overrideobj = {"attachment":{ "payload":{ "text":"What do you want to do next?"}}} ;
{"override_welcomeoptions": overrideobj}
```

Similarly, any type of user step element can be modified by overriding specific parts of its json object.

---

# callback\_after

**Usage:**

```
{"callback_after" : {
        "callbackalias" : "anyname_for_future_reference",  //for analytics and other references
        "afterseconds" : 60,                               //in seconds
        "functionalias" : "step_name",                     //name of the step to be triggered
        "payload": "your-payload-string"                   //any data to be passed to the step's function
        }
    }
```

**Comments:**

This triggers the UX flow step after the specified time \(in seconds\). The name of the step to trigger is is passed through as "functionalias". Any data can be passed to that function by specifying the "payload" string. This is passed to the function under the req.textinput object.

---

# callback\_at

**Usage:**

```
{"callback_at" : {
        "callbackalias" : "anyname_for_future_reference",  //for analytics and other references
        "at" : "2017-05-10T13:19:11Z",         //ISO datetime string can have timezone offset as well: 2017-05-10T13:19:11-05:30, or 2017-05-10T13:19:11Z
        "timezoneoffset" : req.user.timezone,  //(optional) this will ensure that the time is calculated as per user's timezone
        "functionalias" : "step_name",         //name of the step to be triggered
        "payload": "your-payload-string"       //any data to be passed to the step's function
        }
    }
```

**Comments:**

This triggers the UX flow step at the specified datetime.

Tip: If you want to trigger the callback at the user's timezone, just send the global variable req.user.timezone under "timezoneoffset".

The name of the step to trigger is is passed through as "functionalias". Any data can be passed to that function by specifying the "payload" string. This is passed to the function under the req.textinput object.

---

Note: all the verbs should be returned inside an object with the key "actions". Please see example projects and code examples.

-_more verbs will be added here as they are publicly released_-

