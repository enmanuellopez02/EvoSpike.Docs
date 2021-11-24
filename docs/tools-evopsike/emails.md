# Emails

Emita correos electrónicos con nuestra api de emails de una manera muy fácil, registre su correo electrónico en la herramienta de emails la cual le asignara una api key que debe guardar en un lugar seguro, luego adjunte la información que desea enviar junto con su api key y nuestra api enviara un correo electrónico con su configuración de manera gratuita y segura.

para generar un api key, haga click sobre el botón `Crear email api key`, luego suministre su correo electronico y su nombre, luego haga click en `Agregar`, esto creara un api key unico para esta configuración.

el siguiente paso para enviar correos electronicos es copiar el api key y realizar una solicitud a nuestra api.

## Ejemplo

```
curl --request POST
     --url https://tools-evospike-funtions.azurewebsites.net/api/emails
     --header 'Content-Type: application/*+json'
     --data 
     {
         "To": "prueba@hotmail.com",
         "Subject": "Título",
         "PlainTextContent": "Hola esto es una prueba",
         "HtmlContent": "<strong>and easy to do anywhere</strong>",
         "ApiKey": "203ec27a-a7f2-497a-978a-6a28efd2eb00"
     }
```