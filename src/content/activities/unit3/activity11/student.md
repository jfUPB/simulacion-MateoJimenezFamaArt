# Entrega

## Codigo

```js
let particles = [];
let blackHole;
let G = 5; // Constante gravitacional elevada para simular el agujero negro
let lightBeams = [];

function setup() {
  createCanvas(800, 600);
  blackHole = new BlackHole(width / 2, height / 2, 1000);
  for (let i = 0; i < 100; i++) {
    particles.push(new Particle(random(width), random(height), random(2, 10)));
  }
  for (let i = 0; i < 50; i++) {
    lightBeams.push(new LightBeam(random(width), random(height)));
  }
}

function draw() {
  background(0);
  blackHole.display();
  blackHole.pullParticles(particles);
  blackHole.bendLight(lightBeams);
  for (let particle of particles) {
    particle.update();
    particle.display();
  }
  for (let beam of lightBeams) {
    beam.update();
    beam.display();
  }
}

class BlackHole {
  constructor(x, y, mass) {
    this.position = createVector(x, y);
    this.mass = mass;
  }

  pullParticles(particles) {
    for (let particle of particles) {
      let force = p5.Vector.sub(this.position, particle.position);
      let distanceSq = constrain(force.magSq(), 100, 5000);
      let strength = (G * this.mass * particle.mass) / distanceSq;
      force.setMag(strength);
      particle.applyForce(force);
    }
  }

  bendLight(beams) {
    for (let beam of beams) {
      let force = p5.Vector.sub(this.position, beam.position);
      let distanceSq = constrain(force.magSq(), 100, 5000);
      let strength = this.mass / distanceSq * 100; // Ajuste para curvar los rayos de luz
      force.setMag(strength);
      beam.applyForce(force);
    }
  }

  display() {
    push();
    translate(this.position.x, this.position.y);
    fill(0);
    noStroke();
    ellipse(0, 0, 100); // Agujero negro
    pop();
  }
}

class Particle {
  constructor(x, y, mass) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-2, 2), random(-2, 2));
    this.acceleration = createVector(0, 0);
    this.mass = mass;
  }

  applyForce(force) {
    let f = force.copy();
    f.div(this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  display() {
    fill(255);
    noStroke();
    ellipse(this.position.x, this.position.y, this.mass * 2); // Partículas
  }
}

class LightBeam {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(5, 0); // Luz viajando a velocidad constante
    this.acceleration = createVector(0, 0);
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  display() {
    stroke(255, 255, 0);
    strokeWeight(2);
    point(this.position.x, this.position.y); // Representar la luz como un punto
  }
}
```


## Como se modelo?
Para modelar este cuerpo de los N cuerpos diseñe un sistema ne el cual hay un agujero negro, un cuerpo principal el cual esta absorbiendo diferentes particulas que tambien se atraen entre si, el agujero negro no se mueve pues es demasiado robusto para ser movido sin embargo a su alrededor todo es un caos por que todos se intentan atraer entre si mientras se estan atrayendo a el agujero negro en el centro

## Link
[Link del Sketch](https://editor.p5js.org/MateoJimenezFamaArt/sketches/Qvb4F5mXW)

## Imagen
![Captura del Modelo](https://github.com/user-attachments/assets/a4de3b16-de42-4838-a3a5-e8d0f2595ffa)
