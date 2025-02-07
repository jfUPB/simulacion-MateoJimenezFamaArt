# Respuesta

Codigo original 

``` js
function setup() {
    createCanvas(100, 100);
}

function draw() {
    background(200);

    let v0 = createVector(50, 50);
    let v1 = createVector(30, 0);
    let v2 = createVector(0, 30);
    let v3 = p5.Vector.lerp(v1, v2, 0.5);
    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple');
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

# Progreso

``` js
function setup() {
    createCanvas(200, 200);
}

function draw() {
    background(200);
  
    let v0 = createVector(50, 50);
    let v1 = createVector(100, 0);
    let v2 = createVector(0, 100);
    let v3 = p5.Vector.lerp(v1, v2, 0.5);
    let v4 = p5.Vector.sub(v2,v1);
    let v5 = createVector(150, 50);
    
    
    drawArrow(v0, v1, 'red'); 
    drawArrow(v0, v2, 'blue'); 
    drawArrow(v0, v3, 'purple');
    drawArrow(v5, v4, 'green');
    
    
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
