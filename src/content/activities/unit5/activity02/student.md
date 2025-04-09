🧐🧪✍️ En tu bitácora responde a esta pregunta para cada una de las simulaciones: ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

📤 Entrega:

Vas a modificar cada una de las simulaciones anteriores incluyen en cada una, al menos un concepto de las unidades anteriores, pero no repitas concepto, la idea es que repases al menos uno de cada unidad.
Vas a gestionar la creación y la desaparición de las partículas y la memoria. Explica cómo lo hiciste.
Explica qué concepto aplicaste, cómo lo aplicaste y por qué.
Incluye un enlace a tu código en el editor de p5.js.
Incluye el código fuente de cada una de las simulaciones.
Captura de pantallas de cada una de las simulaciones con las imágenes que más te gusten como resultado de la ejecución de cada una de las simulaciones.


## 1. Array de particulas

La creacion y destruccion de las particulas se gestiona mediante un array el cual lleva registro de cada que una particula se crea o destruye, cuando una particula  cumple su tiempo de vida ya se elimina del array con un splice() haciedno que este metodo permita a cada particula tener su tiempo de vida y luego desaparecer librando espacio para las siguientes

Aca implemente el concepto de la onda sin, esto para que el valor de X oscile entre los posibles valores de esta onda para que las particulas se vayan regando en un patron interesante y organico. La creacion y desaparicion se mantiene igual, he aplicado este concepto ya que me llamaba la atencion la idea de que las particulas se fueran moviendo como si fuera una cortinilla de lluvia. 

### Codigo

```js
let particles = [];
let t = 0; // time variable for sine wave

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);

  // Calculate x using sine wave
  let amplitude = width / 3; // how wide the sine wave is
  let frequency = 0.05; // how quickly it oscillates
  let x = width / 2 + sin(t) * amplitude;
  let y = 20;

  particles.push(new Particle(x, y));

  // Update time
  t += frequency;

  // Looping through backwards to delete
  for (let i = particles.length - 1; i >= 0; i--) {
    let particle = particles[i];
    particle.run();
    if (particle.isDead()) {
      particles.splice(i, 1);
    }
  }
}

```

### Haz click aqui (>.<)[https://editor.p5js.org/MateoJimenezFamaArt/sketches/RktWYHx6b]

