# Explicacion del ejemplo

Se entiende que se esta creando una clase mover el cual tiene tres metodos, uno para revisar si toca la pared, al hacerlo volvera a aparecer en la pared contraria. Se utiliza un metodo show para en este caso dibujar un circulo con el fin de poder ver el objeto que estamos movilziando. Ya por ultimo tenemos el metodo que calcula la sumatoria en este caso se llama Update. 

# Que pasaria si?

Que pasaria si en vez de cambiar la ubicacion en la pantalla el codigo hiciera que el objeto cambiara su direccion como si estuviera rebotando contra los bordes?

## Codigo

``` js
// Declare the Mover object.
let mover;

function setup() {
  createCanvas(640, 240);
  // Create the Mover object.
  mover = new Mover();
}

function draw() {
  background(255);
  // Call methods on the Mover object.
  mover.update();
  mover.checkEdges();
  mover.show();
}

class Mover {
  constructor() {
    // The object has two vectors: position and velocity.
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(random(-2, 2), random(-2, 2));
  }

  update() {
    // Motion 101: position changes by velocity.
    this.position.add(this.velocity);
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 48);
  }

  checkEdges() {
    if (this.position.x >= width || this.position.x <= 0) {
      this.velocity.x *= -1; // Reverse X direction
    }

    if (this.position.y >= height || this.position.y <= 0) {
      this.velocity.y *= -1; // Reverse Y direction
    }
  }
}

```

Me imagino que a la hora de llegar a los bordes la pelotica que henmos dibujado hara un rebote y se direccionara hacia otro lado y todo esto por que simplemente comenzamos a multiplicar su vector de velocidad por -1, esto haciendo pues que gracias a la naturaleza del vector se vea como un rebote.

Sucedio justo lo que pense, aunque la pelota se mueve muy lento y se alcanza a meter media pelota al borde antes de realizar el rebote.

Esto ocurre por que en el momento en que la posicion de la pelota llega a uno de los bordes estamos multiplicando su vector velocidad por -1 haciendo que la direccion que estaba tomando se convierta en -1

En conclusion el movimiento propuesto por Motion 101 puede servirnos mucho y mas aun si le agregamos la complijdad de otros elementos como lo son el rozamiento de la superficie en la cual se mueve y la aceleracion que nuestr objeto en cuestion llegara a tener.

