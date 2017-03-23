# Getting Started

The process requires some additional setup steps for 1st time new creators. Once you have setup your first UX coversation flow, the second one is a lot faster!

## For first-time creators:

**Step 1:** Create a new Kriti app: [https://build.kriti.ai/app/create](https://build.kriti.ai/app/create)

**Step 2:** Configure App Settings page

* Setup connections to your AWS account
  * Enter your S3 bucket access credentials in "Content Storage Settings"
  * Enter your AWS Lambda access credentials  in  "Code Deployment Settings"
  * Click on "Deploy" button to automatically setup lambda functions and auto-configure the Api gateway
  * Click on info button on the settings page for detailed instructions, if you are new to Amazon AWS
* Enter your FB app's info on the same Kriti App settings page

**Step 3:** Configure your first UX Model

* Click on UX design link on the left navigation bar and click on "Create new UX Model" button. Enter the name and select "Github + AWS auto deploy" option
* It will show up as a new UX Model panel on the same page. Click on "Github integration" and enter the access info to your project's repo

**Step 4:** Create the UX flow in your UX Model

* Create the necessary UX elements for your chatbot. There is a clear separation of the design and code. You can put various elements inside different folders/modules
* The copywriter can add/edit the messaging language from the visual UX design interface

**Step 5:** Connect FB page with the UX Model

* Click on the "Activate tab" to connect with your FB app and attach the desired FB page with a specific UX model
* Additional settings can be set up using the on screen options. e.g. 'Get Started' payload, Payment settings, PGP key, Persistent Menu, Greeting text etc

**Step 6:** Write business logic for your bot

1. Give names to your UX flow elements
   1. Click on the "&lt;/&gt;" button in front of each element to connect a specific function with the same name to the element.
   2. Enable "Has business logic?" dropdown to execute remote logic processing for your custom code
2. Write your custom code
   1. The custom code is modular MVC format, with each function now corresponding 1:1 with a specific step of the flow
   2. The user input is available via the passed object to the function
   3. The function responds back a simple json object to affect the flow of the conversation, via abstracted verbs



### Here is an early DEMO video which has these steps 1 to 5 covered:

[https://www.youtube.com/watch?v=qJFC0cHMRyg](https://www.youtube.com/watch?v=qJFC0cHMRyg)

---

## For existing creators:

You can use the same app for multiple use cases. Each app that you create is a bot making platform in itself.  Just create a new UX model and start creating. Different pages can be connected to different UX models under the same app.

_Tip: you can directly start with Step 3,  as shown above. In step 4 click on "Clone from existing" if you want to initiate work with a cloned copy of an existing chatbot UX model._

