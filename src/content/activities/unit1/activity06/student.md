# En que caso seria interesante usarlo?

El vuelo de levy puede ser interesante para usarse a la hora de programar la IA de un enemigo basada en que ejecute ciertas acciones en una probabilidad. Por ejemplo si yo quiero hacer que un enemigo se mueva de manera randomizada en un area. Yo puedo implementarle saltos de Levy para que pueda recorrer el terreno de manera un poco mas eficientemente y aun mejor podria usar los saltos de levy para que si se detecta un jugdaor se aumenten las probabilidades de que el enemigo recorra esa area.

# Codigo de la simulacion

``` js
class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    let step = 5;
    let xstep = acceptreject() * step;
    if (random([false, true])) {
      xstep *= -1;
    }
    let ystep = acceptreject() * step;
    if (random([false, true])) {
      ystep *= -1;
    }
    this.x += xstep;
    this.y += ystep;
  }
}

function acceptreject() {
  // We do this “forever” until we find a qualifying random value.
  while (true) {
    // Pick a random value.
    let r1 = random(1);
    // Assign a probability.
    let probability = r1 * r1;
    // Pick a second random value.
    let r2 = random(1);

    //{!3} Does it qualify?  If so, we’re done!
    if (r2 < probability) {
      return r1;
    }
  }
}

let walker; // Explicitly declare walker

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

```

# Captura de la simulacion

![image](https://github.com/user-attachments/assets/72806a54-7307-43be-8c49-ea1480553abc)
