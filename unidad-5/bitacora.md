
# Evidencias de la unidad 5
# ACTIVIDAD 1
### 1. Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?

El micro:bit se comunica con el navegador a través de UART (puerto serie a 115200 baudios). Cada 100 ms (10 veces por segundo) envía un mensaje en ASCII con 4 datos separados por comas:

* xValue: posición en el eje X del acelerómetro.
* yValue: posición en el eje Y del acelerómetro.
* aState: estado del botón A (True/False).
* bState: estado del botón B (True/False).

El sketch en p5.js recibe esa cadena, la interpreta y la usa para dibujar.

### 2. ¿Cómo es la estructura del protocolo ASCII usado?

Cada mensaje sigue esta estructura:

xValue,yValue,aState,bState\n


### EJEMPLO DE LO QUE MAS O MENOS SE VERIA EN LA CAPTURA DE PANTALLA (PROXIMAMENTE):
```
-123,456,True,False
```


* Los valores están separados por comas.
* El salto de línea \n indica el final del mensaje.
* Es un protocolo legible por uno  mismo, lo que facilita depuración, pero ocupa más espacio que binario.

### 3. Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.
```
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    }
  }
}
```

* El puerto serie se lee hasta \n.
* La cadena se divide por comas en un arreglo de 4 elementos.
* xValue y yValue se convierten a enteros y se ajustan al centro de la pantalla (+ windowWidth/2 y + windowHeight/2).
* aState y bState se transforman en booleanos (true o false).

### 4. ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?

En la función updateButtonStates(newAState, newBState) se comparan los estados actuales (newAState, newBState) con los estados previos (prevmicroBitAState, prevmicroBitBState):
```
if (newAState === true && prevmicroBitAState === false) {
  lineModuleSize = random(50, 160);
  clickPosX = microBitX;
  clickPosY = microBitY;
  print("A pressed");
}
```
```
if (newBState === false && prevmicroBitBState === true) {
  c = color(random(255), random(255), random(255), random(80, 100));
  print("B released");
}
```


* A pressed se detecta cuando antes estaba en false y ahora está en true.
* B released se detecta cuando antes estaba en true y ahora pasa a false.

Así se generan eventos en p5.js basados en los datos que envía el micro:bit.

![prueba2](https://github.com/user-attachments/assets/363fe9df-3e7d-49a6-941c-4d1b7bd4d99e)
![pruebas](https://github.com/user-attachments/assets/18992595-0506-4cdf-b426-297d124bff3d)



# ACTIVIDAD 2
### 1. 
<img width="1919" height="938" alt="1" src="https://github.com/user-attachments/assets/efc8eca0-e4f5-4634-99b0-87e305f43bbd" />
Cuando muestro los datos binarios como tectp ASCII los caracteres que me manda son extraños, no son legibles, esto porque estan codificados en binario. Los bytes representan valors numericos en formato compacto y por eso no se pueden leer como un texto.

### 2.
<img width="1919" height="937" alt="2" src="https://github.com/user-attachments/assets/a59e3ae7-0c1c-4720-93fc-bf2cc90a3d12" />
Para ver los datos correctamente hay que mostrarlos en formato hexadecimal o interpretarlos correctamente con un programa que decodifique el formato binario.

### Como se relaciona esto con la línea de código????

Esto se relaciona con la línea de código data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState)) ya que el formato >2h2B indica que se envían 2 enteros cortos (2h, 16 bits cada uno) para xValue y yValue, y 2 enteros sin signo (2B, 8 bits cada uno) para aState y bState, en orden big-endian (>), es decir, con el byte más significativo primero. Por eso, cada mensaje consta de 6 bytes en total.

### 3.
### ¿Por qué es más difícil leer el binario que el texto ASCII?
El binario es más difícil de leer porque, aunque es compacto y eficiente, no resulta comprensible para uno.
En cambio, el texto ASCII es legible, pero consume más espacio al representar la información.
Por ejemplo, el número 1024 en ASCII se envía como los caracteres “1, 0, 2, 4”, ocupando 4 bytes.
En binario el mismo valor se transmite en solo 2 bytes lo que reduce el tamaño y aumenta la velocidad.

### 4.
### VENTAJAS Y DESVENTAJAS: FORMATO BINARIO VS. TEXTO ASCII
<img width="1024" height="768" alt="Cuadro comparativo proyecto de investigación ilustrado azul y naranja" src="https://github.com/user-attachments/assets/cf356c5e-7226-428b-8b81-289cd7c5c86a" />

### 5.
### SHAKE
<img width="979" height="175" alt="3" src="https://github.com/user-attachments/assets/cfb848ad-da69-492d-9d97-88a3272b85f9" />
<img width="988" height="200" alt="4" src="https://github.com/user-attachments/assets/0764fd81-3bd0-406a-aeb3-2f920c6842c9" />

El micro:bit solo envía datos cuando detecta el gesto de “shake”. Al agitarlo, se transmiten 6 bytes por mensaje. Esto concuerda con el formato >2h2B, donde se envían dos valores del acelerómetro (2 bytes cada uno) y dos estados de botones (1 byte cada uno). Los datos aparecen correctamente en hexadecimal al visualizarse con la aplicación de puerto serial.

### ¿Qué diferencias hay entre los datos en ASCII y en binario?

En binario los datos son compactos, se transmiten rápido, pero son ilegibles para humanos.

En ASCII los datos son más largos y lentos de procesar, pero fáciles de leer y depurar.

### ¿Qué ventajas y desventajas se ven en binario?

### Ventajas: 
compacto, eficiente, rápido de transmitir.

### Desventajas: 
ilegible para humanos, dependes del formato exacto.

