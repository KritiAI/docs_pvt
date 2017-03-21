# Kriti AI App Architecture

* **Each Kriti AI App is connected to:**

  * Single FB App
  * Single S3 bucket
  * Single Lambda function
  * Single API gateway

* **Each Kriti AI app can have:**

  * Unlimited UX Models and UX flows
  * Unlimited Facebook Pages each connected to the desired UX model
  * Unlimited users and clients with specific roles and permissions





* **Each UX model is:**

  * Connected to a specific branch in a defined Github repo
  * Auto-deployed with versioning and aliasing to a Lambda function from github repo
  * Auto-deployed to a specific aliased end-point on Api Gateway
  * Connected to unlimited Facebook Pages



