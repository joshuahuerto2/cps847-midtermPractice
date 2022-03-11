# Steps for Echo Bot

## Step 1
Create a new workspace on Slack

## Step 2
Create a new Slack App and give it the following bot scopes:
    ```
    app_mentions:read
    chat:write
    im:write
    incoming-webhook
    ```
Install into workspace after completion

## Step 3
Enable Incoming Webhooks by clicking on Incoming Webhooks in the app settings.
Choose a channel in your workspace where the Webhook can reside.
Paste the sample curl request into a terminal to test if it works.
## Step 4
Create a new folder and start python virtual environment:
    ```bash
    python -m venv .venv
    source .venv/scripts/activate (Windows)
    ```

# Steps for Echo Bot

## Step 1
Create a new workspace on Slack

## Step 2
Create a new Slack App and give it the following bot scopes:
```
app_mentions:read
chat:write
im:write
incoming-webhook
```
Install into workspace after completion.

## Step 3
Enable Incoming Webhooks by clicking on Incoming Webhooks in the app settings.
Choose a channel in your workspace where the Webhook can reside.
Paste the sample curl request into a terminal to test if it works.

## Step 4
Create a new folder and start python virtual environment:
```bash
python -m venv .venv
source .venv/scripts/activate (Windows)
```
## Step 5
Export tokens into virtual environment:
```bash
export SLACK_BOT_TOKEN=xoxb-token
export SLACK_SIGNING_SECRET=secretToken
```

## Step 6
Ensure that ngrok is installed on machine and run the following command:
```bash
ngrok http 3000
```

## Step 7
Install slack_bolt python package:
```bash
pip install slack_bolt
```
And add the following code into a new app.py file:
```python
import os
# Use the package we installed
from slack_bolt import App

# Initializes your app with your bot token and signing secret
app = App(
    token=os.environ.get("SLACK_BOT_TOKEN"),
    signing_secret=os.environ.get("SLACK_SIGNING_SECRET")
)
# Add functionality here
@app.event("app_mention")
def mention_handler(body, say):
    say(body.get("event").get("text"))
# Start your app
if __name__ == "__main__":
    app.start(port=int(os.environ.get("PORT", 3000)))
```

## Step 8
Enable event subscriptions in Slack app settings, making sure that the ngrok URL includes /slack/events.
Click on Subscribe to bot events and add the ``app_mention`` event, making sure to save changes before leaving.
    

## Step 9
Run the program:
```bash 
python app.py
```

## Step 10 
Profit.
