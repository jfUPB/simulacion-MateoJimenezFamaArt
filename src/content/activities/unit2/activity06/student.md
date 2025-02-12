# Codigo

``` js
let t = 0;  // Interpolation factor
let direction = 1; // Controls direction of interpolation

function setup() {
    createCanvas(800, 800);
}

function draw() {
    background(200);

    let base = createVector(mouseX, mouseY); // Base moves with mouse
    let scaleFactor = map(mouseX, 0, width, 0.5, 2); // Scale factor based on mouse position

    let v1 = createVector(100, 0).mult(scaleFactor);   // Red arrow (scaled)
    let v2 = createVector(0, 100).mult(scaleFactor);   // Blue arrow (scaled)
    let v3 = p5.Vector.lerp(v1, v2, t); // Interpolated vector (scaled)
    let v4 = p5.Vector.sub(v2, v1); // Green Arrow 1 (scaled)
    let v5 = createVector(100, 0).mult(scaleFactor); // Green Arrow 2 (scaled)

    // Interpolated color
    let c1 = color(255, 0, 0); // Red
    let c2 = color(0, 0, 255); // Blue
    let c3 = lerpColor(c1, c2, t); // Interpolated color

    drawArrow(base, v1, 'red');  // Red Arrow
    drawArrow(base, v2, 'blue'); // Blue Arrow
    drawArrow(base, v3, c3);     // Interpolating Arrow
    drawArrow(base.copy().add(v5), v4, 'green'); // Green Arrow (adjusted base)

    // Animation interpolation
    t += 0.02 * direction;
    if (t >= 1 || t <= 0) {
        direction *= -1; // Reverse direction
    }
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```
# Como?

Logramos hacer esta version donde todo se logra mover al hacer que la base de donde se dibujan todos los vectores dependan de la posicion actual del raton, aplicamos lo mismo para la escala/
