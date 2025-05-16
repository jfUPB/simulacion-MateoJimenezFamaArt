## Link del sketch

Haz click aca [>.<](https://editor.p5js.org/MateoJimenezFamaArt/sketches/CZ1K5tNp9)

## Codigo de simulacion


```js
let angle = 0;
let angleVelocity = 0.2;
let amplitude = 100;

function setup() {
  createCanvas(640, 240);
  stroke(0);
  strokeWeight(2);
  fill(127, 127);
}

function draw() {
  background(255); // Limpiar la pantalla en cada frame
  
  // Reiniciar el ángulo para mantener la onda en movimiento
  let angleOffset = angle; 
  
  for (let x = 0; x <= width; x += 24) {
    // 1) Calcular la posición y de acuerdo a la amplitud y el seno del ángulo
    let y = amplitude * sin(angleOffset);
    
    // 2) Dibujar un círculo en la posición (x, y)
    circle(x, y + height / 2, 48);
    
    // 3) Incrementar el ángulo para que la onda continúe
    angleOffset += angleVelocity;
  }
  
  // Incrementar el ángulo general para crear la animación de movimiento
  angle += 0.05;
}

```

## Screeshot
![image](https://github.com/user-attachments/assets/f7aa9078-4dbf-444e-8997-b1a6800d94b1)
