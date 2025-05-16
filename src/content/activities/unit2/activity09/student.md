# Codigo

``` js
// Declare the Mover object.
let mover;

function setup() {
  createCanvas(640, 240);
  RandomValue = 0;
  // Create the Mover object.
  Bola1 = new Mover(50,height/4 , 0,0, 0.01, 0);
  Bola2 = new Mover(50,height / 4 + height/4, RandomValue,0);
  Bola3 = new Mover(50, height / 4 + height/4 + height/4 ,0,0);
}

function draw() {
  background(255);
  
  Bola1.update(false,false);
  Bola1.checkEdges();
  
  Bola2.update(true,false);
  Bola2.checkEdges();
  
  Bola3.update(false,true);
  Bola3.checkEdges();
  
  Bola1.show();
  Bola2.show();
  Bola3.show();
}

class Mover {
  constructor(positionX , positionY, velocityX , velocityY , accelX , accelY) {
    // The object has two vectors: position and velocity.
    this.position = createVector(positionX, positionY);
    this.velocity = createVector(velocityX,velocityY);
    this.acceleration = createVector(accelX, accelY);
    this.topSpeed = 10;
  }

  update(isRandomValue, isMouseFollower) {
    
    if(isRandomValue == true)
    {
      this.acceleration = p5.Vector.random2D();
    }
    
    if (isMouseFollower)
    {
      let mouse = createVector(mouseX, mouseY);
      let dir = p5.Vector.sub(mouse, this.position);
      dir.normalize();
      dir.mult(0.2);
      this.acceleration = dir;
    }
    
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topSpeed);
    this.position.add(this.velocity);
    
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 48);
  }

  checkEdges() {
    if (this.position.x >= width || this.position.x <= 0) {
      this.velocity.x *= -1; // Reverse X direction
    }

    if (this.position.y >= height || this.position.y <= 0) {
      this.velocity.y *= -1; // Reverse Y direction
    }
  }
}

```


# Reporte

Encontre que el de aceleracion constante es el mas sencillo ya que simplemente describe un cuerpo cuya acceleracion no cambia. Tambien encontre que el que se mueve en aceleracion random se ve interesante siempre y cuando sea en multiples ejes puesto que si hacemos que acelere de manera random en un solo eje se ve extraña la forma en la que se mueve por que se ve como pegado. Finalmente el de la aceleracion del mouse es el mas divertido por que se siente como en un mini videojuego. Finalmente encuentro el por que de cada cosa puesto que la aceleracion constante es sencilla de replicar, la random me parece caotica pero util y la parametrizada por el mouse es la mas interesante para usarse.
