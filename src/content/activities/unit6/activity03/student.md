Explica con tus palabras el objetivo y la lógica general de cálculo de cada una de las tres reglas de Flocking (Separación, Alineación, Cohesión).
Lista los parámetros clave identificados (radio de percepción, pesos de las reglas, maxspeed, maxforce).
Describe la modificación que realizaste al código y explica detalladamente el efecto que tuvo en el comportamiento colectivo del enjambre (¿se dispersan? ¿forman grupos compactos? ¿se mueven caóticamente?). Incluye una captura de pantalla o GIF si ilustra bien el cambio. Muestra el fragmento de código modificado.


## Explicacion del objetivo y la logica general

Separacion : La regla de separacion tiene como objetivo evitar que los vehiculos esten montandose uno sobre el otro constantemente y que se sobrepongan. Su logica se radica en cambiar la direccion a otra opuesta cuando esta demasiado cerca de otro boid

Alineacion : La regla de alineacion tiene como objetivo simular ese comportamiento de enjambre en el cual se mueven un union hacia un objetivo en particular. Su logica radica en que todo el flock este siguiendo el mismo vector director en ciertos momentos.

Cohesion : La regla de cohesion tiene como objetivo simular ese comportamiento de manada en el cual se mueven estando cerca los unos de los otros. Su logica radica en que haya un radio y en ese radio se aplican las otras dos reglas para lograr esa uniformidad.

## Parametros clave identificados

Radio de percepcion : El radio bajo el cual se empiezan a aplicar las reglas del flocking

Pesos de las reglas : Estos valores determinan que tanta influencia tienen las reglas, si se modifican puede hacer que sea una manada mas uniforme, mas montonera o mas caotica en su movimiento

maxSpeed y maxForce : Son los valores que modifican la velocidad y los cambios que adn los boids al moverse

## Modificacion

Para modificar el codigo y que sea mas interesante le agregue un metodo llamado scatter

```js
  scatter() {
    // Movimiento aleatorio fuerte para dispersión
    let chaos = p5.Vector.random2D();
    chaos.mult(this.maxspeed * 2);
    let steer = p5.Vector.sub(chaos, this.velocity);
    steer.limit(this.maxforce * 3);
    this.applyForce(steer);
  }
```

Con este metodo lo que lgoramos es simular como si a la bandada de pajaros les tiramos una piedra, esto hace que todos salgan dispersos a diferentes lados como locos y ya luego se reunen nuevamente. 

![image](https://github.com/user-attachments/assets/d63f0bb0-66ef-4e70-935f-c81ac700791b)

(Pobres pajaritos me hiciste tirarles piedras >.<)
