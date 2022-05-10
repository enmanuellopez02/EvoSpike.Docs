# Emails

Send emails with our email api in a very easy way, register your email in the email tool which will assign you an api key that you must keep in a safe place, then attach the information you want to send along with your api key and our api will send an email with your configuration for free and safely.

to generate an api key, click the `Create email api key` button, then supply your email and name, then click `Add`, this will create a unique api key for this configuration.

the next step to send emails is to copy the api key and make a request to our api.

## Example

```
curl --request POST
     --url https://tools-evospike-funtions.azurewebsites.net/api/emails
     --header 'Content-Type: application/*+json'
     --data 
     {
         "To": "prueba@hotmail.com",
         "Subject": "Title",
         "PlainTextContent": "Hello this is a test",
         "HtmlContent": "<strong>and easy to do anywhere</strong>",
         "ApiKey": "203ec27a-a7f2-497a-978a-6a28efd2eb00"
     }
```