# Abstracted Verbs for Kriti AI applications

Here is the currently documented abstracted verbs available to your chatbot logic. These can be chained by putting in an array. The order of execution would be their position in the array.

e.g. the following nodejs function will show the typing-on indicator for 2.5 seconds, then removes the typing indicator and moves the user to the element name called  "next\_step\_name" of the flow.

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

| Name | Usage | Comments |
| :--- | :--- | :--- |
| goto | {"goto" : "step\_name"} | Moves the conversation to a specified named element or step of the UX model |
| wait | {"wait" : 2000} | Wait time in milliseconds. Good for providing some pause between multiple chained conversational steps |
| action | {"action" : "typing\_on"},{"action" : "typing\_off"} | Sends the 'typing on' or 'typing off' indicators to the user |
| override\_{step\_name} | {override\_step\_name : overrideobj} | This overides the message object of the element |
|  |  |  |
|  |  |  |
|  |  |  |



