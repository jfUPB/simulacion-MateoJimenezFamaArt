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

- Paso por valor hace referente a pasar directamente el valor de una varibale a una funcion para ser ejecutada
- Paso por referencia hace referente a pasar la direccion de la variable para una funcion con el fin de ser ejecutada

  Si bien el resultado sera el mismo el proceso durante no lo sera. En un ejemplo si tenemos una variable a = 1 y un variable b = 2. Si llamamos una funcion que haga a++; y luego haga a+b; vamos a obtener que en ambas rutas entra 1 y un 2 se le sumara 1 al 1 y quedara 2+2 = 4. En donde radica la diferencia?

  Si pasamos por valor entonces solo entra el 1 y el 2, al 1 se le suma otro 1 y nos da de resultado 4, pero el valor de las variables a y b sigue siendo 1 y 2 respectivamente.
  Si pasamos por referencia entronces entran el valor en a y en b (o sea 1 y 2), se realiza la operacion y nos da de resultado 4. Pero como le pasamos el valor de direccion en vez del valor como tal entonces el operador de a++ va a hacer que ahora el valor de a sea 2, asi que haciendolo otra vez tendriamos que el   valor seria 5 y seguiria creciendo.

  Ejemplo en JS

 ``` js
function modifyPrimitive(x) {
    x = 10; // This change won't affect the original value
    console.log("Inside function (primitive):", x);
}

let num = 5;
console.log("Before function call (primitive):", num);
modifyPrimitive(num);
console.log("After function call (primitive):", num);

// Passing by Reference (Objects)
function modifyObject(obj) {
    obj.name = "Changed"; // This change will reflect outside
    console.log("Inside function (object):", obj);
}

let myObj = { name: "Original" };
console.log("Before function call (object):", myObj);
modifyObject(myObj);
console.log("After function call (object):", myObj);
```

En una explicacion breve aca se hace por paso de valor puesto que enviamos valores primitivos y js hace una copia la modifica y opera. Por lo contrario al hacer paso por referencia js lo que hace es si recibe un array o un objeto hace una referencia directa a este, esto hace que si modificamos algun valor de este en la funcion tambien se vera modificado la version por afuera de la funcion.

## ¿Qué tipo de paso se está realizando en el código?

En el codigo se hace paso por referencia ya que la funcion recibe un vector (un tipo de array) y modifica sus valores, esto hace que los valroes del vector que se estan modificando permanezcan modificados inclusive afuera de la funcion.

## ¿Qué aprendiste?

Aprendi a repasar el concepto de paso por valor y por referencia al igual que sus diferencias y como usarlas, finalmente tambien aprendi de este codigo que no se debe hacer calculos y luego esperar verlos si no tienes ningun tipo de objeto dibujado que se modifique segun los calculos que estas realizando
