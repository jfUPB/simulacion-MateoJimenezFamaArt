## Concepto de desarrollo

La idea es hacer un programa en el cual se pueda jugar pong de manera interactiva pero esta la pelota se movera en una onda seno cada vez que un jugador le pegue a la bola.

## Avances de codigo

```js
let ball;
let paddleLeft, paddleRight;
let isSineWave = false;  // Variable para saber si la pelota está en onda

function setup() {
  createCanvas(800, 400);

  // Pelota (movediza)
  ball = new Ball(width / 2, height / 2, 15);

  // Paletas (controles de jugador)
  paddleLeft = new Paddle(20, height / 2, 10, 100);
  paddleRight = new Paddle(width - 30, height / 2, 10, 100);
}

function draw() {
  background(255);

  // Actualizar las posiciones
  ball.update();
  paddleLeft.update();
  paddleRight.update();

  // Mostrar los elementos
  ball.show();
  paddleLeft.show();
  paddleRight.show();

  // Control de paletas (movimiento hacia arriba y abajo)
  if (keyIsDown(87)) {  // Tecla W
    paddleLeft.move(-5);
  }
  if (keyIsDown(83)) {  // Tecla S
    paddleLeft.move(5);
  }
  if (keyIsDown(UP_ARROW)) {
    paddleRight.move(-5);
  }
  if (keyIsDown(DOWN_ARROW)) {
    paddleRight.move(5);
  }
}

// Clase para la pelota
class Ball {
  constructor(x, y, r) {
    this.pos = createVector(x, y);
    this.r = r;
    this.velocity = createVector(2, 0);  // Velocidad inicial
    this.acceleration = createVector(0, 0);
    this.time = 0;  // Para controlar el tiempo de la onda
  }

  update() {
    if (isSineWave) {
      // Generar movimiento en onda de seno si es necesario
      this.acceleration = 0.1 * sin(this.time); // Onda senoidal en el movimiento
      this.time += 0.1; // Aumentar el tiempo para que la onda avance
      print(this.acceleration);
    } else {
      // Movimiento normal (sin onda)
      this.pos.add(this.velocity);  // Actualizar la posición según la velocidad
      this.velocity.add(this.acceleration);  // Actualizar la velocidad según la aceleración
      this.acceleration.mult(0);  // Resetear la aceleración

      // Colisión con los bordes (pantalla)
      if (this.pos.y - this.r < 0 || this.pos.y + this.r > height) {
        this.velocity.y *= -1;  // Rebote vertical
      }
    }

    // Colisión con las paletas
    if (this.pos.x - this.r < paddleLeft.x + paddleLeft.width && 
        this.pos.y > paddleLeft.y && 
        this.pos.y < paddleLeft.y + paddleLeft.height) {
      this.velocity.x *= -1;  // Rebote horizontal
      this.pos.x = paddleLeft.x + paddleLeft.width + this.r;
      isSineWave = true; // Activar el modo onda cuando golpea la paleta izquierda
    }

    if (this.pos.x + this.r > paddleRight.x && 
        this.pos.y > paddleRight.y && 
        this.pos.y < paddleRight.y + paddleRight.height) {
      this.velocity.x *= -1;  // Rebote horizontal
      this.pos.x = paddleRight.x - this.r;
      isSineWave = true; // Activar el modo onda cuando golpea la paleta derecha
    }
  }

  show() {
    fill(127);
    noStroke();
    ellipse(this.pos.x, this.pos.y, this.r * 2);
  }
}

// Clase para las paletas
class Paddle {
  constructor(x, y, w, h) {
    this.x = x;
    this.y = y;
    this.width = w;
    this.height = h;
  }

  update() {
    // Restringir la paleta a que no se salga de la pantalla
    this.y = constrain(this.y, 0, height - this.height);
  }

  move(amount) {
    this.y += amount;  // Mover la paleta
  }

  show() {
    fill(0);
    noStroke();
    rect(this.x, this.y, this.width, this.height);
  }
}

```
### Issues
Actualmente la pelota choca con la paleta pero se detiene puesto que su aceleracion no esta siendo correctamente procesada

