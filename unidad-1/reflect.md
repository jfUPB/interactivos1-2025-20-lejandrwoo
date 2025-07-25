# Unidad 1

## 🤔 Fase: Reflect

# ACTIVIDAD 7:
### PARTE 1:
- 1
SENSORES DE ENTRADA: se detecta información como movimientos, luz, temperatura, botones etc.
PROCESAMIENTO DE INFO: Interpreta las entradas y decide que se hace con eso.
SENSORES DE SALIDA: dan respuestas de info perceptible como movimientos, luz, temperatura, botones etc.

- 2
INPUT: es la entrada, es presionar el boton A del microbit
PROCESS: el microbit detecto la accion y envia un mensaje
OUTPUT: es la salida, creo que es con p5.js que recibe el mensaje y muestra la figura.


- 3
  ¿Cuál es la función de la línea uart.write('A') en el código del micro:bit y qué función en p5.js se encarga de “escuchar” ese mensaje?/: en el MICROBIT wart.write('A') envia la letra 'A' al pc por el puerto serial. EN P5.JS la funcion se activa en automatico cuando llega nueva info por el puerto.

- 4
  ¿Cuál es la diferencia fundamental entre el arte/diseño tradicional y el arte/diseño generativo?
  /: el arte es cuando el crea la obra manual o digitalmente y el arte generativo es cuando el artista con algoritomos de computadora crea arte sonoro, visual o fisicos, puede ser impredecible o no.

- 5
  Imagina que quieres que un círculo en p5.js cambie a un color aleatorio cada vez que sacudes el micro:bit. Describe qué tendrías que programar en el micro:bit y qué tendrías que programar en p5.js para lograrlo.

  /: MICROBIT: no me acuerdo bien de como, pero podria poner un input.onGesture(Gesture.shake y lo demas no se.

  P5.JS: desde el serial event ecuchar un mensaje 'shake' y usar random para que cambie aleatoriamente los colores.


  ### PARTE 2:
  
  
