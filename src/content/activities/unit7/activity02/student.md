## Experimentos basicos

![image](https://github.com/user-attachments/assets/0e7287ff-06dc-4d5e-95cc-33eefcab183d)

Objetos basicos uno sobre el otro
```js
const {Engine, Body, Bodies, Composite, Render, Runner} = Matter;

let engine;
let render;
let box;
let gorund;
let runner;

function setup() {
  noCanvas();
  engine = Engine.create();
  render = Render.create({
    element: document.body,
    engine: engine,
    options :  {
      width : 400,
      height : 400
    }
  });
  
  
  box = Bodies.rectangle(100,100,50,50);
  Body.setAngularVelocity(box,0.2);
  
  circle = Bodies.circle(120,0,20);
  Body.setAngularVelocity(circle,0.8);
  
  polygon = Bodies.polygon(250,30,6,30);
  Body.setAngularVelocity(polygon,-0.5);
  
  ground = Bodies.rectangle(200, 300, 400, 10, {isStatic: true});
  
  Composite.add(engine.world, [box,circle,polygon,ground]);
  
  Render.run(render);
  
  runner = Runner.create();
  Runner.run(runner,engine);
}

function draw()
{
  background(220);
  
  print(box.position);
}


```

![image](https://github.com/user-attachments/assets/8533971a-3c83-4c17-b112-6ae22bad3742)

Suelo estatico
```js
const {Engine, Body, Bodies, Composite, Render, Runner} = Matter;

let engine;
let render;
let box;
let gorund;
let runner;

function setup() {
  noCanvas();
  engine = Engine.create();
  render = Render.create({
    element: document.body,
    engine: engine,
    options :  {
      width : 400,
      height : 400
    }
  });
  
  
 
  ground = Bodies.rectangle(200, 300, 400, 10, {isStatic: true});
  
  Composite.add(engine.world, [ground]);
  
  Render.run(render);
  
  runner = Runner.create();
  Runner.run(runner,engine);
}

function draw()
{
  background(220);
  
  print(box.position);
}

```

## Dificultades de matter

Me costo importarlo en el html por que lo escribi mal pero luego lo corregi

## Conceptos

Engine ->  Powers the physiscs simulation
World ->  Enviroment containing all elements including bodies, constraints and physics
Bodies ->  Diferent shapes with presets
Constraint ->  The boundaries where those objects interact
MouseConstraint -> The rule imposed to use as a spawner for more bodies
