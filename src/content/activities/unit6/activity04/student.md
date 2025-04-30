## 1 Eleccion

Trabajare con ambas, flocking me gusto mucho mucho pero quiero usar flow sistems para recrear un viento cool

## 2 Brainstorming

Mi idea sera utilizar flow sistems para crear un visual de viento y hacer un sistema de flocking para representar aves atravesando ese viento, adicionalmente me gustaria que los boids tengan una pequeña interaccion con el viento en que los aparten de su camino.

## 3 Diseño del codigo

Empleare el flow sistem del ejemplo pasado y lo modificare un poco para simular vientos. Adicionalmente voy a utilizar flocking para hacer las aves moviendose atravez de todo, modificare las reglas del flock para que sean varias bandadas de pajaros en vez de una grande y adicionalmente les agregare esa posible interaccion con el viento para que lo empujen un poco hacia los lados al atravesarlo.

Idealmente hare que el viento sea azul y en forma de triangulo muy muy delgado y que las aves sean triangulos de varios colores (a exepcion de azul) y todo esto sobre un fondo celeste como si fuera un cielo

## 4 Implementacion del codigo


BIRDS IN THE WIND

boid.js
```js
class Boid {
  constructor(x, y, color) {
    this.acceleration = createVector(0, 0);
    this.velocity = p5.Vector.random2D();
    this.position = createVector(x, y);
    this.maxspeed = 2.5;
    this.maxforce = 0.05;
    this.color = color;
    this.r = 3;
  }
  
  separate(boids) {
  let desiredSeparation = 25;
  let steer = createVector(0, 0);
  let count = 0;

  for (let other of boids) {
    let d = p5.Vector.dist(this.position, other.position);
    if (d > 0 && d < desiredSeparation) {
      let diff = p5.Vector.sub(this.position, other.position);
      diff.normalize();
      diff.div(d); // Más lejos, menos efecto
      steer.add(diff);
      count++;
    }
  }

  if (count > 0) {
    steer.div(count);
  }

  if (steer.mag() > 0) {
    steer.normalize();
    steer.mult(this.maxspeed);
    steer.sub(this.velocity);
    steer.limit(this.maxforce);
  }
  return steer;
}

  align(boids) {
  let neighborDist = 50;
  let sum = createVector(0, 0);
  let count = 0;
  for (let other of boids) {
    let d = p5.Vector.dist(this.position, other.position);
    if (d > 0 && d < neighborDist) {
      sum.add(other.velocity);
      count++;
    }
  }

  if (count > 0) {
    sum.div(count);
    sum.normalize();
    sum.mult(this.maxspeed);
    let steer = p5.Vector.sub(sum, this.velocity);
    steer.limit(this.maxforce);
    return steer;
  } else {
    return createVector(0, 0);
  }
}

  cohere(boids) {
  let neighborDist = 50;
  let sum = createVector(0, 0);
  let count = 0;
  for (let other of boids) {
    let d = p5.Vector.dist(this.position, other.position);
    if (d > 0 && d < neighborDist) {
      sum.add(other.position);
      count++;
    }
  }

  if (count > 0) {
    sum.div(count);
    return this.seek(sum);
  } else {
    return createVector(0, 0);
  }
}
  
seek(target) {
  let desired = p5.Vector.sub(target, this.position);
  desired.normalize();
  desired.mult(this.maxspeed);
  let steer = p5.Vector.sub(desired, this.velocity);
  steer.limit(this.maxforce);
  return steer;
}



  applyForce(force) {
    this.acceleration.add(force);
  }

  applyWind(wind) {
    let windEffect = wind.copy().mult(0.3); // sutil
    this.applyForce(windEffect);
  }

  flock(boids) {
    let sep = this.separate(boids).mult(1.5);
    let ali = this.align(boids).mult(1.0);
    let coh = this.cohere(boids).mult(1.0);
    this.applyForce(sep);
    this.applyForce(ali);
    this.applyForce(coh);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.maxspeed);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    fill(this.color);
    stroke(0);
    push();
    translate(this.position.x, this.position.y);
    rotate(this.velocity.heading());
    beginShape();
    vertex(this.r * 2, 0);
    vertex(-this.r * 2, -this.r);
    vertex(-this.r * 2, this.r);
    endShape(CLOSE);
    pop();
  }

  borders() {
    if (this.position.x < -this.r) this.position.x = width + this.r;
    if (this.position.y < -this.r) this.position.y = height + this.r;
    if (this.position.x > width + this.r) this.position.x = -this.r;
    if (this.position.y > height + this.r) this.position.y = -this.r;
  }

  run(boids, flowField) {
    this.flock(boids);
    let wind = flowField.lookup(this.position);
    this.applyWind(wind);
    this.update();
    this.borders();
    this.show();
  }

  // Métodos: align, cohere, separate... mismos que ya tenías.
}

```

