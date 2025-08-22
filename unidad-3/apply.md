# Unidad 3


## 🛠 Fase: Apply

# P5J
[link](https://editor.p5js.org/lejandrwoo/sketches/SwgsaYpvr)

```js
let taskBomb;
let taskSerial;
let signalEvent;
let serialPort;
let btnConnect;

function setup(){
  createCanvas(400,400);
  textAlign(CENTER,CENTER);
  textSize(32);

  // Puerto y botón
  serialPort = createSerial();
  btnConnect = createButton('Connect To Microbit');
  btnConnect.position(130,300);
  btnConnect.mousePressed(connectBtnClick);

  // Objetos
  signalEvent = new EventSignal();
  taskBomb = new TaskBomb();
  taskSerial = new TaskSerial();
}

function draw(){
  background(0);

  // Actualizar
  taskSerial.update();
  taskBomb.update();

  // Mostrar bomba
  taskBomb.display();
}


class EventSignal {
  constructor(){
    this.value = null;
  }
  set(val){ this.value = val; }   // Guardar
  clear(){ this.value = null; }   // Borrar
  read(){ return this.value; }    // Leer
}


class TaskSerial {
  update(){
    // Leer datos
    if(serialPort.availableBytes() > 0){
      let dataRx = serialPort.read(1);
      if(dataRx === 'A') signalEvent.set('A');
      else if(dataRx === 'B') signalEvent.set('B');
      else if(dataRx === 'S') signalEvent.set('S');
      else if(dataRx === 'T') signalEvent.set('T');
    }

    // Texto del botón
    if (!serialPort.opened()) btnConnect.html('Connect to micro:bit');
    else btnConnect.html('Disconnect');
  }
}


class TaskBomb {
  constructor(){
    this.SECRET = ['A','B','A'];   // Clave
    this.sequence = [];            // Entrada
    this.timer = 20;               // Tiempo
    this.startMillis = millis();   // Reloj
    this.mode = 'CONFIG';          // Estado
  }

  update(){
    if(this.mode === 'CONFIG'){
      // Ajustar tiempo
      if(signalEvent.read() === 'A'){
        signalEvent.clear();
        this.timer = min(this.timer + 1, 60);
      }
      else if(signalEvent.read() === 'B'){
        signalEvent.clear();
        this.timer = max(this.timer - 1, 10);
      }
      // Iniciar
      else if(signalEvent.read() === 'S'){
        signalEvent.clear();
        this.startMillis = millis();
        this.mode = 'ARMED';
      }
    }

    else if(this.mode === 'ARMED'){
      // Cuenta atrás
      if(millis() - this.startMillis > 1000){
        this.timer--;
        this.startMillis = millis();
        if(this.timer <= 0){
          this.mode = 'EXPLODED';
        }
      }

      // Revisar clave
      if(signalEvent.read() === 'A' || signalEvent.read() === 'B'){
        this.sequence.push(signalEvent.read());
        signalEvent.clear();
        if(this.sequence.length === this.SECRET.length){
          if(this.sequence.join('') === this.SECRET.join('')){
            this.mode = 'CONFIG';
            this.timer = 20;
          }
          this.sequence = [];
        }
      }
    }

    else if(this.mode === 'EXPLODED'){
      // Reset
      if(signalEvent.read() === 'T'){
        signalEvent.clear();
        this.mode = 'CONFIG';
        this.timer = 20;
        this.startMillis = millis();
      }
    }
  }

  display(){
    fill(255);
    if(this.mode === 'CONFIG'){
      text(`CONFIG\\n${this.timer}`, width/2, height/2);
    }
    else if(this.mode === 'ARMED'){
      text(`ARMED\\n${this.timer}`, width/2, height/2);
    }
    else if(this.mode === 'EXPLODED'){
      fill(255,0,0);
      text("JOB APPLICATION🔥💼💀", width/2, height/2);
    }
  }
}

function connectBtnClick(){
  // Abrir o cerrar
  if(!serialPort.opened()){
    serialPort.open('MicroPython',115200);
  } else {
    serialPort.close();
  }
}

function keyPressed() {
  // Simular datos
  if (key === 'A') signalEvent.set('A');
  else if (key === 'B') signalEvent.set('B');
  else if (key === 'S') signalEvent.set('S');
  else if (key === 'T') signalEvent.set('T');
}
````
# MICROBIT

```py
from microbit import *

# Alias para los controles
btnA = button_a
btnB = button_b
accel = accelerometer
logoTouch = pin_logo

uart.init(baudrate=115200)
display.show(Image.HAPPY)

while True:
    display.show(Image.HAPPY)
    if btnA.was_pressed():
        uart.write('A')
        display.show(Image.ARROW_N)
        sleep(200)
    if btnB.was_pressed():
        uart.write('B')
        display.show(Image.ARROW_S)
        sleep(200)
    if accel.was_gesture('shake'):
        uart.write('S')
        display.show(Image.SAD)
        sleep(200)
    if logoTouch.is_touched():
        uart.write('T')
        display.show(Image.HAPPY)
        sleep(200)
````
