# Unidad 1

## 🛠 Fase: Apply

# ACTIVIDAD 6
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
# ACTIVIDAD 5

````
from microbit import *

uart.init(baudrate=115200)

while True:

    if button_a.is_pressed():
        uart.write('A')
    else:
        uart.write('N')

    sleep(100)
````
````
  let port;
  let connectBtn;
  let connectionInitialized = false;

  function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton("Connect to micro:bit");
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
  }

  function draw() {
    background(220);

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let dataRx = port.read(1);
      if (dataRx == "A") {
        fill("red");
      } else if (dataRx == "N") {
        fill("green");
      }
    }

    rectMode(CENTER);
    rect(width / 2, height / 2, 50, 50);

    if (!port.opened()) {
      connectBtn.html("Connect to micro:bit");
    } else {
      connectBtn.html("Disconnect");
    }
  }

  function connectBtnClick() {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
      connectionInitialized = false;
    } else {
      port.close();
    }
  }
````
### EXPLICACIÓN DEL SISTEMA:

Este conjunto de códigos permite que una micro:bit se comunique con una página web mediante comunicación serial. El programa en MicroPython para la micro:bit detecta si el botón A está presionado y envía continuamente por UART la letra 'A' si lo está, o 'N' si no. En paralelo, una interfaz web creada con p5.js utiliza la Web Serial API para conectarse a la micro:bit, leer esos datos y visualizar un rectángulo cuyo color cambia: rojo si recibe 'A' y verde si recibe 'N'. Así, el estado del botón en la micro:bit se refleja en tiempo real en la web, mostrando una interacción sencilla entre hardware y navegador. Despues de todo este sistema funciona de tal manera de que cuando corra en p5.js este mismo dibuje un cuadrado que cuando se presione el boton "A" del microbit el cuadrado cambie de color y vuelve al color original cuando se deje de presionar.