flock.js
```js
class Flock {
  constructor(num, colorPalette) {
    this.boids = [];
    for (let i = 0; i < num; i++) {
      let color = random(colorPalette);
      this.boids.push(new Boid(random(width), random(height), color));
    }
  }

  run(allBoids, flowField) {
    for (let b of this.boids) {
      b.run(allBoids, flowField); // usa todos los boids visibles
    }
  }

  getBoids() {
    return this.boids;
  }
}

```

flowfield.js
```js
class FlowField {
  constructor(resolution) {
    this.resolution = resolution;
    this.cols = floor(width / this.resolution);
    this.rows = floor(height / this.resolution);
    this.field = this.make2DArray(this.cols);
    this.initNoise();
  }

  make2DArray(cols) {
    let arr = new Array(cols);
    for (let i = 0; i < cols; i++) {
      arr[i] = [];
    }
    return arr;
  }

  initNoise() {
    let xoff = 0;
    for (let i = 0; i < this.cols; i++) {
      let yoff = 0;
      for (let j = 0; j < this.rows; j++) {
        let theta = noise(xoff, yoff) * TWO_PI * 2;
        this.field[i][j] = p5.Vector.fromAngle(theta);
        yoff += 0.1;
      }
      xoff += 0.1;
    }
  }

  lookup(lookup) {
    let column = constrain(floor(lookup.x / this.resolution), 0, this.cols - 1);
    let row = constrain(floor(lookup.y / this.resolution), 0, this.rows - 1);
    return this.field[column][row].copy();
  }

  display() {
    stroke(0, 50, 255, 50);
    strokeWeight(1);
    for (let i = 0; i < this.cols; i++) {
      for (let j = 0; j < this.rows; j++) {
        let x = i * this.resolution;
        let y = j * this.resolution;
        push();
        translate(x, y);
        rotate(this.field[i][j].heading());
        triangle(0, 0, 10, -2, 10, 2); // viento como triángulo fino
        pop();
      }
    }
  }
}

```

sketch.js
```js
let flowField;
let flocks = [];

function setup() {
  createCanvas(800, 600);
  background(200, 220, 255); // cielo celeste
  flowField = new FlowField(20);

  let palette = ['#FF595E', '#FFCA3A', '#8AC926', '#1982C4', '#6A4C93'];
  for (let i = 0; i < 3; i++) {
    flocks.push(new Flock(30, palette));
  }
}

function draw() {
  background(200, 220, 255, 40); // Cielo con leve rastro
  flowField.display();

  let allBoids = flocks.flatMap(f => f.getBoids());

  for (let flock of flocks) {
    flock.run(allBoids, flowField);
  }
}

```


## 5 Prueba Final

![image](https://github.com/user-attachments/assets/8d2323c0-91d2-49cb-a48c-ebf652e58f7d)

Link del sketch aca [>.<](https://editor.p5js.org/MateoJimenezFamaArt/sketches/SSC6ALePe)
