# Teoria
Para modelar las sigueintes fuerzas:

Friccion
Resistencia del aire y fluidos
Atraccion gravitacional

Se deben primero definir las formulas de estos.

Vamos a ver como se escribe cada formula 

Friccion
![image](https://github.com/user-attachments/assets/19084b24-8f9a-4ab0-89ed-56d9525a5a96)

Ressitencia
![image](https://github.com/user-attachments/assets/06e0a734-807e-4702-b261-86e5b3d40815)

Atraccion Gravitacional
![image](https://github.com/user-attachments/assets/3354f986-d093-499a-9b59-312e36f5660a)


Como podemos ver las formulas para entender estos movimientos varian en complejidad, pero mas alla que simplemente entender las formulas debemos entender como se han de mover estos elementos.

Primero la friccion, es una fuerza opuesta a un movimiento en una superficie, o sea que si me estoy moviendo a la derecha deberia haber una fuerza a la izquierda que me este deteniendo lentamente

Segundo la resistencia, en una resistencia sea de fluido o de aire mi objeto deberia ir perdiendo velocidad mientras mas se mueva en ese medio esto se debe a que el aire o el fluido estan retrasando y absorbiendo energia de nuestro objeto, si la friccion enviaba fuerza a la direccion contraria en la superficie de desplazamiento la de restencia tendra como objetivo hacer que nuestor objeto pierda fuerza segun la direccion que tome 

Tercer la atraccion gravitacional, en esta fuerza es algo mas interesante ya que dependera de como se utilice, si hacemos un punto invisible que atraera a algun otro objeto, podremos ver como este se acerca a gran velocidad hacia nuestro punto invisible pero en el momento en que lo sobre pase entonces este va a atravesarlo y se comenzara a alejar de nuestro punto invisible por ende la fuerza que en algun momento fue digamos positiva hacia el punto invisible ahora se estara volviendo una fuerza negativa para que el objeto no vaya a aseguir su trayectoria si no que vaya a pegarse en el punto invisible. Basicamente es como una relacion toxica, te va a acercar muchsimo muchismo y no te va a dejar ir cuando ya te hayas estrellado contra ella.

# Como se modela cada una?

Para la de friccion vamos a realizar un codigo en el cual haya un "carro" al cual le podemos dar velocidad oprimiendo flecha hacia arriba, en el momento en el que oprimamos La barra espaciadora la pista que no tenia friccion comenzara a tener friccion y esta hara que el carro vaya perdiendo fuerza.

Para la de Resistencia vamos a hacer un objeto que intente seguir el mouse, ciertas secciones de la pantalla tendran viento y otras tendran miel, si el objeto pasa por esas secciones debera ser sometido a la fuerza de arrastre de estos al intentar seguir el mouse

Para la de atraccion gravitacional vamos a hacer un sistema visual de un atomo y usaremos la fuerza de atraccion para mostrar como los electrones orbitan alrededor de los neutrones y protones. (Si bien esto cientificamente no es cierto puesto que los atomos tienen su movimiento gracias a las fuerzas de atraccion y repulsion de energias positivas y negativas, podemos utilizar el modelo de la fuerza gravitacional para al canzar una representacion grafica interesante)


# Codigos:

1. Friccion

```js
let mover;
let braking = false;
let frictionless = true; // Estado de la pista

function setup() {
  createCanvas(800, 400);
  mover = new Mover();
}

function draw() {
  background(220);
  drawRoad();
  if (braking) {
    mover.applyFriction();
    frictionless = false; // Si se frena, la pista tiene fricción
  }
  mover.update();
  mover.display();
  displayInstructions();
}

function keyPressed() {
  if (key === ' ') {
    braking = true;
  }
  if (keyCode === UP_ARROW) {
    mover.applyForce(createVector(2, 0)); // Aplicar fuerza para acelerar el carro
  }
}

function keyReleased() {
  if (key === ' ') {
    braking = false;
    frictionless = true; // La pista vuelve a ser sin fricción
  }
}

class Mover {
  constructor() {
    this.position = createVector(50, height / 2);
    this.velocity = createVector(5, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
  }

  applyForce(force) {
    let f = force.copy();
    f.div(this.mass);
    this.acceleration.add(f);
  }

  applyFriction() {
    let friction = this.velocity.copy();
    friction.normalize();
    friction.mult(-1);

    let normalForce = 1; // Fuerza normal para simplificar
    let mu = braking ? 0.3 : 0; // Ficción solo si frenamos
    friction.setMag(mu * normalForce);

    this.applyForce(friction);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0); // Reiniciar aceleración

    if (this.position.x > width + 40) { // Cuando salga de la pantalla
      this.position.x = -40; // Reiniciar al otro lado
    }
  }

  display() {
    fill(127);
    rect(this.position.x, this.position.y - 20, 60, 40); // Dibujar "carro"
  }
}

function drawRoad() {
  if (frictionless) {
    fill(0, 255, 255); // Azul cyan si no hay fricción
  } else {
    fill(128, 0, 0); // Vinotinto oscuro si hay fricción
  }
  rect(0, height / 2 + 20, width, 10); // Dibujar "carretera"
}

function displayInstructions() {
  fill(0);
  textSize(16);
  textAlign(CENTER);
  text("Presiona ESPACIO para frenar, FLECHA ARRIBA para acelerar", width / 2, 30);
}

```
([Link del Sketch de friccion](https://editor.p5js.org/MateoJimenezFamaArt/sketches/Z6qCpJx_y))

2 Arrastre o Drag

```js
let mover;

function setup() {
  createCanvas(800, 400);
  mover = new Mover();
}

function draw() {
  background(220);
  drawSections();
  mover.applyInput(); // Ahora sigue un input para moverse
  mover.update();
  mover.display();
  displayInstructions(); // Mostrar instrucciones
}

class Mover {
  constructor() {
    this.position = createVector(50, 50);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
  }

  applyForce(force) {
    let f = force.copy();
    f.div(this.mass);
    this.acceleration.add(f);
  }

  applyInput() {
    let force = createVector(0, 0);
    if (keyIsDown(LEFT_ARROW)) {
      force.add(createVector(-0.1, 0));
    }
    if (keyIsDown(RIGHT_ARROW)) {
      force.add(createVector(0.1, 0));
    }
    if (keyIsDown(UP_ARROW)) {
      force.add(createVector(0, -0.1));
    }
    if (keyIsDown(DOWN_ARROW)) {
      force.add(createVector(0, 0.1));
    }
    this.applyForce(force);

    // Aplicar arrastre según la sección
    if (this.position.y < height / 3) {
      // Vacío (sin fricción)
    } else if (this.position.y < 2 * height / 3) {
      // Aire (resistencia baja)
      this.applyDrag(0.05);
    } else {
      // Miel (resistencia alta)
      this.applyDrag(0.2);
    }
  }

  applyDrag(coefficient) {
    let speed = this.velocity.mag();
    let dragMagnitude = coefficient * speed * speed;
    let dragForce = this.velocity.copy();
    dragForce.mult(-1);
    dragForce.setMag(dragMagnitude);
    this.applyForce(dragForce);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);

    if (this.position.x > width) this.position.x = width;
    if (this.position.x < 0) this.position.x = 0;
    if (this.position.y > height) this.position.y = height;
    if (this.position.y < 0) this.position.y = 0;
  }

  display() {
    fill(127);
    ellipse(this.position.x, this.position.y, 40, 40);
  }
}

function drawSections() {
  noStroke();

  // Sección sin fricción (vacío)
  fill(255);
  rect(0, 0, width, height / 3);

  // Sección con viento (aire)
  fill(200);
  rect(0, height / 3, width, height / 3);
  drawParticles();

  // Sección con fluido (miel)
  fill(255, 204, 0);
  rect(0, 2 * height / 3, width, height / 3);
}

function drawParticles() {
  fill(150);
  for (let i = 0; i < 50; i++) {
    let x = random(width);
    let y = random(height / 3, 2 * height / 3);
    ellipse(x, y, 5, 5);
  }
}

function displayInstructions() {
  fill(0);
  textSize(16);
  textAlign(CENTER);
  text('Usa las flechas para mover el objeto. Experimenta con las distintas secciones.', width / 2, height - 20);
}

```

[Link del Sketch](https://editor.p5js.org/MateoJimenezFamaArt/sketches/YGBWkJ8r3)


3 Fuerza Gravitacional


```js
let electrones = [];
let nucleo;
let G = 1; // Constante gravitacional
let font;

function preload() {
  font = loadFont('https://cdnjs.cloudflare.com/ajax/libs/topcoat/0.8.0/font/SourceCodePro-Light.otf'); // Cargar una fuente
}

function setup() {
  createCanvas(800, 600, WEBGL);
  textFont(font); // Establecer la fuente cargada
  nucleo = new Nucleo();
  for (let i = 0; i < 10; i++) { // Agregamos más electrones
    electrones.push(new Electron());
  }
}

function draw() {
  background(30);
  orbitControl(); // Control de cámara
  nucleo.rotateNucleus(); // Rotar el núcleo
  nucleo.display();
  for (let electron of electrones) {
    electron.attracted(nucleo); // Aplicar la fuerza gravitacional
    electron.update();
    electron.display();
  }
  displayInstructions();
}

function keyPressed() {
  if (keyCode === UP_ARROW) {
    G += 0.1; // Incrementar la gravedad
  } else if (keyCode === DOWN_ARROW) {
    G = max(0, G - 0.1); // Disminuir la gravedad, pero no menos de 0
  }
}

class Nucleo {
  constructor() {
    this.position = createVector(0, 0, 0);
    this.mass = 20; // Masa del núcleo
    this.angle = 0; // Ángulo inicial para rotación
  }

  rotateNucleus() {
    this.angle += 0.01; // Velocidad de rotación
    rotateY(this.angle); // Rotar en el eje Y
    rotateX(this.angle / 2); // Rotar en el eje X para más variación
  }

  display() {
    push();
    fill(255, 0, 0);
    noStroke();
    sphere(50); // Esfera del núcleo
    pop();
  }
}

class Electron {
  constructor() {
    this.position = p5.Vector.random3D().mult(200); // Posición aleatoria alrededor del núcleo
    this.velocity = createVector(0, 0, 0);
    this.acceleration = createVector(0, 0, 0);
    this.mass = 1;
  }

  applyForce(force) {
    let f = force.copy();
    f.div(this.mass);
    this.acceleration.add(f);
  }

  attracted(nucleo) {
    let force = p5.Vector.sub(nucleo.position, this.position); // Vector desde el electrón al núcleo
    let distanceSq = constrain(force.magSq(), 25, 500); // Evitar que se acerque demasiado
    let strength = (G * this.mass * nucleo.mass) / distanceSq;
    force.setMag(strength);
    this.applyForce(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  display() {
    push();
    translate(this.position.x, this.position.y, this.position.z);
    fill(0, 0, 255);
    noStroke();
    sphere(10); // Esfera para representar el electrón
    pop();
  }
}

function displayInstructions() {
  push();
  translate(-width / 2 + 20, -height / 2 + 20);
  fill(255);
  textSize(16);
  text('Usa las flechas arriba y abajo para modificar la gravedad (G): ' + G.toFixed(2), 10, 30);
  pop();
}
```

[Link del Sketch](https://editor.p5js.org/MateoJimenezFamaArt/sketches/IooZ6Ub99)
