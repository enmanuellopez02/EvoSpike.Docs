# Webhooks

Webhooks are events that trigger actions between systems, so you can generate information with our tools and then send it to your system through webhooks.

to add a new webhook click on the button `Create webhook`, then add the url address where the data will be sent later.

## Example

```
curl --request POST
     --url https://example.com/api/variants/products
     --header 'Content-Type: application/*+json'
     --data 
     {
         "property1": "value1",
         "property2": "value2",
     }
```