# Que esta mal de ese planteamiento?

Resulta que cuando llamamos el applyForce(wind) y luego el gravity, por la forma en que esta escrito estariamos remplazando una de las fuerzas X la otra, entonces si hacemos primero wind y luego gravity la fuerza del viento no se estaria teniendo en cuenta ya que no se estaria sumando a las fuerzas totales, seria mejor plantearlo de tal forma en que uno pueda agregar varias fuerzas a una lista y luego sumarlas todas juntas para calcular el movimiento.
Para implementarlo en p5.js seria algo como:

``` js
//Para el apply force

applyForce(force){
this.acceleration.add(force);
}

//Esto para que las fuerzas sean cumulativas y luego en el update

update(){
...
...
...
...

//Luego de realizar todo el movimeinto se debe hacer un
this.acceleration.mul(0);

//Esto para limpiar la acceleracion de los objetos despues de cada frame para que se pueda recalcular nuevamente
}
```