### Captura de pantalla
![image](https://github.com/user-attachments/assets/1c240185-0e97-4632-96a7-4dcac291b65f)


________________________________________________________________________________________________________________________________________________________

## 2. Sistema de emisores

La creacion de las particulas en este sistema es particular, puesto que lo que hacemos no es crear las particulas directamente si no que hacemos emisores que crean las particulas como tal. Sin embargo hay que ser cuidadosos en este caso pues los emisores en esta simulacion no tienen un stopping point por lo que generaran particulas infinitamente y eso se presta para problemas, una posible forma de manejarlo seria que produzcan una cantidad fija de particulas y luego dejen de existir.

Aca quiero implementar el concepto de el ruido perlin, que los emisores produzcan particulas segun un valor derivado del perlin y de esta manera habran unos que duren mucho mas y otro mucho menos pero de manera muy organica.

### Codigo

```js
class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
    this.noiseOffset = random(1000); // separate noise seed for each emitter
  }

  addParticle() {
    // Calculate max particles based on Perlin noise
    let noiseVal = noise(this.noiseOffset);
    let maxParticles = floor(map(noiseVal, 0, 1, 10, 100)); // you can tweak this range

    // Only add a new particle if we haven't reached the max
    if (this.particles.length < maxParticles) {
      this.particles.push(new Particle(this.origin.x, this.origin.y));
    }

    // Advance the noise offset slowly
    this.noiseOffset += 0.01;
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      this.particles[i].run();
      if (this.particles[i].isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

```
Modificamos la clase emitter para que solo produzca particulas segun el valor en perlin

### Link de simulacion (>.<)[https://editor.p5js.org/MateoJimenezFamaArt/sketches/6K-JiU6ez]

### Captura de pantalla
![image](https://github.com/user-attachments/assets/e24ccd00-3b6f-4aa1-9ad9-9ac442630244)

________________________________________________________________________________________________________________________________________________________

## 3. Sistema de Polimorfismos

En este sistema se emplea algo similar al anterior ya que es el emsior el que se encarga de crear particulas sin embargo ahora lo que se hace es que primero solo hay un emisor y segundo todas las particulas se manejan utilizando el metodo de la lista que vimos mas arriba con el fin de que se sostenga en el tiempo como un proceso optimo.

Aca quiero implementar el concepto de la distribucion gaussiana para que sea mas probable que salga confeti a que salga la particula normal por ejemplo

### Codigo 

```js
class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    // Use a Gaussian distribution and bias it
    let gaussian = randomGaussian(); // mean = 0, stddev = 1
    let r = gaussian + typeBias; // shift it based on user input

    // Normalize it to a usable decision
    if (r < 0) {
      this.particles.push(new Particle(this.origin.x, this.origin.y));
    } else {
      this.particles.push(new Confetti(this.origin.x, this.origin.y));
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.run();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

```

Modificamos la clase emmiter para usar gaussian y en el main hicimos lo siguiente

```js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

// Particles are generated each cycle through draw(),
// fall with gravity and fade out over time
// A ParticleSystem object manages a variable size
// list of particles.


let typeBias = 0; // 0 = neutral, >0 = more confetti, <0 = more particles
let emitter;

function setup() {
  createCanvas(640, 240);
  emitter = new Emitter(width / 2, 20);
}

function draw() {
  background(255);
  emitter.addParticle();
  emitter.run();
}

function keyPressed() {
  if (key === 'C') {
    typeBias = constrain(typeBias + 0.5, -2, 2); // tilt toward Confetti
  } else if (key === 'P') {
    typeBias = constrain(typeBias - 0.5, -2, 2); // tilt toward Particle
  }
}
```
Con esto podemos controlar si queremos mas confeti o mas particualas ehehe

### Link de simulacion (>.<)[https://editor.p5js.org/MateoJimenezFamaArt/sketches/rDHBxAXC6]

### Captura de pantalla

![image](https://github.com/user-attachments/assets/65a590e4-b794-40f4-a17e-25c606cfc1d9)


________________________________________________________________________________________________________________________________________________________

## 4. Sistema de Particulas con Fuerzas

Se emplea el mismo metodo de aggar particulas a un array y luego de agregarlos cuando cumple su tiempo de vida y muere se le hace un splice() para salir del array

En este sistema quiero Implementar el concepto de rebote, que las particulas puedan rebotar una con la otra de una manera fisica con fuerzas, asi que haremos que las particulas reboten entre si

### Code

```js
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-2, 0));
    this.lifespan = 255.0;
    this.mass = 1; // You could randomize this for fun
    this.radius = 8; // For collision detection
  }

  run(particles) {
    this.update();
    this.checkCollisions(particles);
    this.show();
  }

  applyForce(force) {
    let f = force.copy().div(this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    this.lifespan -= 2.0;
  }

  checkCollisions(particles) {
    for (let other of particles) {
      if (other === this) continue;

      let dir = p5.Vector.sub(other.position, this.position);
      let dist = dir.mag();
      let minDist = this.radius;

      if (dist < minDist && dist > 0) {
        // Normalize the direction
        dir.normalize();

        // Push them apart (simple positional correction)
        let overlap = minDist - dist;
        this.position.sub(p5.Vector.mult(dir, overlap / 2));
        other.position.add(p5.Vector.mult(dir, overlap / 2));

        // Calculate relative velocity
        let relativeVel = p5.Vector.sub(this.velocity, other.velocity);
        let speed = relativeVel.dot(dir);

        if (speed < 0) continue; // Already moving apart

        // Calculate impulse scalar
        let impulse = (2 * speed) / (this.mass + other.mass);

        // Apply impulse
        this.velocity.sub(p5.Vector.mult(dir, impulse * other.mass));
        other.velocity.add(p5.Vector.mult(dir, impulse * this.mass));
      }
    }
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, this.radius);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

```

Cambios principalmente en partciles para que se reboten entre si

### Link to the code (>.<)[editor.p5js.org/natureofcode/sketches/uZ9CfjLHL]

### Screenshot

![image](https://github.com/user-attachments/assets/b1531826-b469-4436-aacc-8154e953005b)


________________________________________________________________________________________________________________________________________________________

## 5. Particle Sistem with a repeller

En este sistema se maneja el mismo tipo de creacion y destruccion de particulas que en los pasados

En este sistema quiero implementar el concepto de una fuerza de viento empujando a las particulas al repeller

### Code

```js
let emitter;
let repeller;

function setup() {
  createCanvas(640, 240);

  // Emit particles from the far right
  emitter = new Emitter(width/2, height / 2);

  // Place the repeller on the far left
  repeller = new Repeller(40, height / 2);
}
function draw() {
  background(255);

  // Move the repeller to follow the mouse
  repeller.position.set(mouseX, mouseY);

  // Add a new particle every frame
  emitter.addParticle();

  // Gravity
  let gravity = createVector(0, 0.1);
  emitter.applyForce(gravity);

  // Wind (visual + functional)
  let wind = createVector(-0.05, 0);
  emitter.applyForce(wind);

  // ✨ Show the wind force visually
  drawVector(wind, createVector(width - 60, height - 40), 500);

  // Repeller effect
  emitter.applyRepeller(repeller);

  // Run particles
  emitter.run();

  // Show repeller
  repeller.show();
}

function drawVector(v, pos, scale = 1) {
  push();
  let arrowSize = 4;
  translate(pos.x, pos.y);
  stroke(0);
  strokeWeight(2);
  fill(0);
  rotate(v.heading());
  let len = v.mag() * scale;
  line(0, 0, len, 0);
  translate(len, 0);
  triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
  pop();
}

```

### Link to the code (>.<)[https://editor.p5js.org/MateoJimenezFamaArt/sketches/U2jDnsLKi]

### Screenshot 
![image](https://github.com/user-attachments/assets/3faf3f5a-b330-4fec-8d35-afc0d38f79ac)
