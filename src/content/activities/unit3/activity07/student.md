El problema con este planteamiento es que al hacer las llamadas estamos modificando el valor de la masa de nuestro objeto por que estamos haciendo una llamada X referencia entonces esto modifica el valor y si fueramos a calcular esto con dos objetos, el primero funcionaria bien y normal pero el segundo tendria como masa el valor de la fuerza restante a la hora de sumar la fuerza. Para poder evitar esto podriamos emplear la funcion de p5.js que se llama .copy, esto hace que podamos crear una copia de un elemento y asi podemos utilziarlo y llamarlo sin estar sobre escribiendo elementos de nuestro objeto como tal.

Para verlo en p5.js seria algo como:

```js
applyForce(force) {
  let f = force.copy();

  f.div(this.mass);

  this.acceleration.add(f);
}
```
