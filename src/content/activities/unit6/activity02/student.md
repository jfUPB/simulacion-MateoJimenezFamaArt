Explica brevemente la estructura de datos usada para el campo de flujo y cómo se generan sus vectores.
Describe con tus palabras cómo un agente utiliza el campo para calcular su fuerza de dirección.
Lista los parámetros clave identificados (resolución, maxspeed, maxforce).
Describe la modificación que realizaste al código y explica detalladamente el efecto que tuvo en el movimiento y comportamiento colectivo de los agentes. Incluye una captura de pantalla o GIF si ilustra bien el cambio. Muestra el fragmento de código modificado.


## Como se hace la estructura de datos y sus vectores?

Esta estructura de datos es un array el cual guarda todos los vectores, este array esta hecho en base a la cantidad de columnas y filas que definimos previamente. Sus vectores se generan de manera dinamica mediante varios metodos, pueden ser generados de manera pre determinada por codigo o dinamicamente modificables mediante ruido perlin o otrso elemntos de randomizacion.

## Como se utiliza el campo para calcular la direccion?

El campo se utiliza al modificar el valor de la velocidad deseada que se quiere tener y esto se resta a la actual para obtener una fuerza de "steering" con esta fuerza de steering se calcula la direccion en la que se estara moviendo el objeto por que como toda buena velocidad es un vector.

## Parametros clave identificados

Resolucion : Cuantos vectores por pixel tendremos en nuestro sistema

maxSpeed : Velocidad maxima que le permitiremos tener a nuestros vehiculos

maxForce : Fuerza maxima en sumatorias que nuestr objeto podra alcanzar

## Modificacion realizada

![image](https://github.com/user-attachments/assets/5a18953e-5de4-4320-aac8-2e5fffcb841e)

Hicimos que los vectores se generen en un patron circular empleando cordenadas polares, para lograr esto modificamos la funcion init() que es donde se crean estos vectores:

'''js
init() {
  let centerX = width / 2;
  let centerY = height / 2;

  for (let i = 0; i < this.cols; i++) {
    for (let j = 0; j < this.rows; j++) {
      let x = i * this.resolution + this.resolution / 2;
      let y = j * this.resolution + this.resolution / 2;

      // Vector desde el centro hasta la celda actual
      let dir = createVector(x - centerX, y - centerY);
      dir.normalize();

      // Girar el vector 90 grados para que sea tangencial (circular)
      let angle = atan2(dir.y, dir.x) + HALF_PI;

      // Crear un nuevo vector con esa dirección
      this.field[i][j] = p5.Vector.fromAngle(angle);
    }
  }
}
'''

En esta modificacion los vehiculos siguen un patron de movimiento circular
