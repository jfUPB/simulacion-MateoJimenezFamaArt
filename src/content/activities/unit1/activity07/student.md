# Explicacion ruido perlin vs random numbers

La mejor forma de describir al ruido perlin es el caos controlado, en una generacion aleatorea de numeros el ruido perlin aproxima ciertos valores para que los numeros tengan una relacion entre si y se vena mas organicos. Por contra parte el valor random asigna numeros y genera muchos picos erraticos mientras que el ruido perlin no.
De las mejores maneras para explicar esto es como si el ruido perlin fuese una melodia tocada en un piano, las notas que anteceden y proceden a las siguientes notas tienen una relacion asi parezca aleatorio, mientras que el random funciona como un niño pequeño tocando piano por primera vez, oprime teclas al azar sin relacionar ninguna en lo absoluto

# Como lo use para generar variaciones

En mi ejemplo tome una de las proposisiones en la documentacion de p5.js con el fin de utilizar el ruido perlin para hacer una especie de mar calmado. La forma de uso fue la siguiente:
Luego de crear un canvas de color gris, utilizamos un metodo for que paso por paso va pintando el canvas por completo hasta llegar al width de este mismo. Luego definimos valores para escalar nuestro ruido en funcion del canvas (para que sea escalable). Luego utilizamos la funcion del ruido perlin con el fin de generar un valor para la Y que se esta dibujando de la linea y poder alterarla con ruido
Ya finalmente dibujamos la linea utilizando los valores de x y para la y empleamos nuestra y calculada con ruido perlin.

# Codigo

``` js
function setup() {
  createCanvas(600,600);

  describe('A calm sea drawn in gray against a black sky.');
}

function draw() {
  background(200);

  // Set the noise level and scale.
  let noiseLevel = 500;
  let noiseScale = 0.002;

  // Iterate from left to right
  for (let x = 0; x < width; x += 0.1) {
    // Scale the input coordinates.
    let nx = noiseScale * x;
    let nt = noiseScale * frameCount;

    // Compute the noise value.
    let y = noiseLevel * noise(nx, nt);

    // Draw the line.
    line(x, 0, x, y);
  }
}
```

# Visualizacion

![image](https://github.com/user-attachments/assets/6cbe4a9a-b373-487c-9496-a99b08c31d25)

