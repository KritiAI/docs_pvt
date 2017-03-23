# Data Storage

Each user has a data store where complex objects can be stored in key/value pairs. The term used for data storage in Kriti AI is called "databag".

#### Usage:

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



