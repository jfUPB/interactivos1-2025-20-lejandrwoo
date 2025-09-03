# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_2_3_01)

Código a modificar:

``` js
'use strict';

var formResolution = 15;
var stepSize = 2;
var distortionFactor = 1;
var initRadius = 150;
var centerX;
var centerY;
var x = [];
var y = [];

var filled = false;
var freeze = false;

function setup() {
  createCanvas(windowWidth, windowHeight);

  // init shape
  centerX = width / 2;
  centerY = height / 2;
  var angle = radians(360 / formResolution);
  for (var i = 0; i < formResolution; i++) {
    x.push(cos(angle * i) * initRadius);
    y.push(sin(angle * i) * initRadius);
  }

  stroke(0, 50);
  strokeWeight(0.75);
  background(255);
}

function draw() {
  // floating towards mouse position
  centerX += (mouseX - centerX) * 0.01;
  centerY += (mouseY - centerY) * 0.01;

  // calculate new points
  for (var i = 0; i < formResolution; i++) {
    x[i] += random(-stepSize, stepSize);
    y[i] += random(-stepSize, stepSize);
    // uncomment the following line to show position of the agents
    // ellipse(x[i] + centerX, y[i] + centerY, 5, 5);
  }

  if (filled) {
    fill(random(255));
  } else {
    noFill();
  }

  beginShape();
  // first controlpoint
  curveVertex(x[formResolution - 1] + centerX, y[formResolution - 1] + centerY);

  // only these points are drawn
  for (var i = 0; i < formResolution; i++) {
    curveVertex(x[i] + centerX, y[i] + centerY);
  }
  curveVertex(x[0] + centerX, y[0] + centerY);

  // end controlpoint
  curveVertex(x[1] + centerX, y[1] + centerY);
  endShape();
}

function mousePressed() {
  // init shape on mouse position
  centerX = mouseX;
  centerY = mouseY;
  var angle = radians(360 / formResolution);
  var radius = initRadius * random(0.5, 1);
  for (var i = 0; i < formResolution; i++) {
    x[i] = cos(angle * i) * initRadius;
    y[i] = sin(angle * i) * initRadius;
  }
}

function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (keyCode == DELETE || keyCode == BACKSPACE) background(255);
  if (key == '1') filled = false;
  if (key == '2') filled = true;

  // pauze/play draw loop
  if (key == 'f' || key == 'F') freeze = !freeze;
  if (freeze) {
    noLoop();
  } else {
    loop();
  }
```

[Enlace a la aplicación modificada](https://editor.p5js.org/lejandrwoo/sketches/ItY-6u4nX)

Código modificado:

``` js
'use strict';

var formResolution = 15;
var stepSize = 2;
var initRadius = 150;
var centerX;
var centerY;
var x = [];
var y = [];
var filled = false; 
var freeze = false;

let port;
let reader;
let xValue = 0;
let yValue = 0;
let aState = 0;
let bState = 0;

async function connectMicrobit() {
  try {
    port = await navigator.serial.requestPort();
    await port.open({ baudRate: 115200 });
    reader = port.readable.getReader();
    document.getElementById("status").innerText = "Estado: conectado";

    readLoop();
  } catch (err) {
    console.error("Error conectando al micro:bit: ", err);
  }
}

async function readLoop() {
  const decoder = new TextDecoder();
  let buffer = "";

  while (true) {
    const { value, done } = await reader.read();
    if (done) break;
    buffer += decoder.decode(value, { stream: true });

    let lines = buffer.split("\n");
    buffer = lines.pop();

    for (let line of lines) {
      let parts = line.trim().split(",");
      if (parts.length === 4) {
        xValue = parseInt(parts[0]);
        yValue = parseInt(parts[1]);
        aState = parseInt(parts[2]);
        bState = parseInt(parts[3]);
      }
    }
  }
}

function setup() {
  createCanvas(windowWidth, windowHeight);

  centerX = width / 2;
  centerY = height / 2;
  let angle = radians(360 / formResolution);
  for (let i = 0; i < formResolution; i++) {
    x.push(cos(angle * i) * initRadius);
    y.push(sin(angle * i) * initRadius);
  }

  stroke(0, 50);
  strokeWeight(0.75);
  background(255);


  document.getElementById("connectBtn").addEventListener("click", connectMicrobit);
}

function draw() {

  centerX += (map(xValue, -1024, 1024, 0, width) - centerX) * 0.01;
  centerY += (map(yValue, -1024, 1024, 0, height) - centerY) * 0.01;

  for (let i = 0; i < formResolution; i++) {
    x[i] += random(-stepSize, stepSize);
    y[i] += random(-stepSize, stepSize);
  }

  if (aState === 1) {

    noFill();
  } else if (bState === 1) {

    fill(random(255), random(255), random(255), 100);
  } else {

    if (filled) {
      fill(random(255), random(255), random(255), 100);
    } else {
      noFill();
    }
  }

  beginShape();
  curveVertex(x[formResolution - 1] + centerX, y[formResolution - 1] + centerY);
  for (let i = 0; i < formResolution; i++) {
    curveVertex(x[i] + centerX, y[i] + centerY);
  }
  curveVertex(x[0] + centerX, y[0] + centerY);
  curveVertex(x[1] + centerX, y[1] + centerY);
  endShape();
}

```

## Video

[Video demostratativo](https://youtu.be/9JPW5jZpfYU?si=fGr154uooacDIjNL)