## Caputra del codigo
![image](https://github.com/user-attachments/assets/532433ab-dfe4-441e-b14d-03cf17c81390)


## Codigo Final

```js
let ball;
let paddleLeft, paddleRight;
let isSineWave = false;  // Variable para saber si la pelota está en onda
let leftScore = 0;  // Puntuación del jugador izquierdo
let rightScore = 0;  // Puntuación del jugador derecho

function setup() {
  createCanvas(800, 400);

  // Pelota (movediza)
  ball = new Ball(width / 2, height / 2, 15);

  // Paletas (controles de jugador)
  paddleLeft = new Paddle(20, height / 2, 10, 100);
  paddleRight = new Paddle(width - 30, height / 2, 10, 100);
}

function draw() {
  background(255);

  // Mostrar puntuaciones
  textSize(32);
  textAlign(CENTER, CENTER);
  fill(0);
  text(leftScore, width / 4, 50);
  text(rightScore, 3 * width / 4, 50);

  // Actualizar las posiciones
  ball.update();
  paddleLeft.update();
  paddleRight.update();

  // Mostrar los elementos
  ball.show();
  paddleLeft.show();
  paddleRight.show();

  // Control de paletas (movimiento hacia arriba y abajo)
  if (keyIsDown(87)) {  // Tecla W
    paddleLeft.move(-5);
  }
  if (keyIsDown(83)) {  // Tecla S
    paddleLeft.move(5);
  }
  if (keyIsDown(UP_ARROW)) {
    paddleRight.move(-5);
  }
  if (keyIsDown(DOWN_ARROW)) {
    paddleRight.move(5);
  }
}

// Clase para la pelota
class Ball {
  constructor(x, y, r) {
    this.pos = createVector(x, y);
    this.r = r;
    this.velocity = createVector(2, 2);  // Velocidad inicial
    this.time = 0;  // Para controlar el tiempo de la onda
  }

  update() {
    if (isSineWave) {
      // Generar movimiento en onda de seno si es necesario
      this.pos.y += 5 * sin(this.time); // Onda senoidal en el movimiento vertical
      this.time += 0.1; // Aumentar el tiempo para que la onda avance
    }

    // Movimiento normal (sin onda para el eje x)
    this.pos.add(this.velocity);  // Actualizar la posición según la velocidad

    // Colisión con los bordes (pantalla superior e inferior)
    if (this.pos.y - this.r < 0 || this.pos.y + this.r > height) {
      this.velocity.y *= -1;  // Rebote vertical
    }

    // Golpea los extremos izquierdo o derecho (puntos)
    if (this.pos.x - this.r < 0) {
      rightScore++;  // El jugador derecho anota
      this.reset();  // Reiniciar la pelota
    } else if (this.pos.x + this.r > width) {
      leftScore++;  // El jugador izquierdo anota
      this.reset();  // Reiniciar la pelota
    }

    // Colisión con las paletas
    if (this.pos.x - this.r < paddleLeft.x + paddleLeft.width && 
        this.pos.y > paddleLeft.y && 
        this.pos.y < paddleLeft.y + paddleLeft.height) {
      this.velocity.x *= -1;  // Rebote horizontal
      this.pos.x = paddleLeft.x + paddleLeft.width + this.r;
      isSineWave = true; // Activar el modo onda cuando golpea la paleta izquierda
    }

    if (this.pos.x + this.r > paddleRight.x && 
        this.pos.y > paddleRight.y && 
        this.pos.y < paddleRight.y + paddleRight.height) {
      this.velocity.x *= -1;  // Rebote horizontal
      this.pos.x = paddleRight.x - this.r;
      isSineWave = true; // Activar el modo onda cuando golpea la paleta derecha
    }
  }

  // Función para reiniciar la pelota al centro de la pantalla
  reset() {
    this.pos = createVector(width / 2, height / 2);  // Colocar la pelota en el centro
    this.velocity = createVector(random([-2, 2]), random([-2, 2]));  // Velocidad aleatoria en cualquier dirección
    isSineWave = false;  // Desactivar el modo onda al reiniciar
    this.time = 0;  // Reiniciar el tiempo de la onda
  }

  show() {
    fill(127);
    noStroke();
    ellipse(this.pos.x, this.pos.y, this.r * 2);
  }
}

// Clase para las paletas
class Paddle {
  constructor(x, y, w, h) {
    this.x = x;
    this.y = y;
    this.width = w;
    this.height = h;
  }

  update() {
    // Restringir la paleta a que no se salga de la pantalla
    this.y = constrain(this.y, 0, height - this.height);
  }

  move(amount) {
    this.y += amount;  // Mover la paleta
  }

  show() {
    fill(0);
    noStroke();
    rect(this.x, this.y, this.width, this.height);
  }
}

```

## Link del Sketch
Haz click aca [>.<](https://editor.p5js.org/MateoJimenezFamaArt/sketches/xiPr4fOvz)
