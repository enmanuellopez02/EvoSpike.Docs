# Product variants

Generate product variants with our powerful tool in a matter of seconds, add images and generate combination results between features such as color, size or material in an easy and intuitive way, then send the results to your system through webhooks.

to generate variations of a product, click on the `Create product variant` button, then fill in the information in the form and then click on the `Generate variations` button.

to send the information to your project, select the webhook with the url address of your project where the data will be sent.

## Example of how the data will be sent to your webhook

```
curl --request POST
     --url https://example.com/api/variants/product
     --header 'Content-Type: application/*+json'
     --data 
     {
         "ProductoID": "P01",
         "Quantity": 10,
         "Images": ["image1.png", "image2.png"],
         "Variants": 
         [
           {
             "SKU": "P01-01",
             "CharacteristicsAttributes": 
             [
                {
                  "AttributeName": "Size", 
                  "ValueId": "S"
                },
                {
                  "AttributeName": "Color", 
                  "ValueId": "Rojo"
                }
             ],
             "VariantType": "S . Rojo",
             "Image": "image1.png",
             "Quantity": 5
           }
         ]
     }
```
