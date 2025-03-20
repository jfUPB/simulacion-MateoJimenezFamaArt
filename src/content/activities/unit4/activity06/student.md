## Link de P5.js

Click aca [>.<](https://editor.p5js.org/juanferfranco/sketches/fE5rCtDS1)

## Codigo


``` js
let amplitude = 100; // Amplitud inicial
let phase = 0;       // Fase inicial
let frequency = 0.05; // Frecuencia de la onda

function setup() {
  createCanvas(800, 400);
}

function draw() {
  background(255);
  stroke(0);
  noFill();
  
  let yOffset = height / 2; // Centro vertical de la onda
  
  beginShape();
  for (let x = 0; x < width; x++) {
    // Onda sinusoidal: y = A * sin(2πfx + θ)
    let y = amplitude * sin(frequency * (x + phase)) + yOffset;
    vertex(x, y);
  }
  endShape();

  // Mostrar la amplitud y la fase actual en la pantalla
  fill(0);
  noStroke();
  textSize(16);
  text(`Amplitud: ${amplitude}`, 10, 20);
  text(`Fase: ${phase}`, 10, 40);
}

// Control de teclas para ajustar la amplitud y la fase
function keyPressed() {
  if (keyCode === UP_ARROW) {
    amplitude += 10; // Incrementar amplitud
  } else if (keyCode === DOWN_ARROW) {
    amplitude -= 10; // Disminuir amplitud
  } else if (keyCode === RIGHT_ARROW) {
    phase += 10; // Desplazar fase hacia la derecha
  } else if (keyCode === LEFT_ARROW) {
    phase -= 10; // Desplazar fase hacia la izquierda
  }
}
```

## Screenshot

![image](https://github.com/user-attachments/assets/4d108a8f-53ca-4865-a9d7-908054659a00)
