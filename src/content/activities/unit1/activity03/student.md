# Actividad 03

## Experimento
Voy a modificar el algoritmo de caminata para que solamente se pueda desplazar en diagonales

## ¿Qué pregunta quieres responder con este experimento?
Que maneras tengo de alterar el algoritmo de moviemiento? Puedo moverme en mas que solo 4 axis?

## Que resultados esperas obtener?
Poder testear los limites de en cuantos ejes de movimiento podria hacer que el algoritmo navegue

## Que resultados obtuviste?
El limite de ejes de movimiento actualmente son 8: Arriba, Abajo, Izquierda, Derecha, Diagonal Arriba Derecha, Diagonal Abajo Derecha, Diagonal Arriba Izquierda, Diagonal Abajo Izquierda

## ¿Qué aprendiste de este experimento?
Aprendi como mediante un algortimo sencillo y la eleccion randomizada de valores puedo generar una pseudo imagen al azar. Coincidencialmente podria tambien manipular esas probabilidades para cambiar el resultado en pantalla y generar una imagen mas parametrizada a algo que yo quiera decidir.

``` js
class Walker {
  // Objects have a constructor where they are initialized.
  constructor() {
    // Objects have data.
    this.x = width / 2;
    this.y = height / 2;
  }

  // Objects have methods.
  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    //{!1} 0, 1, 2, or 3. The random choice determines the step.
    let choice = floor(random(8));
    if (choice === 0) {
      this.x++;
      this.y++;
    } else if (choice === 1) {
      this.x--;
      this.y--;
    } else if (choice === 2) {
      this.y++;
      this.x--;
    } else if (choice === 3) {
      this.y--;
      this.x++;
    } else if (choice === 4){
      this.x++;
    } else if (choice === 5){
      this.y++;
    } else if (choice === 6){
      this.x--;
    } else if (choice === 7){
      this.y--;
    }
    
  }
}

//{!1} Remember how p5.js works? setup() is executed once when the sketch starts.
function setup() {
  createCanvas(640, 240);
  // Create the walker.
  walker = new Walker();
  background(255);
}

//{!1} Then draw() loops forever and ever (until you quit).
function draw() {
  // Call functions on the walker.
  walker.step();
  walker.show();
}
```
