# CODE

let particles = [];
let font;
let points = [];
let formingText = false;
let message = "A L I V E";
let textSizeFactor;

function preload() {
  font = loadFont('Main.ttf');
}

function setup() {
  createCanvas(1920, 1080);
  textAlign(CENTER, CENTER);
  textSizeFactor = min(width, height) / 3; // Adjusted text size factor for better clarity
  initializeParticles();
}

function draw() {
  background(255);
  for (let i = particles.length - 1; i >= 0; i--) {
    particles[i].update();
    particles[i].display();
    if (!particles[i].valid) {
      particles.splice(i, 1); // Remove invalid particles
    }
  }
}

function keyPressed() {
  if (!formingText) {
    formingText = true;
    points = font.textToPoints(message, width / 2 - textSizeFactor * 2.5, height / 2 + textSizeFactor / 3, textSizeFactor, {
      sampleFactor: 0.4 // Increased sample factor for better letter clarity
    });
    adjustParticles();
  }
}

function initializeParticles() {
  let numParticles = 2000; // Increased number of particles for more density
  for (let i = 0; i < numParticles; i++) {
    particles.push(new Particle(random(width), random(height)));
  }
}

function adjustParticles() {
  let requiredParticles = points.length;
  while (particles.length > requiredParticles) {
    particles.pop(); // Remove excess particles
  }
  while (particles.length < requiredParticles) {
    particles.push(new Particle(random(width), random(height)));
  }
  
  for (let i = 0; i < particles.length; i++) {
    let target = points[i];
    particles[i].setTarget(target.x, target.y);
  }
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(-1, 1)); // Reduced initial random movement
    this.acceleration = createVector(0, 0);
    this.maxSpeed = 2; // Slower movement for more precision
    this.size = 3;
    this.target = this.position.copy();
    this.arrived = false;
    this.valid = true;
  }

  setTarget(x, y) {
    this.target = createVector(x, y);
  }

  update() {
    if (formingText) {
      let force = p5.Vector.sub(this.target, this.position);
      if (force.mag() < 0.2) { // Tighter convergence for better shape
        this.arrived = true;
        this.position = this.target.copy();
        this.velocity.set(0, 0);
      } else {
        force.setMag(0.1); // Reduced force to prevent overshooting
        this.acceleration.add(force);
      }
    }
    
    if (formingText && this.target.mag() === 0) {
      this.valid = false; // Remove particles not contributing to the text
    }
    
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.maxSpeed);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  display() {
    if (this.valid) {
      fill(0);
      noStroke();
      ellipse(this.position.x, this.position.y, this.size);
    }
  }
  
Yo queria que el codigo funcionara mediante inputs de microfono y reconociera la voz sin embargo se salia demasiado de mis conocimientos tecnicos y ya depeneder enteramente de IA no me llamaba la atencion. Para realizar este proyecto use IA para poder generar el codigo, sin embargo le planteamiento y  el entendimiento del codigo si fueron realizados por mi, no ib a aponer un codigo que no conociera como funciona bien.
