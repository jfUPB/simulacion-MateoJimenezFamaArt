## Enlace de Simulacion

Haz click aca [>.<](https://editor.p5js.org/MateoJimenezFamaArt/sketches/8WA48zPSg)

## Codigo de la simulacion

``` js
let vehicle;

function setup() {
  createCanvas(800, 600); // Crear un lienzo de 800x600
  vehicle = new Vehicle(width / 2, height / 2); // Colocar el vehículo en el centro
}

function draw() {
  background(255);

  vehicle.update(); // Actualizar la posición y la velocidad del vehículo
  vehicle.display(); // Mostrar el vehículo en pantalla
}

function keyPressed() {
  if (keyCode === RIGHT_ARROW) {
    vehicle.turn(0.1); // Girar hacia la derecha
  } else if (keyCode === LEFT_ARROW) {
    vehicle.turn(-0.1); // Girar hacia la izquierda
  }
}

class Vehicle {
  constructor(x, y) {
    this.position = createVector(x, y); // Posición del vehículo
    this.velocity = createVector(0, 0); // Velocidad del vehículo
    this.acceleration = createVector(0, 0); // Aceleración del vehículo
    this.angle = 0; // Ángulo del vehículo
    this.r = 20; // Radio del vehículo (tamaño)
  }

  update() {
    this.velocity.add(this.acceleration); // Agregar aceleración a la velocidad
    this.position.add(this.velocity); // Mover la posición del vehículo según la velocidad

    // Limitar la velocidad máxima del vehículo
    this.velocity.limit(5);

    // Frenar la aceleración
    this.acceleration.mult(0);

    // Mantener el vehículo dentro de la pantalla
    this.position.x = (this.position.x + width) % width;
    this.position.y = (this.position.y + height) % height;
  }

  applyForce(force) {
    this.acceleration.add(force); // Aplicar fuerza como aceleración
  }

  turn(angle) {
    this.angle += angle; // Girar el ángulo del vehículo
    this.velocity = p5.Vector.fromAngle(this.angle); // Ajustar la velocidad según el ángulo
  }

  display() {
    let angle = this.velocity.heading();

    stroke(0);
    strokeWeight(2);
    fill(127);
    push();
    translate(this.position.x, this.position.y); // Mover a la posición del vehículo
    rotate(this.angle); // Rotar según la dirección del vehículo
    // Dibujar un triángulo que representa el vehículo
    beginShape();
    vertex(this.r, 0); // Vértice frontal
    vertex(-this.r, this.r / 2); // Vértice trasero izquierdo
    vertex(-this.r, -this.r / 2); // Vértice trasero derecho
    endShape(CLOSE);
    pop();
  }
}
```

## Imagen de Simulacion

![image](https://github.com/user-attachments/assets/51032c13-d821-4696-9551-f10e19682aec)
