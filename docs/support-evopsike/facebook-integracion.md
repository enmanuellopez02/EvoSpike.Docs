# Messenger from Facebook

Using the EvoSpike Support Facebook Messenger integration, you can create a Facebook Messenger bot to interact with your end-users.

## How it works

This is how the integration works:

-  You create a Facebook app that uses the [Facebook Messenger platform](https://developers.facebook.com/docs/messenger-platform/overview).

-  You configure the EvoSpike Support integration and Facebook app, so that they communicate with each other.

-  The EvoSpike Support integration sends messages to the end-user by using the [Facebook Messenger API](https://developers.facebook.com/docs/messenger-platform/reference/send-api/).

-  The EvoSpike Support integration receives messages from the end-user by acting as the [Facebook Messenger Webhook](https://developers.facebook.com/docs/messenger-platform/webhooks).

## Setup

To set up the integration:

1. Follow the steps to create a Facebook app: [Facebook App Development](https://developers.facebook.com/docs/development).

2. Set up the Facebook app to use the Facebook Messenger Platform. Follow steps in the [Setting Up Your Facebook App](https://developers.facebook.com/docs/messenger-platform/webhooks) documentation to accomplish the following:
    - Add the Messenger Platform to your Facebook app.

    - Subscribe your app to a Facebook page. You are provided with an access token at this step. Copy this value. This token will be used to configure the integration from the EvoSpike Support.

    - Do not configure the webhook or test your integration yet.

3. Configure the integration from the EvoSpike Support

    - Go to the [EvoSpike Support](https://support.evospike.com/Dominios/Configuracion).

    - Click **Chatbot** and then **Integrations** in the left sidebar menu.

    - Click **Messenger from Facebook**.

    - A configuration dialog opens:

        - **Callback URL**: Copy this value. This will be used to configure the Facebook Messenger Webhook.

        - **Verify Token**: You can enter any private token you desire. Copy this value. This will be used to configure the Facebook Messenger Webhook.

        - **Page Access Token**: Enter the access token you copied when creating the Facebook page.

        - **Start**: Click to start this integration service for your agent.

4. Finish setup of the Facebook app and test it. Follow steps in the [Setting Up Your Facebook App](https://developers.facebook.com/docs/messenger-platform/webhooks) documentation to accomplish the following:
    - Configure the Facebook webhook for your app. Use the Callback URL and Verify Token values you copied above. Be sure to enable messages and messaging_postbacks.

    - Test your app.