# Unidad 1

## 🛠 Fase: Apply

# ACTIVIDAD 5
[Link al P5JS](https://editor.p5js.org/lejandrwoo/sketches/C4VPwmWh2)

````
from microbit import *

# Inicializa UART
uart.init(baudrate=115200)

while True:
    if button_a.was_pressed():
        uart.write('A/a')
    elif button_b.was_pressed():
        uart.write('B/b')
````    
````
let port;
let connectBtn;
let x = 200;
let ballColor = "green";

function setup() {
  createCanvas(400, 400);
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(10, height + 10);
  connectBtn.mousePressed(toggleConnection);
}

function draw() {
  background(220);

  if (port.opened() && port.availableBytes() > 0) {
    let data = port.read(1);
    if (data === "A") x -= 10, toggleColor();
    if (data === "B") x += 10, toggleColor();
  }

  x = constrain(x, 25, width - 25);
  fill(ballColor);
  noStroke();
  ellipse(x, height / 2, 50);
}

function toggleColor() {
  ballColor = ballColor === "green" ? "red" : "green";
}

function toggleConnection() {
  if (!port.opened()) port.open("MicroPython", 115200);
  else port.close();
}
````
````
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>micro:bit + p5.js</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>
  <script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>
  <script src="sketch.js"></script>
</head>
<body></body>
</html>
````
kkkkkk
