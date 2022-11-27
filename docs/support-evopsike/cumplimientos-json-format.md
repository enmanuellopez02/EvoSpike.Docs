# Fulfillment

Fulfillment are events that trigger actions across systems, so you can collect information from an intent and then send it to your system through compliance.


## Compliance information

```
curl --request POST
     --url https://api.evospike.com/webhook
     --header 'Content-Type: application/*+json'
     --data
     {
         "intencion": "package tracking",
         "botName": "spiky",
         "idioma": "english",
         "parametros": 
         [
            {
                "nombre": "nombre",
                "entidad": "Person",
                "valor": "juan perez"
            },
            {
                "nombre": "tracking",
                "entidad": "Quantity.Number",
                "valor": "897529384790284"
            }
         ]
     }
```

to issue a response based on the information collected, you can respond to this request by sending back a message in response to this compliance.

## Compliance response

``` JSON
{
    "mensaje": "Best regards, Juan Perez, your package corresponding to the tracking number '897529384790284' is in transit"
}
```