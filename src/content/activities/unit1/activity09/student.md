# Code

``` js
class Walker {
  constructor() {
    this.x = 1;
    this.y = height / 2;
    this.choiceValue = 0;
    this.xAddition = 1;
  }

  show() {
    stroke('red');
    point(this.x, this.y);
  }

  step() {
    let choice = floor(randomGaussian(this.choiceValue));
    if (choice === 0) {
      this.x += this.xAddition;
    }
    if (choice === 1) {
      this.y--;
      if (this.y <= 0) {
        print("Choice Value is " + this.choiceValue);
        this.y = height / 2;
        this.choiceValue = 2;
        print("Choice now Value is " + this.choiceValue);
      }
    }
    if (choice === 2) {
      this.y++;
      if (this.y >= height) {
        print("The value of Y became more than Max");
        this.y = height / 2;
        this.choiceValue = 0;
      }
    }
  }
}

let walker;

function setup() {
  createCanvas(600, 100);
  walker = new Walker();
  background(255);
}

function draw() {
  
   // Ruido Perlin Para el Terreno
  let noiseLevel = 100;
  let noiseScale = 0.02;

  let x = frameCount;
  let nx = noiseScale * x;

  let y = noiseLevel * noise(nx);

  stroke(0)
  line(x, 0, x, y);
  
  walker.step();
  walker.show();
}

function keyPressed() {
  if (keyCode === UP_ARROW) {
    walker.choiceValue = 1; // Moves upward more often
  } else if (keyCode === DOWN_ARROW) {
    walker.choiceValue = 2; // Moves downward more often
  } else if (keyCode === LEFT_ARROW) {
    walker.xAddition = -1; // Moves left
  } else if (keyCode === RIGHT_ARROW) {
    walker.xAddition = 5; // Moves right faster
  }
}

```

# Imagen 

![image](https://github.com/user-attachments/assets/f8cb92c5-760d-40a9-bdc8-04d71830e1b8)

# Cambios

El diseno y lo que termine logrando me parece llego a un nivel satisfactorio de complecion.
