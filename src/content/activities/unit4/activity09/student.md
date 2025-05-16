## Link del sketch

Haz click aca [>.<](https://editor.p5js.org/MateoJimenezFamaArt/sketches/cZEpBoVI3)

## Codigop

SKETCH.js
```js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

// Mover objects
let bob1, bob2;

// Spring objects
let spring1, spring2;

function setup() {
  createCanvas(640, 240);

  // Create first spring and bob
  spring1 = new Spring(width / 2, 10, 100);
  bob1 = new Bob(width / 2, 100);
  
  // Create second spring and bob (second spring connects bob1 and bob2)
  spring2 = new Spring(width / 2, 100, 100);
  bob2 = new Bob(width / 2, 200);
}

function draw() {
  background(255);

  // Apply gravity to both bobs
  let gravity = createVector(0, 2);
  bob1.applyForce(gravity);
  bob2.applyForce(gravity);

  // Update bobs
  bob1.update();
  bob2.update();

  bob1.handleDrag(mouseX, mouseY);
  bob2.handleDrag(mouseX, mouseY);

  // Connect the bobs to the springs
  spring1.connect(bob1);  // Connect first spring to bob1
  spring2.connect(bob2);  // Connect second spring to bob2

  // Apply a force between bob1 and bob2 with spring2
  spring2.connectBetween(bob1, bob2);

  // Constrain spring distances
  spring1.constrainLength(bob1, 30, 200);
  spring2.constrainLength(bob2, 30, 200);

  // Draw everything
  spring1.showLine(bob1);
  spring2.showLine(bob2);
  bob1.show();
  bob2.show();
  spring1.show();
  spring2.show();
}

function mousePressed() {
  bob1.handleClick(mouseX, mouseY);
  bob2.handleClick(mouseX, mouseY);
}

function mouseReleased() {
  bob1.stopDragging();
  bob2.stopDragging();
}

```

SPRING.js
```js
// Nature of Code
// Daniel Shiffman
// Chapter 3: Oscillation

class Spring {
  constructor(x, y, length) {
    this.anchor = createVector(x, y);
    this.restLength = length;
    this.k = 0.2;
  }

  // Calculate and apply spring force
  connect(bob) {
    let force = p5.Vector.sub(bob.position, this.anchor);
    let currentLength = force.mag();
    let stretch = currentLength - this.restLength;
    force.setMag(-1 * this.k * stretch);
    bob.applyForce(force);
  }

  // New method: Connects two bobs (for springs between them)
  connectBetween(bob1, bob2) {
    let force = p5.Vector.sub(bob1.position, bob2.position);
    let currentLength = force.mag();
    let stretch = currentLength - this.restLength;
    force.setMag(-1 * this.k * stretch);

    // Apply equal and opposite forces to each bob
    bob1.applyForce(force);
    force.mult(-1); // Opposite force
    bob2.applyForce(force);
  }

  constrainLength(bob, minlen, maxlen) {
    let direction = p5.Vector.sub(bob.position, this.anchor);
    let length = direction.mag();

    if (length < minlen) {
      direction.setMag(minlen);
      bob.position = p5.Vector.add(this.anchor, direction);
      bob.velocity.mult(0);
    } else if (length > maxlen) {
      direction.setMag(maxlen);
      bob.position = p5.Vector.add(this.anchor, direction);
      bob.velocity.mult(0);
    }
  }

  // Draw the anchor
  show() {
    fill(127);
    circle(this.anchor.x, this.anchor.y, 10);
  }

  // Draw the spring connection between Bob position and anchor
  showLine(bob) {
    stroke(0);
    line(bob.position.x, bob.position.y, this.anchor.x, this.anchor.y);
  }
}
```

## Screenshot

![image](https://github.com/user-attachments/assets/28392182-4311-497f-9469-298e5cb0a1d8)