### ¿Qué ventajas y desventajas se ven en ASCII?

### Ventajas: 
legible, fácil de depurar.

### Desventajas: 
ocupa más espacio, más lento de procesar.

## PREGUNTAS DE REFLEXIÓN: 
### ¿En qué situaciones reales sería mejor usar binario en lugar de ASCII?
Cuando necesite transmitir datos rapidamente y con poco espacio como en sensores, algun videojuego o comunicacion entre dispositivos.

### ¿Cómo podrías combinar lo mejor de ambos mundos (binario + ASCII) en un mismo sistema de comunicación?
Podria enviar los datos en binario para procesarlos y mandar una copia en ASCII para depurarlos.

### ¿Qué impacto tendría en la memoria y en la velocidad si en lugar de h se usa i (enteros de 32 bits) para xValue y yValue?
Seria mas grande el mensaje por ahi 10 bytes en vez de 6 y tardaria un poco mas en transmitirse pero permitiria números mas grandes.

### ¿Qué pasaría si otro dispositivo recibiera estos datos binarios sin conocer el formato >2h2B?

Los datos binarios son solo una secuencia de bytes, sin un significado por sí mismos. El significado se lo da el formato que define cómo deben interpretarse. Si el otro dispositivo no sabe que esos 6 bytes están organizados como xValue (2 bytes), yValue (2 bytes), aState (1 byte), bState (1 byte), lo único que verá serán valores que parecen símbolos o números extraños.

En ASCII en cambio si no sabes el formato puedes intuir que estos son números separados de comas: -123,456,1,0. Es como recibir un mensaje cifrado: sin la clave del formato, no puedes entender el contenido.

# ACTIVIDAD 3
### 1. ¿Por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario?

En la unidad anterior, los datos se enviaban como texto (strings), por ejemplo:
```
"500,524,True,False\n"
```
Entonces, necesitábamos un delimitador (como la coma ,) para separar cada valor y un salto de línea (\n) para saber cuándo terminaba un paquete.

En cambio, ahora los datos se envían como binarios, en un tamaño fijo de 6 bytes, entonces ya sabemos exactamente cuántos bytes corresponden a cada dato (2 bytes para x, 2 para y, 1 para aState y 1 para bState). Como el tamaño es siempre el mismo, no se necesita ningún carácter especial para saber dónde empieza o termina el paquete.


### 2. ¿Qué cambios observas entre el código anterior y el actual al recibir los datos seriales?
### Antes:
Se leían líneas de texto (port.readLine()) y se separaban los valores con .split(',').

### Ahora:
Se leen directamente 6 bytes con port.readBytes(6), y se interpretan usando DataView como números binarios (enteros y booleanos).


* Y ahora se utiliza DataView para leer esos bytes como getInt16 (para x e y) y getUint8 (para aState y bState), que son lecturas más precisas y seguras para datos binarios.


### 3. ¿Qué ves en la consola? ¿Por qué crees que se produce este error?

Cuando ejecuto el código varias veces, veo que a veces aparecen valores extraños o inesperados, como:
```
microBitX: 500 microBitY: 524
microBitX: 3073 microBitY: 1
```

Esto pasa porque el programa de p5.js lee mal los datos, como si empezara a leer desde la mitad de un paquete, o mezclando bytes de dos paquetes distintos.

Es un error de sincronización. Como no hay una forma de saber dónde empieza el paquete (porque todos los bytes parecen válidos), se pierde la alineación correcta, y entonces se interpretan mal los valores.



### 4. ¿Qué cambios tienen los programas y qué puedes observar en la consola del editor de p5.js?


* Se añade un byte de inicio (0xAA) → para marcar el comienzo del paquete.

* Se calcula un checksum (la suma de los 6 bytes de datos, módulo 256) → para asegurar que los datos llegaron bien.

* El paquete ahora tiene 8 bytes: header (1) + data (6) + checksum (1)

### Observaciones en p5.js:

* Se crea un buffer serial que acumula todos los bytes que llegan.

* Se busca el header 0xAA dentro del buffer.

* Solo si hay 8 bytes disponibles y el checksum es válido, se procesan los datos.

* Si hay error de checksum, se descarta el paquete y se sigue buscando el siguiente válido.


## Preguntas que me surgieron como estudiante:
###¿Qué pasa si el byte 0xAA aparece dentro de los datos?

Si un dato binario tiene el valor 0xAA, puede parecer un header. En este caso como el header va solo al principio, y el tamaño es fijo, no hay mucho problema mientras el framing funcione.

### ¿Qué pasaría si el checksum falla muchas veces seguidas?

Son señales de ruido en la conexión, problemas de velocidad (desincronización), cable USB defectuoso. El checksum nos ayuda a detectar el problema, pero no a solucionarlo. Por eso también se puede implementar un contador de errores, o incluso reenviar paquetes.

### ¿Por qué se usa buffer y DataView en p5.js?

Porque en JavaScript no se pueden leer los datos binarios directamente como enteros o bytes. DataView nos permite interpretar cualquier porción de un ArrayBuffer como el tipo que queramos: getInt16, getUint8, etc.

### ¿Qué pasaría si los datos se enviaran a una velocidad más alta (por ejemplo, 1000 Hz)?

Podrían empezar a llegar paquetes más rápido de lo que el programa los puede procesar. Eso haría que el buffer se llene, y podríamos empezar a perder paquetes o tener errores más frecuentes. Por eso se usa sleep(100) en micro:bit (para enviar a solo 10 Hz), que es una frecuencia muy segura para este tipo de proyectos.


# ACTIVIDAD 4: 











