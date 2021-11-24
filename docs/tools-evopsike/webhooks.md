# Webhooks

Los webhooks son eventos que desencadenan acciones entre sistemas, de esta manera puedes generar información con nuestras herramientas y posteriormente enviarlas a tu sistema a través de los webhooks.

para agregar un nuevo webhook haga click sobre el botón `Crear webhook`, luego agrege la dirección url donde posteriormente se enviaran los datos.

## Ejemplo

```
curl --request POST
     --url https://example.com/api/variantes/productos
     --header 'Content-Type: application/*+json'
     --data 
     {
         propiedad1: "valor1",
         propiedad2: "valor2",
     }
```