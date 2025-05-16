En la simulacion se esta creando un canvas y se dibujan dos circulos y una linea entre ellos y se esta rotando el angulo en medida de cada vez que se dibuja

Creo que se esta trasladando al centro de la pantalla por que si no lo hiciera el objeto comenzaria a alejarse y a perderse del frame, el centrar el eje permite que todo permanezca en el encuadre

El sistema de cordenadasse asigna en el centro siempre y el rotate creo que rota directamente todo el canvas por que al meter otro elemento digamos un triangulo, tambien se puede observar como este esta rotando constantemente

La razon por la cual se calcula todo desde el centro en vez de la esquina como el 00 es para que se pueda observar bien como todo el elemento esta rotando y para que el eje de rotacion del canvas como tal sea desde un punto centrado


    ¿Qué hace la función heading()?
    ¿Qué hace la función push() y pop()? Realiza algunos experimentos para entender su funcionamiento.
    ¿Qué hace rectMode(CENTER)? Realiza algunos experimentos para entender su funcionamiento.
    ¿Cuál es la relación entre el ángulo de rotación y el vector de velocidad? Trata de dibujar en un papel el vector de velocidad y cómo se relaciona con el ángulo de rotación y la operación de traslación y rotación.

La funcion heading sirve para calcular el angulo entre el vector 2D y el eje positivo, basicamente hacia donde sea el psoitivo para ese vector en otras palabras

Push y pop funcionan para que los elementos que afectan todos los elementos del canvas sean parametrizados digamos a solo una serie de elementos. Como ejemplo la funcion rotate() pondria a girar todo el canvas, por contraparte si la llamamos entre un statemenet de push y pop solamente rotaria los elementos contenidos en ese bloque de push pop

rectMode cambia en donde se estaran dibujando los elementos, en particular rectMode(CENTER) hace que los elementos se dibujen desde el centro de el 00 en vez de alguna esquina de este
