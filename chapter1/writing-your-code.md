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

**Note 1: The project name and the REPO name SHOULD BE the same i.e. "samplebot" in this case.**

**Note 2: The main script name SHOULD NOT be same as the repo name. **Use any other name e.g. app.js, index.js or anything but  the repo name \(samplebot.js in this case\)

Lets create your main script, assuming you selected "index.js" when doing npm init:

```
touch index.js
```

Now open your index.js file in your favorite code editor and put your code in this format:

```
module.exports.welcome_logic = function(req){

    var jsonobj = [];                                     //actions array
    jsonobj.push({"goto" : "welcome_txt"});         //adding an abstracted verb action
    return {"actions" : jsonobj};                         //returning this response to the bot 
}
```

Note: The abstracted verbs are being sent back as an array under the key "actions" for the return object

**Here is a more comprehensive example:**

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

## Deploying your code

If you have enabled the github auto deployment option in your UX model settings and setup the kriti AI provided webhook under your repo's settings, then the deployment process is automatic all the time.

After making any change to your code files, you can run this command to push the changes to your github repo:

```
git add -A && git commit -a -m "description of your new changes" && git push origin master
```

This will push the new changes to your github repo. From there the github repo will inform the Kriti AI engine via the webhook about the new code changes. The Kriti AI automated Continuous Integration and Continuous Deployment engine will run a basic sanity check of your code and deploy it as a new aliased version of the lambda function and make necessary changes behind the scenes to ensure that everything works!

This generally takes 3 seconds to 10 seconds depending on the size of your codebase .

## The "req" object

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
      "key1" : "value1",                        //just sample data for illustration
      "key2" : ["value2_0", "value2_1"]         //just sample data for illustration
   }
}
```

## Data Storage

Each user has a data store where complex objects can be stored in key/value pairs. The term used for data storage in Kriti AI is called "databag".

Access the databag via the req.databag object and add/modify the contents or key/value pairs.

To save this data for future access, return the modified databag as the result of the function call. If no databag parameter is returned the original databag contents remain unaltered.

```
function step_name(req){
var jsonobj = [];
jsonobj.push({"goto" : "main_menu"});

req.databag["key3232"] = {"k1" : "v1", "k2": "v2"};

return {"actions" : jsonobj, "databag" : req.databag};
}
```

Now in subsequent function calls the databag will contain the keys and the associated data that you added in this step above.

## 

## Promises:

Please note that when using lambda serverless deployment, you should return either the response object synchronously or return a javascript promise which will have the response object. You can choose to work with native Promises or any of the popular promise ibraries. e.g. bluebird etc

Here is an example of using bluebird promise. First install the bluebird library.

```
npm install -S bluebird
```

Then add references on top of your index.js file:

```
const Promise = require('bluebird');
```

Now in any of your functions you can return response object like this:

```
module.exports.STEP_NAME  = function(req){

var jsonobj = [];

if (req.textinput && req.textinput != ""){  //user typed somthing

return get_NLP_results(req.textinput)   // assuming get_NLP_results is a function which returns a promise
                .then(function(wht){ 
                        if(wht != ""){
                            jsonobj.push({"goto" : "show_search_result"});  //display "show_search_result" step
                        }
                        else{
                            jsonobj.push({"goto" : "show_options"});   //show the "show_options" step
                        }
                })
                .then(function(){                    
                        return {"actions" : jsonobj}; //returning this response to the bot
                });
}
else{  //user clicked on something
    jsonobj.push({"goto" : "main_menu"});
}

return {"actions" : jsonobj, "databag" : req.databag};  //returning this response to the bot if not inside textinput
}
```

# Support and Community access

1. Please join [this facebook group](https://www.facebook.com/groups/689444534571301/ "Kriti AI Creators Hub") to get access to the latest information, feature roadmap and feedback on various aspects
2. Email: support\[at\]kriti.ai



