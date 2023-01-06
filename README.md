
# AutomaticBackgroundGradient

[![GitHub top language](https://img.shields.io/github/languages/top/altaskur/AutomaticBackgroundGardient?style=for-the-badge)](/) [![GitHub](https://img.shields.io/github/license/altaskur/AutomaticBackgroundGardient?style=for-the-badge)](/)

Un pequeño ejercicio practicando con canvas, en el que analizamos una imagen y creamos un color de fondo, según sus bordes

Puedes ver la [versión live aquí](/src/index.html).

Para ello utilizamos un canvas creado en Js para dibujar la imagen dentro pero con el tamaño que queramos analizar de la imagen.
con la propiedad `drawImage`

```js
const sensibility = image.width * 0.40;

context.drawImage(image, 0, 0, image.width, image.height);
```

Analizamos la imagen en las zonas que nos interesa, en este caso
en los margenes izquierdo y derecho de nuestra imagen y abarcando según la sensibilidad

```js
context.getImageData(0, 0, sensibility, image.height).data;
```

La propiedad `getImageData` nos devuelve un Uint8ClampedArray,
Uint8ClampedArray, es un array que utiliza valores de 8 bits truncando los valores de 255 y 0 en el caso de ser mayor o menor de estos. Esto nos devuelve cuatro valores por cada pixel RGBA, siendo A el canal alpha.

Recorremos el array de cuatro en cuatro, teniendo de limite de columna, la sensibilidad.

```js
for (let i = 0; i < leftSideData.length; i += 4 * sensibility) {
```

Con esto obtenemos el color más común de cada sección y lo usamos para crear un background.

```js
figure.style.background = `linear-gradient(to right, ${leftEdgeDominantColor}, ${rightEdgeDominantColor})`;
```
