- DOM Document object Model. (el arbol de etiquetas).
[NOTE]
Las cookies tienen alternativas que son local storage y sessionStorage, IndexDB
- Este año vamos a usar la localhost para ver las webs qeu hagamos 127.0.0.1
usaremos el vs code server live, que usa el puerto que nos diga en el ide y la direccion del workspace que estemos usando. 
- Vamos a usar mdn de mozilla developers va a ser nuestra biblia este año para ver informacion y dudas de Javascript. 

## Promesas  (programacion asincrona)
Yo pido algo al servidor, el me lo gestiona y mientras se lanza o no lanza, se van cargando el resto de datos de la pagina.

20/9/24

### Los códigos de estado de HTTP:

200 -299 va bien
400-499 el error es del cliente
500 -599 el error es del servidor

para seleccionar un elemento podemos hacerlo de estas formas 
```javascript
document.getElementById("encabezado").innerHTML = "texto cambiado"; //la id encabezado la cambia por texto cambiado
document.querySelector("h1");//seleccion el h1 como objeto
document.querySelectorAll();
document.querySelector("h1").innerHTML //Selecciona el interior de la etiqueta.
document.querySelector("h1").outerHTML //Selecciona la etiqueta desde que abre hasta que cierra entera.
```