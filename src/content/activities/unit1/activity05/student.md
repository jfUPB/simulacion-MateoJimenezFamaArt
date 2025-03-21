# Codigo del ejemplo

```js
class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
    this.tipX = this.x + 50; // Use this.tipX
    this.tipY = this.y + 50; // Use this.tipY
  }
  
  show() {
    stroke(0);
    triangle(this.x - 50, this.y, this.x + 50, this.y, this.tipX, this.tipY); // Use this.tipX and this.tipY
  }
  
  step() {
    // Random choice determines the step
    let choice = floor(randomGaussian(random(7)));
    if (choice === 0) { // Diag Derecha Abajo
      this.tipX++;
      this.tipY++;
    } else if (choice === 1) { // Diag Izquierda Arriba
      this.tipX--;
      this.tipY--;
    } else if (choice === 2) { // Diag Izquierda Abajo
      this.tipY++;
      this.tipX--;
    } else if (choice === 3) { // Diago Derecha Arriba
      this.tipY--;
      this.tipX++;
    } else if (choice === 4) { // Derecha
      this.tipX++;
    } else if (choice === 5) { // Abajo
      this.tipY++;
    } else if (choice === 6) { // Izquierda
      this.tipX--;
    } else if (choice === 7) { // Arriba
      this.tipY--;
      choice = 0;
    }
  }
}

let walker; // Explicitly declare walker

function setup() {
  createCanvas(400, 400); // Ensure canvas is created first
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

```

# Captura de pantalla

![Description] (../../../../assets/CapturaActividad5.jpg)


# Explicacion

La distribucion normal entra en esta visualizacion por que lo que estamos haciendo es fusionar una distribucion gaussiana y una random con el fin de randomizar la media de lo que nos queremos dirigir. Este algortimo tiene dentro de sus posibilidades el terminar pintando una especie de circulo en la pantalla si se le deja suficiente tiempo

![image](https://github.com/user-attachments/assets/6a372f56-28e6-4a3a-98ed-75c89bfe6ced)
