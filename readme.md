# Facebook Messenger Bot
This is a simple python template that uses Flask to build a webhook for Facebook's Messenger Bot API.
Complete tutorial and original repository by: https://blog.hartleybrody.com/fb-messenger-bot/

## Install Python Dependencies
- mkvirtualenv test-bot
- pip install -r requirements.txt

## Heroku Configuration
- heroku create
- git push heroku master
- heroku open (this command will open the heroku url created, it will be used as a callback url for the webhook)
- heroku config:add PAGE_ACCESS_TOKEN=your_page_token_here
- heroku config:add VERIFY_TOKEN=your_verification_token_here (any string)

## Connecting webhook to Facebook page
At https://developers.facebook.com/apps/, add the product WEBHOOK. When prompted, provide the url created by heroku as the Callback URL and the chosen VERIFY_TOKEN.

Select your page to be subscribed by your webhook events.


## "Callback verification failed"

![Facebook Error](https://cloud.githubusercontent.com/assets/18402893/21538944/f96fcd1e-cdc7-11e6-83ee-a866190d9080.png)

The #1 error that gets reported in issues is that facebook returns an error message (like above) when trying to add the heroku endpoint to your facebook chat application.

Our flask application intentionally returns a 403 Forbidden error if the token that facebook sends doesn't match the token you set using the heroku configuration variables.

If you're getting this error, it likely means that you didn't set your heroku config values properly. Run `heroku config` from the command line within your application and verify that there's a key called `VERIFY_TOKEN` that has been set, and that it's set to the same value as what you've typed into the window on facebook.
