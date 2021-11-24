# Variantes de productos

Genere variantes de producto con nuestra poderosa herramienta en cuestiones de segundos, añada imagenes y genere resultados de combinación entre características como color, size o material de una manera fácil e intuitiva, luego envíe los resultados a su sistema a través de los webhooks.

para generar variaciones de un producto, haga click sobre el botón `Crear variante de productos`, luego rellene la información del formulario y luego haga click en el botón `Generar variaciones`.

para enviar la información a su projecto, seleccione el webhook con la dirección url de su projecto donde seran enviado los datos.

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