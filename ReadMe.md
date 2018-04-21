
# xMatters MSTeams integration
Stand alone MSTeams bot coded in NodeJS

<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

# Pre-Requisites
* Microsoft Teams bot appID and password 
	* This requires you to sign up for an msbot account here (https://dev.botframework.com)
	* Create a bot by going to here (https://dev.botframework.com/bots/new)
* A place to host a NodeJS application
* xMatters account - If you don't have one, [get one](https://www.xmatters.com)!

# Files
* [ExampleCommPlan.zip](ExampleCommPlan.zip) - This is an example comm plan to help get started. 

# How it works
Once this is setup then you can install the application into MS Teams, when a message gets sent to the bot the message gets processed by the NodeJS application and makes the required calls to xMatters and returns a response message.

# Installation
Details of the installation go here. 

## xMatters set up

1. Import a communication plan (link: http://help.xmatters.com/OnDemand/xmodwelcome/communicationplanbuilder/exportcommplan.htm)

2. Create the "MSTeams" Endpoint and add the url for the hosted bot.

3. Create the "MSTeams path" Constant and add the value "/api/response".

## New to Microsoft Bots?
1. Setup a sample bot with Bot Service
https://docs.microsoft.com/en-us/azure/bot-service/bot-service-quickstart

2. Test the sample Bot in Web Chat
https://docs.microsoft.com/en-us/azure/bot-service/bot-service-manage-test-webchat

3. Test the sample Bot in MS Teams with 1 on 1 chat.
https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/bots/bots-test

4. In MS Teams use Teams App Studio to access your bot in Teams. Essentially, in Teams App Studio you will define a Manifest that points to the bot in step 1.  
https://docs.microsoft.com/en-us/microsoftteams/platform/get-started/get-started-app-studio

A couple things of note:
a. The bot frameworkid is the same as the Microsoft AppID.  You will enter this in two places.  You can get the Microsoft AppID of the bot from the Azure console.

<kbd>
  <img src="need picture">
</kbd>

5. Export the manifest and import it to a Team.  You will be able to @botname a command to bot in that team.
https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/apps/apps-upload

6. Now you have a working bot in teams you can customize it with the following information.

## Deploy bot from Github repo to Azure
1. Fork the sample repo.

2. Login to Azure portal.  Create a new bot 
https://docs.microsoft.com/en-us/azure/bot-service/bot-service-quickstart

3. Follow directions below to setup continous deliver.
https://docs.microsoft.com/en-us/azure/bot-service/bot-service-build-continuous-deployment

## Deploy bot from Github repo to Node.js server (Google Cloud)
1. Generate the MSTeams installation file by running "gulp" in the route directory.

2. Host the files in a location and run using the following commands:

```

npm install
npm start

```
3. or To deploy your own version run the following command:

	gcloud app deploy --version <your version name> --no-promote
	

## Specific AppId's, webhooks and credentials that need to be modified.

1. Replace all instances of "********-****-****-****-************" with your microsoftAppId.

```
.env:
line 3

manifest.json:
line 5,
line 42,
line 76

default.json:
line 3

```

2. Replace all instances of "-----------------------" with your microsoftAppPassword.

```
.env:
line 4

/config/default.json:
line 4

```

3. Replace all instances of "https://xmatters-url.com" with your xMatters URL.

```

/config/default.json:
line 7

```

4. Add your xMatters rest username and password to /config/default.json

5. update the integration codes in /config/default.json to match the inbound integrations in your xMatters instance.

```
Example:

https://xmatters-url.com/api/integration/1/functions/d0b41e9a-dc8b-4620-93ec-03e96f5cabf8/triggers

Would be "d0b41e9a-dc8b-4620-93ec-03e96f5cabf8"

```

## MS Teams set up

1. In MS Teams use Teams App Studio to access your bot in Teams. Essentially, in Teams App Studio you will define a Manifest that points to the bot in step 1.  
https://docs.microsoft.com/en-us/microsoftteams/platform/get-started/get-started-app-studio

A couple things of note:
The bot frameworkid is the same as the Microsoft AppID.  You will enter this in two places.  You can get the Microsoft AppID of the bot from the Azure console.

<kbd>
  <img src="need picture">
</kbd>

2.Export the manifest and import it to a Team.  You will be able to @botname a command to bot in that team.
https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/apps/apps-upload


# Testing
This integration has had some testing but more is required, to do this follow these steps in windows:

1. download the msteams botframework emulator

	https://github.com/Microsoft/BotFramework-Emulator/releases

2. Download the ngrok executable to your local machine.

	https://ngrok.com/

3. Open the emulator's App Settings dialog, enter the path to ngrok, select whether or not to bypass ngrok for local addresses, and click Save.

4. connect to the url (localhost if testing locally)

	https://hosted-site.com/api/messages

5. type in help to get the list of commands

# Development

To run a dev environment locally run:

```

npm run dev

```

This will automatically restart the app when any files are changed.




