# Unidad 2

## 🔎 Fase: Set + Seek

# Actividad 01
Analizando un programa con una máquina de estados simple
Analicemos juntos el siguiente código identificando estados, eventos y acciones. Responde las preguntas planteadas.

````
from microbit import *
import utime

class Pixel:
    def __init__(self,pixelX,pixelY,initState,interval):
        self.state = "Init"
        self.startTime = 0
        self.interval = interval
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState

    def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeout"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

        elif self.state == "WaitTimeout":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                if self.pixelState == 9:
                    self.pixelState = 0
                else:
                    self.pixelState = 9
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

pixel1 = Pixel(0,0,0,1000)
pixel2 = Pixel(4,4,0,500)

while True:
    pixel1.update()
    pixel2.update()
````

## Describe detalladamente cómo funciona este ejemplo.
Este código hace que dos LEDs del micro:bit se enciendan y apaguen de manera intermitente, cada uno con un intervalo de tiempo distinto.

- Clase Pixel: Representa un LED con sus coordenadas, brillo inicial y tiempo de espera para alternar entre encendido y apagado.
- Atributos y método update():

pixelX, pixelY: Ubicación del LED.

interval: Tiempo entre cambios.

startTime: Guarda el momento del último cambio.

pixelState: Brillo del LED (0 a 9).
El método update() alterna entre dos estados: "Init" (configuración inicial) y "WaitTimeout" (espera y cambio de brillo).
- Objetos creados:

pixel1: Coordenadas (0,0), parpadea cada 1000 ms.

pixel2: Coordenadas (4,4), parpadea cada 500 ms.

## ¿Cuáles son los estados en el programa?

"Init": Inicializa y muestra el LED con brillo inicial.

"WaitTimeout": Espera y cambia el brillo cuando se cumple el intervalo.

## ¿Cuáles son los eventos/inputs en el programa?

Evento interno: Paso del tiempo (startTime + interval). 
No existen entradas externas como botones.

## ¿Cuáles son las acciones en el programa?

- Dibujar LED inicial.

- Esperar el tiempo definido.

- Alternar entre brillo 0 y 9.

- Actualizar pixel en pantalla.

# Actividad 02
### Implementando un semáforo con máquina de estados
Implementemos juntos un semáforo simple (rojo, amarillo, verde) utilizando una máquina de estados en Micropython. Representaremos cada color del semáforo con un LED del display del micro:bit.



Estados:

RED (rojo)

YELLOW (amarillo)

GREEN (verde)
El estado inicial es RED.

Eventos:

Paso del tiempo:

3 segundos en RED -> GREEN

3 segundos en GREEN  -> YELLOW

1 segundo en YELLOW -> RED

Acciones:

````
.py
from microbit import *
import utime

# Estados 
RED = "Red"
GREEN = "Green"
YELLOW = "Yellow"

# Estado inicial
estado = RED

def mostrar_estado(estado):
    display.clear()
    if estado == RED:
        display.set_pixel(2, 0, 9)  # Rojo arriba
    elif estado == YELLOW:
        display.set_pixel(2, 2, 9)  # Amarillo en el centro
    elif estado == GREEN:
        display.set_pixel(2, 4, 9)  # Verde abajo

# Bucle principal 
while True:
    mostrar_estado(estado)

    if estado == RED:
        utime.sleep(3)
        estado = GREEN
    elif estado == GREEN:
        utime.sleep(3)
        estado = YELLOW
    elif estado == YELLOW:
        utime.sleep(1)
        estado = RED
````
Esta función borra la pantalla y enciende un único LED en la posición y brillo correspondientes al estado actual.

# Actividad 03
### Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.
Porque el código está diseñado para estar pendiente tanto del tiempo como de las entradas del botón sin detenerse, lo que hace posible que responda a ambos casos casi al mismo momento.

### Identifica los estados, eventos y acciones en el programa
### ESTADOS:

INIT

HAPPY

SMILE

SAD

EVENTOS:

Transcurso del tiempo

Presionar el botón A

### ACCIONES:

Mostrar la imagen correspondiente

Cambiar al estado indicado según el evento
Cambiar estado.


