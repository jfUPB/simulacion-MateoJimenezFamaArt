# Diferencia entre paso a paso y referencia

Cuando hablamos de la diferencia entra paso a paso y referencia estos dos elementos son fundamentalmente diferentes en el sentido en que:

*Paso a paso* -> Permite alterar el valor que este en una variable por completo y guarda eso de manera "directa"
*referencia* -> Permite alterar el valor que esta asignado a una variable de manera "indirecta"

La mejor forma de describir esto es que hacer paso a paso es cambiar el valor de una variable de manera puntual y ya. Pero hacerlo por referencia es cambiar el valor que se encuentra almacenado en esa variable como tal.

# Que implica

En el fragmento de codigo implica que si hacemos 

``` js
let friction = this.velocity.copy();
```

Vamos a crear una nueva copia de la friccion como una velocidad y si queremos podemos llamarla como referencia y modificarla pero su valor incial seguiria siendo el mismo

Sin emabrgo si llamamos

```js
let friction = this.velocity;
```

Vamos a hacer que la friccion sea la velocidad y si luego esta la alteramos entonces la nueva velocidad de friccion va a ser la velocidad alterada que acabamos de crear puesto a que aca se hace por referencia.
