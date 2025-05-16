## Preguntas

### Flujo de trabajo: describe brevemente el flujo de trabajo que seguiste para integrar Matter.js en p5.js. ¿Qué se configura en setup()? ¿Qué sucede en draw() respecto a Matter.js (actualizar el motor) y al dibujo de los cuerpos?

En setup() inicialicé el motor de Matter.js, el mundo y el suelo; en draw() actualizo la pantalla y dibujo cuerpos según sus posiciones físicas, ya que el motor se ejecuta automáticamente con Engine.run().

### Representación visual vs. simulación física: ¿Cómo manejaste la relación entre los cuerpos físicos de Matter.js (que tienen posición, ángulo, vértices) y su representación visual en el canvas de p5.js? ¿Hubo algún desafío en “dibujar” los cuerpos correctamente?

Relacioné las coordenadas del cuerpo físico (posición) con el canvas para dibujar la letra “O”, la dificultad o el reto fue alinear visualmente el texto con la simulación para que pareciera parte del mismo diseño.

### Creación de formas complejas: ¿Qué técnica utilizaste para crear las formas de las letras con Matter.js? ¿Fue fácil o difícil? ¿Qué limitaciones encontraste?

 Usé un cuerpo circular para representar la “O”; crear letras reales como cuerpos físicos sería mucho más complejo y requeriría formas personalizadas (vértices), lo cual es limitado y poco práctico para tipografía precisa.

### Física para la semántica: ¿Qué tan efectivo crees que fue usar una simulación física para representar el significado de una palabra? ¿Qué tipo de significados crees que se prestan mejor a este enfoque? ¿Cuáles serían más difíciles?

Es bastante efectivo cuando el significado tiene una relación con movimiento, peso o interacción física (como “caer” o “jugar”); sería más difícil para conceptos abstractos como “amor” o “libertad”.

### Potencial exploratorio: más allá de este reto, ¿Qué otras posibilidades creativas te sugiere la combinación de p5.js y Matter.js?

Puede usarse para juegos tipográficos, visualizaciones interactivas, arte generativo o simulaciones educativas donde el texto cobra vida mediante física realista.
