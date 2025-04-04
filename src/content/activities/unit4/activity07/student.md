## Enlace a la simulacion

Haz click aca [>.<](https://editor.p5js.org/MateoJimenezFamaArt/sketches/_FHOheIT9)

## Codigo :D

```js
class Oscillator {
  constructor() {
    // Ángulos iniciales en 0
    this.angle = createVector();
    
    // Velocidad angular aleatoria
    this.angleVelocity = createVector(random(-0.05, 0.05), random(-0.05, 0.05));
    
    // Amplitud aleatoria
    this.amplitude = createVector(random(20, width / 2), random(20, height / 2));
    
    // Fuerza de rozamiento (un valor cerca de 1 para que disminuya lentamente)
    this.friction = 0.99;
    
    // Fuerza del viento, una pequeña constante que empuja hacia la derecha
    this.windForce = createVector(0.001, 0);
  }

  update() {
    // Aplicar rozamiento para reducir la velocidad angular
    this.angleVelocity.mult(this.friction);

    // Aplicar el viento (empuja hacia la derecha en el eje x)
    this.angleVelocity.add(this.windForce);

    // Actualizar el ángulo
    this.angle.add(this.angleVelocity);
  }

  show() {
    // Calcular la posición x y y basados en los ángulos
    let x = sin(this.angle.x) * this.amplitude.x;
    let y = sin(this.angle.y) * this.amplitude.y;

    // Dibujar el oscilador
    push();
    translate(width / 2, height / 2);
    stroke(0);
    strokeWeight(2);
    fill(127);
    line(0, 0, x, y);
    circle(x, y, 32);
    pop();
  }
}

let oscillators = [];

function setup() {
  createCanvas(800, 600);
  
  // Crear múltiples osciladores con diferentes propiedades
  for (let i = 0; i < 10; i++) {
    oscillators.push(new Oscillator());
  }
}

function draw() {
  background(255);
  
  // Actualizar y mostrar cada oscilador
  for (let osc of oscillators) {
    osc.update();
    osc.show();
  }
}
```

## Caputra de Pantalla
![image](https://github.com/user-attachments/assets/b769d3d8-0131-40d1-bd0b-34fcd2e98a06)

