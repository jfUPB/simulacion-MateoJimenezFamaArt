Identifica motion 101. ¿Qué modificación hay que hacer al motion 101 cuando se quiere agregar fuerzas acumulativas? Trata de recordar por qué es necesario hacer esta modificación.


La modificacion que se debe hacer al motion 101 es que se le debe hacer una suma de las fuerzas independientes y luego pasar eso al add force. Y finalmente debemos resetearlo para que no se acumule hasta el infinito y mas alla.


Identifica dónde está el Attractor en la simulación. Cambia el color de este.

![image](https://github.com/user-attachments/assets/83f3d59d-774c-4f51-b7ea-ddc8f3ba2edf)


Observa que el Attractor tiene dos atributos this.dragging y this.rollover. Estos atributos no se modifican en el código, pero permitirían mover el attractor con el mouse y cambiar su color cuando el mouse está sobre él. 
¿Cómo podrías modificar el código para que esto funcione? considera las funciones que ofrece p5.js para interactuar con el mouse.

Para hacer que el atractor funcione con el mouse podemos emplear las varibales de mouseX/Y y con esto y unos cuantos calculos matematicos podemos definir la posicion de nuestro mouse y asi poder interactuar cuando hacemos click usando digamos la funcion mousePressed() o mouseReleased()

