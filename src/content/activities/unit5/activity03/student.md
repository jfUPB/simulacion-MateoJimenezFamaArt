# Planing

- The idea is to create an ineractive experience where there is a catapult that after a certain threshold of a microphone (or a key pressed). After the threshold happens a random object is tossed with varying properties (Each object should be a polimorfism of tossed object but with different characteristics like wieght and stuff). On top of this there is an ongoing particle effect system which dranw lines in the wind simulating the movement of this using a mix between perlin noise and sin waves in order to have a very organic and lively wind that is affected by the elements being tossed aka they will be repellant from the wind particles themselves. As for concepts we will use: 
1. Wind resistance
2. Motion 101
3. Orbital movement
4. Random Values

The way the sistem should handle the creation and destruction of particles is to have them spawn from one side and after they finish their journy trhough the canvas they should get eliminated from the list of particles to be generated and new ones should only be created when old ones are destroyed. 

## Coding

'''js
// Interactive Catapult with Wind Physics System - Complete
// Inspired by The Nature of Code by Daniel Shiffman

let particles = [];
let tossedObjects = [];
let catapult;
let windField;
let useKeyPress = true; // Use key press for launching objects

function setup() {
  createCanvas(windowWidth, windowHeight);
  
  // Initialize the catapult
  catapult = new Catapult(width * 0.2, height * 0.7);
  
  // Initialize the wind field
  windField = new WindField();
  
  background(25, 25, 35);
}

function draw() {
  background(25, 25, 35);
  
  // Update and display the wind field
  windField.update();
  windField.display();
  
  // Update and display the catapult
  catapult.update();
  catapult.display();
  
  // Update and display all tossed objects
  for (let i = tossedObjects.length - 1; i >= 0; i--) {
    let obj = tossedObjects[i];
    
    // Apply gravity
    obj.applyForce(createVector(0, obj.mass * 0.1));
    
    // Apply wind force from wind field
    let windForce = windField.getForceAt(obj.position.x, obj.position.y);
    obj.applyForce(windForce);
    
    // Update object physics
    obj.update();
    obj.display();
    
    // Remove if off screen
    if (obj.position.y > height + 100 || obj.position.x > width + 100) {
      tossedObjects.splice(i, 1);
    }
    
    // Object affects wind particles - repellant effect
    windField.applyRepeller(obj);
  }
  
  // Display object count
  fill(255);
  noStroke();
  textAlign(LEFT);
  text("Objects: " + tossedObjects.length, 20, 30);
  text("Press SPACE to launch", 20, 50);
}

function keyPressed() {
  if (key === ' ') {
    launchObject();
  }
}

function launchObject() {
  // Only launch if catapult is ready
  if (catapult.isReady()) {
    // Create a random tossed object
    let objectTypes = ["Rock", "Ball", "Box", "Star"];
    let type = random(objectTypes);
    let mass = random(0.5, 3);
    let launchForce = p5.Vector.fromAngle(-PI/3, random(10, 20));
    
    let newObject;
    switch(type) {
      case "Rock":
        newObject = new Rock(catapult.launchPosition.x, catapult.launchPosition.y, mass);
        break;
      case "Ball":
        newObject = new Ball(catapult.launchPosition.x, catapult.launchPosition.y, mass);
        break;
      case "Box":
        newObject = new Box(catapult.launchPosition.x, catapult.launchPosition.y, mass);
        break;
      case "Star":
        newObject = new Star(catapult.launchPosition.x, catapult.launchPosition.y, mass);
        break;
    }
    
    // Apply launch force
    newObject.applyForce(p5.Vector.mult(launchForce, newObject.mass));
    tossedObjects.push(newObject);
    
    // Reset catapult
    catapult.launch();
  }
}

// Wind Field class
class WindField {
  constructor() {
    this.particles = [];
    this.maxParticles = 50; // Reduced for better performance
    this.noiseScale = 0.01;
    this.noiseOffset = 0;
    this.timeOffset = 0;
  }
  
  update() {
    // Add new particles if needed
    while (this.particles.length < this.maxParticles) {
      this.particles.push(new WindParticle(0, random(height)));
    }
    
    // Update existing particles
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let particle = this.particles[i];
      
      // Calculate wind force using Perlin noise and sine wave
      let noiseVal = noise(
        particle.position.x * this.noiseScale, 
        particle.position.y * this.noiseScale, 
        this.noiseOffset
      );
      
      let sineVal = sin(particle.position.y * 0.01 + this.timeOffset) * 0.5;
      
      // Combine for organic effect
      let windAngle = map(noiseVal + sineVal, 0, 2, 0, TWO_PI);
      let windMagnitude = map(noiseVal, 0, 1, 2, 4);
      
      let windForce = p5.Vector.fromAngle(windAngle, windMagnitude);
      
      // Apply basic wind direction (left to right)
      windForce.add(createVector(1.5, 0));
      
      particle.applyForce(windForce);
      particle.update();
      
      // Remove particles that exit the screen
      if (particle.position.x > width) {
        this.particles.splice(i, 1);
      }
    }
    
    // Update noise and time offsets for animation
    this.noiseOffset += 0.003;
    this.timeOffset += 0.01;
  }
  
  display() {
    stroke(100, 150, 255, 100);
    strokeWeight(1);
    
    for (let particle of this.particles) {
      particle.display();
    }
  }
  
  // Calculate wind force at a specific position
  getForceAt(x, y) {
    let noiseVal = noise(x * this.noiseScale, y * this.noiseScale, this.noiseOffset);
    let sineVal = sin(y * 0.01 + this.timeOffset) * 0.5;
    
    let windAngle = map(noiseVal + sineVal, 0, 2, 0, TWO_PI);
    let windMagnitude = map(noiseVal, 0, 1, 0.05, 0.15);
    
    let windForce = p5.Vector.fromAngle(windAngle, windMagnitude);
    windForce.add(createVector(0.1, 0)); // Base rightward flow
    
    return windForce;
  }
  
  // Have objects repel wind particles
  applyRepeller(obj) {
    for (let particle of this.particles) {
      let force = p5.Vector.sub(particle.position, obj.position);
      let distance = force.mag();
      let repelRadius = obj.size * 2;
      
      if (distance < repelRadius) {
        let strength = map(distance, 0, repelRadius, 0.5, 0);
        force.normalize();
        force.mult(strength);
        particle.applyForce(force);
      }
    }
  }
}

// Wind Particle class
class WindParticle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(1, 3), 0);
    this.acceleration = createVector(0, 0);
    this.history = [];
    this.maxHistory = 10;
  }
  
  applyForce(force) {
    this.acceleration.add(force);
  }
  
  update() {
    // Update physics
    this.velocity.add(this.acceleration);
    this.velocity.limit(4);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    
    // Store position history for trail
    this.history.push(createVector(this.position.x, this.position.y));
    if (this.history.length > this.maxHistory) {
      this.history.shift();
    }
  }
  
  display() {
    // Draw trail
    noFill();
    beginShape();
    for (let i = 0; i < this.history.length; i++) {
      let alpha = map(i, 0, this.history.length, 50, 220);
      stroke(200, 220, 255, alpha);
      vertex(this.history[i].x, this.history[i].y);
    }
    endShape();
  }
}

// Catapult class
class Catapult {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.launchPosition = createVector(x + 60, y - 40);
    this.armAngle = -PI/6;
    this.targetAngle = -PI/6;
    this.loading = 0;
    this.readyToLaunch = true;
    this.lastLaunchTime = 0;
    this.cooldownTime = 1000; // 1 second cooldown
  }
  
  update() {
    // Handle the arm animation
    if (this.loading > 0) {
      this.armAngle = lerp(this.armAngle, PI/4, 0.1);
      this.loading -= 1;
      if (this.loading <= 0) {
        this.targetAngle = -PI/6;
        this.readyToLaunch = true;
      }
    } else {
      this.armAngle = lerp(this.armAngle, this.targetAngle, 0.1);
    }
    
    // Update launch position based on arm angle
    this.launchPosition.x = this.position.x + cos(this.armAngle) * 60;
    this.launchPosition.y = this.position.y + sin(this.armAngle) * 60;
  }
  
  display() {
    push();
    // Draw the base
    fill(120, 80, 40);
    rect(this.position.x - 30, this.position.y, 60, 30);
    
    // Draw the arm
    stroke(90, 60, 30);
    strokeWeight(10);
    line(this.position.x, this.position.y, 
         this.position.x + cos(this.armAngle) * 80, 
         this.position.y + sin(this.armAngle) * 80);
    strokeWeight(1);
    
    // Draw the launch cup
    fill(150, 100, 50);
    ellipse(this.launchPosition.x, this.launchPosition.y, 20, 20);
    pop();
  }
  
  launch() {
    if (this.readyToLaunch && millis() - this.lastLaunchTime > this.cooldownTime) {
      this.loading = 20; // Frames to load
      this.readyToLaunch = false;
      this.lastLaunchTime = millis();
    }
  }
  
  isReady() {
    return this.readyToLaunch && millis() - this.lastLaunchTime > this.cooldownTime;
  }
}

// Base TossedObject class (parent class for polymorphism)
class TossedObject {
  constructor(x, y, mass) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = mass;
    this.size = mass * 10;
    this.angularVelocity = random(-0.1, 0.1);
    this.angle = 0;
    this.airResistance = 0.01;
    this.color = color(200, 200, 200);
  }
  
  applyForce(force) {
    // Newton's second law: F = ma, so a = F/m
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }
  
  update() {
    // Apply air resistance
    let resistance = this.velocity.copy();
    resistance.normalize();
    resistance.mult(-1 * this.airResistance * this.velocity.magSq());
    this.applyForce(resistance);
    
    // Update physics
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    
    // Update angular position
    this.angle += this.angularVelocity;
  }
  
  display() {
    push();
    translate(this.position.x, this.position.y);
    rotate(this.angle);
    fill(this.color);
    ellipse(0, 0, this.size, this.size);
    pop();
  }
}

// Rock class (extends TossedObject)
class Rock extends TossedObject {
  constructor(x, y, mass) {
    super(x, y, mass);
    this.numVertices = floor(random(5, 8));
    this.vertices = [];
    this.airResistance = 0.008; // Less air resistance
    this.color = color(120, 120, 120);
    
    // Generate random vertices for the rock shape
    for (let i = 0; i < this.numVertices; i++) {
      let angle = map(i, 0, this.numVertices, 0, TWO_PI);
      let r = this.size/2 * random(0.7, 1.1);
      this.vertices.push({
        x: cos(angle) * r,
        y: sin(angle) * r
      });
    }
  }
  
  display() {
    push();
    translate(this.position.x, this.position.y);
    rotate(this.angle);
    fill(this.color);
    stroke(80);
    strokeWeight(1);
    
    beginShape();
    for (let v of this.vertices) {
      vertex(v.x, v.y);
    }
    endShape(CLOSE);
    pop();
  }
}

// Ball class (extends TossedObject)
class Ball extends TossedObject {
  constructor(x, y, mass) {
    super(x, y, mass);
    this.airResistance = 0.005; // Less air resistance (smoother)
    this.color = color(220, 60, 40);
  }
  
  display() {
    push();
    translate(this.position.x, this.position.y);
    fill(this.color);
    stroke(180, 30, 20);
    strokeWeight(1);
    ellipse(0, 0, this.size, this.size);
    
    // Add lines to show rotation
    rotate(this.angle);
    line(-this.size/2, 0, this.size/2, 0);
    line(0, -this.size/2, 0, this.size/2);
    pop();
  }
}

// Box class (extends TossedObject)
class Box extends TossedObject {
  constructor(x, y, mass) {
    super(x, y, mass);
    this.airResistance = 0.015; // More air resistance due to shape
    this.color = color(70, 130, 180);
  }
  
  display() {
    push();
    translate(this.position.x, this.position.y);
    rotate(this.angle);
    fill(this.color);
    stroke(40, 80, 120);
    strokeWeight(1);
    rectMode(CENTER);
    rect(0, 0, this.size, this.size);
    pop();
  }
}

// Star class (extends TossedObject)
class Star extends TossedObject {
  constructor(x, y, mass) {
    super(x, y, mass);
    this.points = 5;
    this.outerRadius = this.size/2;
    this.innerRadius = this.size/4;
    this.airResistance = 0.02; // High air resistance due to complex shape
    this.angularVelocity = random(-0.15, 0.15); // Stars spin more
    this.color = color(220, 220, 40);
  }
  
  display() {
    push();
    translate(this.position.x, this.position.y);
    rotate(this.angle);
    fill(this.color);
    stroke(180, 180, 20);
    strokeWeight(1);
    
    // Draw a star shape
    beginShape();
    for (let i = 0; i < this.points * 2; i++) {
      let radius = (i % 2 === 0) ? this.outerRadius : this.innerRadius;
      let angle = map(i, 0, this.points * 2, 0, TWO_PI);
      let x = cos(angle) * radius;
      let y = sin(angle) * radius;
      vertex(x, y);
    }
    endShape(CLOSE);
    pop();
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
'''

## Explicacion

Qué concepto de cada unidad aplicaste, cómo lo aplicaste y por qué?

Los conceptos aplicados fueron los siguiente:

1. Ruido perlin -> aplicado a las particulas del viento en su desplazamiento con el fin de ser organico
2. Onda seno -> aplicado tambien al sistema del viento para que este tenga un movimiento medio senoidal dentro de todo el caos del ruido perlin para simular aun mas naturalidad
3. Motion 101 -> aplicado al movimiento de los elementos lanzados por la catapulta
4. Resistencia al viento y fuerzas -> aplicado a todos los elementos lanzados desde la catapulta, estos elementos son afectados por fuerzas como el viento y la gravedad al igual que interactuar con el viento 100x100 intended

Finalmente el polimorfismo fue incorporado para el tipo de objeto a ser lanzado y la memoria gestionaba la creacion y destruccion no solo de particulas si no tambien de los elementos arrojables de l misma manera con su lista y su splice().

## Captura de Pantalla
![image](https://github.com/user-attachments/assets/9a0f0bdb-4548-466a-a53c-5ca64423594c)
