# Writing your code

The best way to get started is to create an empty repo in github, say "samplebot".

Also it would be convenient to create a '[Personal Access token](https://github.com/settings/tokens)' for github, Select the scopes under "repo".   
Lets say the token is : 9e1cadee492b1f3fdfaa8f0bd5e04d79

On your terminal type:

```
git clone --branch=master https://USERNAME:9e1cadee492b1f3fdfaa8f0bd5e04d79@github.com/USERNAME/samplebot.git samplebot

```

Note: replace USERNAME with your github username.

This will create a folder called "samplebot" and set up git remote to the repo. 

Now create your nodejs project by typing in your terminal:

```
cd samplebot
npm init
```

This will take you through the node js project creation steps.

Note 1: The project name and the REPO name SHOULD BE the same i.e. "samplebot" in this case.

Note 2: The main script name SHOULD NOT be same as the repo name. Use any other name e.g. app.js, index.js or anything but  the repo name \(samplebot.js in this case\)

Lets create your main script, assuming you selected "index.js" when doing npm init:

```
touch index.js
```

Now open your index.js file in your favorite code editor and put your code in this format:

```
module.exports.welcome_logic = function(req){

    var jsonobj = [];                                     //actions array
    jsonobj.push({"kriti_goto" : "welcome_txt"});         //adding an abstracted verb action
    return {"actions" : jsonobj};                         //returning this response to the bot 
}
```

Note: The abstracted verbs are being sent back as an array under the key "actions" for the return object



Here is a more comprehensive example:

```
module.exports.STEP_NAME = function(req){

if(req.payload && req.payload != ""){

    //user clicked on a button or a quick-reply option, handle the payload response here
}
else if (req.textinput && req.textinput != ""){

    //user typed in something, now you can handle the response here

}  
else if(req.fileinput.length > 0){

      //user uploaded a file, now you can loop through the fileinput object to get the file details
      //req.fileinput[0].url : url of the file archived in your s3 bucket
      //req.fileinput[0].filetype : "image", "video", "audio", "file"
      //req.fileinput[0].fileinfo.fname : name of the file 
      //req.fileinput[0].fileinfo.fext : "gif", "mp4" etc
}

}
```



More details about the "req" object passed to your function. It contains the type of input, basic info about the fb app and fb page, user profile information, and your persistent key/value datastore named as "databag"

```
{  
   "textinput": "user's typed text",
   "payload":"",
   "fileinput":[],
   "fb":{  
      "fbappid": ID_OF_YOUR_FB_APP,
      "fbpageid": ID_OF_YOUR_FB_PAGE,
      "fbpagename": NAME_OF_YOUR_FB_PAGE,
      "addedon": UNIX_TIMESTAMP
   },
   "user":{  
      "fbpsid": FB_PAGE_SCOPED_ID_OF_THE_USER,
      "firstseen": UNIX_TIMESTAMP,
      "first_name": FIRST_NAME,
      "last_name": LAST_NAME,
      "gender": GENDER,
      "locale": "en_US",
      "timezone": Timezone_number_relative_to_GMT,
      "is_payment_enabled":FLAG_SET_BY_FB,
      "picture": PROFILE_PICTURE_URL
   },
   "databag":{  
      "key1" : "value1", 
      "key2" : ["value2_0", "value2_1"]
   }
}
```



