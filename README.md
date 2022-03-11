# Steps for Echo Bot

## Step 1
    Create a new workspace on Slack

## Step 2
    Create a new Slack App and give it the following bot scopes:
    ![Screenshot](https://github.com/joshuahuerto2/cps847-midtermPractice/blob/master/BotTokens.png)
    Install into workspace after completion

## Step 3
    Create a new folder and start python virtual environment:
    ```bash
    python -m venv .venv
    source .venv/scripts/activate (Windows)
    ```

## Step 4
    Export tokens into virtual environment:
    ```bash
    export SLACK_BOT_TOKEN=xoxb-token
    export SLACK_SIGNING_SECRET=secretToken
    ```

## Step 5
    Ensure that ngrok is installed on machine and run the following command:
    ```bash
    ngrok http 3000
    ```

## Step 6
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

## Step 7
    Enable event subscriptions in Slack app settings, making sure that the URL includes /slack/events:
    ![Screenshot](https://github.com/joshuahuerto2/cps847-midtermPractice/blob/master/EventTokens.png)

## Step 8
    Run the program:
    ```bash 
    python app.py
    ```

## Step 9 
    Profit.
