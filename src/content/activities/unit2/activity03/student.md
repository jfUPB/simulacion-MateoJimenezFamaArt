# Preguntas a responder

CODIGO

```
let position;

function setup() {
    createCanvas(400, 400);
    posicion = createVector(6,9);
    playingVector(posicion);
    noLoop();
}

function playingVector(v){
    v.x = 20;
    v.y = 30;
}

function draw() {
    background(220);
    console.log("Only once");
}
```

## ¿Qué resultado esperas obtener?

Esperaria que se forme una linea entre el punto (6,9) y el punto (20,30). Esto por que estamos definiendo un vector en el setup y lo estamos modificando en el metodo pasandole el vector creado. Sin embargo en ningun momento se esta creando una figura que permita visualizar el comportamiento del vector por ende solo se veria un fondo gris.


## ¿Qué resultado obtuviste?

Un fondo gris

## Recuerda los conceptos de paso por valor y paso por referencia en programación. Muestra ejemplos de este concepto en javascript.

PREGUNTAR AL PROFE ***

## ¿Qué tipo de paso se está realizando en el código?

PREGUNTAR AL PROFE ***

## ¿Qué aprendiste?

RESPONDER DESPUES DE HABLAR CON PROFE ***
