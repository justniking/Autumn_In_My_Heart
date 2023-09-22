# Autumn_In_My_Heart
let leaves = [];

function setup() {
  createCanvas(800, 600);
  for (let i = 0; i < 50; i++) {
    leaves.push(new Leaf());
  }
}

function draw() {
  background(255, 204, 0);  // Yellow background

  // Ground
  fill(165, 42, 42); // Brown for the ground
  rect(0, height - 50, width, 50);

  // Buildings instead of trees
  drawBuilding(100, height - 200, 30, 150);
  drawBuilding(300, height - 250, 30, 200);
  drawBuilding(500, height - 300, 30, 250);
  drawBuilding(700, height - 220, 30, 170);

  // Display leaves
  for (let leaf of leaves) {
    leaf.update();
    leaf.display();
  }
}

function drawBuilding(x, y, w, h) {
  fill(120, 120, 120); // Gray for building
  rect(x, y, w, h);

  fill(255); // White for windows
  for (let i = x + 5; i < x + w - 5; i += 10) {
    for (let j = y + 5; j < y + h - 5; j += 20) {
      rect(i, j, 5, 10);
    }
  }
}

class Leaf {
  constructor() {
    this.x = random(width);
    this.y = random(height - 50);
    this.speedX = random(-0.5, 0.5);
    this.speedY = random(0.5, 1.5);
    this.size = random(10, 20);
    this.color = color(random(200, 255), random(100, 150), 0);  // Warm shades for leaves
  }

  update() {
    this.x += this.speedX;
    this.y += this.speedY;

    if (this.y > height - 50) {
      this.y = random(height - 50);
      this.x = random(width);
    }
  }

  display() {
    fill(this.color);
    noStroke();

    // Draw leaf shape
    push();
    translate(this.x, this.y);
    beginShape();
    vertex(0, -this.size / 2);
    bezierVertex(this.size / 4, -this.size / 4, this.size / 4, this.size / 4, 0, this.size / 2);
    bezierVertex(-this.size / 4, this.size / 4, -this.size / 4, -this.size / 4, 0, -this.size / 2);
    endShape(CLOSE);
    pop();
  }
}

