
# Evidencias de la unidad 5

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
