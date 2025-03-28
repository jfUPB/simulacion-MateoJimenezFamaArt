# Ejecisico 1.1 Codigo

```
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  position = createVector(100,100);
  velocity = createVector(2.5,2);
  
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();

}

class Walker {
  constructor() {
    position.x = width / 2;
    position.y = height / 2;
  }

  show() {
    stroke(0);
    point(position.x, position.y);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      velocity.x = velocity.x * 1;
    } else if (choice == 1) {
      velocity.x = velocity.x * -1;
    } else if (choice == 2) {
      velocity.y = velocity.y * 1;
    } else {
      velocity.y = velocity.y * -1;
    }
    position.add(velocity);
  }
}

```

Para realizar la conversion tuve que:
1. Crear vector posicion y vector velocidad en el setup
2. Hacer que ahora el point se dibuje en position.x y position.y
3. Para el movimiento aleatoreo debia tomar el vector velocidad y multiplicarlo por -1 en sus ejes con el fin de cambiar la direccion que este tomaria
4. Finalmente luego de que se hace la distribucion para saber que componente velocidad se altera hacemos una suma vectorial entre la posicion y la velocidad de nuestra figura

En esencia para usar vectores debemos:
1. Definirlo en setup (como posision y velocidad siempre)
2. Hacer que el draw de nuestra figura dependa de los contenidos en sus componentes vectoriales
3. Modificar nuestros componentes de position mediante el add(velocity) {Ya si se necesita cambiar la forma en que este se mueve se altera el vector velocidad}

   En resumen el posicion es donde estoy y el velocidad es a donde me quieren mover.
