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


# Final

``` js
let t = 0;  // Interpolation factor
let direction = 1; // Controls direction of interpolation

function setup() {
    createCanvas(200, 200);
}

function draw() {
    background(200);

    let v0 = createVector(50, 50);
    let v1 = createVector(100, 0);   // Red arrow
    let v2 = createVector(0, 100);   // Blue arrow
    let v3 = p5.Vector.lerp(v1, v2, t); // Interpolated vector
    let v4 = p5.Vector.sub(v2,v1); //Green Arrow 1
    let v5 = createVector(150, 50); // Green Arrow 2

    // Interpolated color
    let c1 = color(255, 0, 0); // Red
    let c2 = color(0, 0, 255); // Blue
    let c3 = lerpColor(c1, c2, t); // Interpolated color

    drawArrow(v0, v1, 'red');  // Red Arrow
    drawArrow(v0, v2, 'blue'); // Blue Arrow
    drawArrow(v0, v3, c3);     // Interpolating Arrow
    drawArrow(v5, v4, 'green'); //Green Arrow
    
  
    // animation interpolation
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

## Imagen

![image](https://github.com/user-attachments/assets/945f109a-3b07-4232-871e-5121b1d31764)

## Preguntas


Lerp funciona interpolando de manera lineal (conectando de manera suave dos puntos) entre un vector y otro al igual que dandole un parametro de que tantos pasos puede tomarse esa interpolacion suave.
LerpColor hace lo mismo ya que cambia el valor de un elemento de manera "suave" entre dos elementos, como para hacer una gradiente. esto lo logra tomando el componente RGB de un elemento y el RGB de otro elemento y calculando los numeros que hay entre ellos y luego ir pasando entre ellos de manera parametrizada por nosotros, puede ir dando pasos de 5 en 5 como pueden ser pasos de 0.3 en 0.3.

Para dibujar una flecha usando el draw arrow propuesto definimos una base que muestra desde donde se dibujara nuestra flecha, luego le damos un parametro para ver en donde nos gustaria que nuestra flecha terminara y al final le asignamos un color con el cual poder identificarla mas facilmente.



