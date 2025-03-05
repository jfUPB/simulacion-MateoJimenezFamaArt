# Respuestas

## ¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?

El metodo mag sirve para encontrar la magnitud de un vector (la longitud de ese vector)
El metodo magSq sirve para encontrar la magnitud de un vector al cuadrado

La diferencia es que uno de ellos llama solo la magnitud de un vector y la otra llama la magnitud de un vector que esta al cuadrado.

En terminos de eficiencia depende de lo que se quiera hacer, si se necesita saber que hay mas alla del vector como para encontrar la magnitud de ese mismo vector al cuadrado entonces es mejor el magSq si no entonces el mag es suficiente para simplemente hayar la magnitud del vector.

## ¿Para qué sirve el método normalize()?

El metodo normalize sirve para poder normalizar el vector que se le este pasando y poder encontrar la direccion de este vector, esto es util ya que saber la direccion del vector nos permite facilmente saber hacia donde se movilizara un objeto.

## Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?

Sirve para hayar el producto punto entre dos vectores.

## El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?

La version estatica se le pasan los valores de un vector ya existente con el fin de hayar el producto punto de vector1 y vector2. La version de instancia de dot() genera un nuevo vector.

## Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.

La interpretacion geometrica del producto cruz de dos vectores da como resultado la normal del plano donde habitan esos dos vectores. Es decir imaginate que tienes una tabla de picar, y en esta tabla hay un pedazo de cebolla (vector 1) y un pedazo de tomate (vector 2), si tomas un cuchillo y cortas ambas a la vez (realizas el producto cruz)
el liquido de la cebolla y del tomate saldra disparado hacia tus ojos de manera perpendicular a la tabla (ya que los jugos son el producto cruz de los dos vectores saliendo del plano como la normal, enteramente perpendicular al plano).

## ¿Para que te puede servir el método dist()?

Sirve para encontrar la distancia entre dos vectores, esto nos sirve para concer cuanta distancia hay entre objeto 1 y 2. Esto con el fin de poder hayar cuanto debe recorrer cierto vector para hayar el punto donde pueda colisionar con el otro por ejemplo en un juego de ponchado si el dist entre pelota y jugador es 0 entonces jugador esta eliminado.

## ¿Para qué sirven los métodos normalize() y limit()?

El metodo normalize es para hayar la direccion del vector normalizandolo a valores de 1, si es 1, 0, -1 nos da a entender la direccion en cuestion de nuestro vector.
El metodo limit es para limitar la magnitud de un vector, o sea nos permite definir un punto maximo hasta donde nuestro vector puede viajar, como ponerle una barrera de que hasta ahi llega y no peude seguir mas.
