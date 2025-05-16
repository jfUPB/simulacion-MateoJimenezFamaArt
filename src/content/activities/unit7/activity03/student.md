## Diseno

Palabra : Volleyball

La palabra deberia tener cada letra representada por un cuerpo de Matter.js

Idealmente la palabra comienza estatica, luego la O se cae y rebota un par de veces como si fuera un balon, luego suena un silbato y la O sale disparada como si fuera un servicio y golpea a las demas letras hacia todos lados.

Para el mundo en Matter.js todo deberia estar bajo un world donde la gravedad es real pero no les afecta si no hasta que despues de que la O colisiona con las letras 

El usuario debera hacer click para iniciar el rebote de la O

## Code

```js
// Requiere importar Matter.js manualmente en el editor de p5.js

// Módulos de Matter.js
let Engine = Matter.Engine,
    World = Matter.World,
    Bodies = Matter.Bodies,
    Body = Matter.Body;

let engine;
let world;
let ground;

let fallingO;
let isODropped = false;

function setup() {
  createCanvas(800, 400);
  
  // Crear motor de física
  engine = Engine.create();
  world = engine.world;
  Engine.run(engine);

  // Crear el suelo
  ground = Bodies.rectangle(width / 2, height - 10, width, 20, {
    isStatic: true,
    label: "ground"
  });
  World.add(world, ground);

  textFont('monospace');
  textSize(64);
  textAlign(CENTER, CENTER);
}

function draw() {
  background(240);
  
  // Mostrar texto con la letra 'O' reemplazada por un círculo físico
  let word = "volleyball";
  let oIndex = word.indexOf("o");
  
  let spacing = 50;
  let startX = width / 2 - spacing * (word.length / 2);

  for (let i = 0; i < word.length; i++) {
    let x = startX + i * spacing;
    let y = height / 3;

    if (i === oIndex && isODropped && fallingO) {
      // Mostrar la "O" como un círculo que cae
      let pos = fallingO.position;
      fill(0);
      ellipse(pos.x, pos.y, 48, 48);

      // Opcional: dibujar la letra "O" sobre el círculo
      fill(255);
      text('O', pos.x, pos.y + 5);
    } else {
      // Dibujar letras normales
      fill(0);
      text(word[i].toUpperCase(), x, y);
    }
  }

  // Dibujar el suelo
  noStroke();
  fill(150);
  rectMode(CENTER);
  rect(ground.position.x, ground.position.y, width, 20);
}

function mousePressed() {
  if (!isODropped) {
    // Crear la letra "O" como un círculo físico
    let x = width / 2 - 50 * 4 + 1 * 50; // Posición X del carácter 'O' (2da letra)
    let y = height / 3;
    fallingO = Bodies.circle(x, y, 24, {
      restitution: 0.6,
      friction: 0.1,
      label: "O"
    });
    World.add(world, fallingO);
    isODropped = true;
  }
}

```

