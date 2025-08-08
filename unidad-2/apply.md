# Unidad 2


## 🛠 Fase: Apply

<img width="1193" height="894" alt="Captura de pantalla 2025-08-08 133841" src="https://github.com/user-attachments/assets/2fcc0c1c-732f-4014-9041-f3210d1b7f8c" />


```py
from microbit import *
import utime
import music

# Estados posibles
INIT = 0
SETUP = 1
ACTIVE = 2

estado = INIT
tiempo_bomba = 20000
inicio_activacion = 0
tiempo_restante = tiempo_bomba

def mostrar_segundos(ms):
    segs = ms // 1000
    for s in str(segs):
        display.show(s)
        sleep(300)

while True:

    if estado == INIT:
        display.show(Image.CONFUSED)
        sleep(800)
        estado = SETUP
        display.clear()

    elif estado == SETUP:
        mostrar_segundos(tiempo_bomba)

        if button_a.was_pressed():
            if tiempo_bomba < 60000:
                tiempo_bomba += 1000
                display.show(Image.ARROW_W)
                sleep(250)

        elif button_b.was_pressed():
            if tiempo_bomba > 10000:
                tiempo_bomba -= 1000
                display.show(Image.ARROW_E)
                sleep(250)

        elif accelerometer.was_gesture("shake"):
            estado = ACTIVE
            inicio_activacion = utime.ticks_ms()
            tiempo_restante = tiempo_bomba
            display.clear()

        sleep(80)

    elif estado == ACTIVE:
        ahora = utime.ticks_ms()
        transcurrido = utime.ticks_diff(ahora, inicio_activacion)
        tiempo_restante = tiempo_bomba - transcurrido

        if tiempo_restante > 0:
            mostrar_segundos(tiempo_restante)
        else:
            display.clear()
            display.show(Image.SKULL)
            music.play(music.FUNERAL)
            sleep(1500)
            display.clear()
            tiempo_bomba = 20000
            estado = SETUP
            continue

        if pin_logo.is_touched():
            estado = SETUP
            tiempo_bomba = 20000
            display.clear()

        sleep(100)
```


### VECTORES DE PRUEBAA
### Prueba 1
Inicio: STATE_CONFIG, BOMB_INTERVAL = 20000 ms
Acciones: Presionar botón A 5 veces → luego agitar el micro:bit

Resultado esperado:

Cada pulsación incrementa 1000 ms (total 25000 ms)

Muestra Image.ARROW_N tras cada incremento

Al agitar: cambia a STATE_ARMED, comienza cuenta regresiva desde 25 s

Al llegar a 0: muestra Image.SKULL, suena music.WAWAWAWAA, vuelve a STATE_CONFIG, reinicia BOMB_INTERVAL a 20000 ms

Resultado obtenido:

Tiempo incrementado correctamente a 25000 ms

Flechas hacia arriba mostradas en cada pulsación

Transición a STATE_ARMED correcta

Cuenta regresiva y explosión ejecutadas según lo esperado

Estado y tiempo reiniciados sin errores


### Prueba 2
Inicio: STATE_CONFIG, BOMB_INTERVAL = 20000 ms
Acciones: Presionar botón B 5 veces → agitar → tocar logo antes de llegar a 0

Resultado esperado:

Cada pulsación disminuye 1000 ms (total 15000 ms)

Muestra Image.ARROW_S en cada decremento

Al agitar: cambia a STATE_ARMED con cuenta desde 15 s

Al tocar logo: vuelve a STATE_CONFIG, reinicia tiempo a 20000 ms

No se muestra Image.SKULL, ni suena música

Resultado obtenido:

Tiempo reducido correctamente a 15000 ms

Flechas hacia abajo mostradas

Transición a STATE_ARMED correcta

Se desarmó antes de tiempo con el logo

Sin explosión ni sonido

Regresó a STATE_CONFIG con tiempo reiniciado


### Prueba 3
Inicio: STATE_CONFIG, BOMB_INTERVAL = 20000 ms
Acciones: Presionar A muchas veces (intenta superar 60000 ms) → luego B muchas veces (intenta bajar de 10000 ms) → agitar

Resultado esperado:

Límite superior de 60000 ms respetado (no se pasa)

Límite inferior de 10000 ms respetado (no se baja)

Flechas mostradas correctamente (N/S)

Al agitar: pasa a STATE_ARMED con tiempo válido

Al llegar a 0: muestra Image.SKULL, suena music.WAWAWAWAA, vuelve a STATE_CONFIG, tiempo reiniciado

Resultado obtenido:

No se exceden los límites (máximo 60000 ms, mínimo 10000 ms)

Flechas mostradas correctamente

Estado armado con el último tiempo válido

Detonación correcta al llegar a 0

Reinicio funcional sin fallos
