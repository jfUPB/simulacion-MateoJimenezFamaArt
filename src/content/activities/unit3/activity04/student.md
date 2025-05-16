# Como se definia antes

Codigos de la unidad anterior sobre como mover los elementos 

```js
      let force = p5.Vector.sub(this.target, this.position);
      if (force.mag() < 0.2) { // Tighter convergence for better shape
        this.arrived = true;
        this.position = this.target.copy();
        this.velocity.set(0, 0);
      } else {
        force.setMag(0.1); // Reduced force to prevent overshooting
        this.acceleration.add(force);
      }
```

Esta es una ligera exepcion a la norma puesto que para el ejercicio anterior aplique el marco de movimiento 101 pero tambien estaba organizando el movimiento teniendo en cuenta elementos de las fuerzas

# Como se definiran ahora las leyes de newton

Ahora la forma en la que se calculara la aceleracion sera con la ley de newton y teniendo en cuenta los elementos de la computacion (Despues de cada update la aceleracion sera 0, la importancia de hacer un copy de la fuerza que vamos a ejercerle a multiples objetos). Esto tiene una gran correlacion con las leyes de movimiento de newton ya que vamos a utilziar principalmente la sumatoria de fuerzas para actualizar las posiciones y la velocidad de nuestros diferentes objetos

