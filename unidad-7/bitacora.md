
# Evidencias de la unidad 7
# ACTIVIDAD 1:
## ¿Por qué la compu y el celular necesitan códigos (socket ID) diferentes?	
Para que el servidor sepa a cuál de los dos enviarle la respuesta. Si un celular mueve una bolita, el servidor necesita saber a qué otro dispositivo mandarle esa actualización.

## ¿Qué es ese type: 'touch' que se repite tanto?

Es como la etiqueta que le pone el celular al mensaje para decirle al servidor que lo que está enviando son datos de un toque o movimiento.

## Si se conectan 10 celulares, ¿se pondrá lento el servidor?
Probablemente sí, porque tiene que manejar muchos mensajes al mismo tiempo, aunque las librerías de sockets están diseñadas para manejar varias conexiones.
<img width="899" height="461" alt="termianl" src="https://github.com/user-attachments/assets/4abb7ad2-00bb-44dd-b513-7dbfe36b53d1" />

# ACTIVIDAD 2:
## 1. ¿Por qué es necesario Dev Tunnels y cómo funciona conceptualmente?
Dev Tunnels es necesario porque mi servidor (localhost:3000) es privado y mi celular no puede verlo. Dev Tunnels crea un enlace público (una URL) en internet que redirige de forma segura las peticiones que vienen de mi celular directamente al puerto 3000 de mi computadora. Así, mi servidor local se vuelve accesible desde cualquier lugar.

## 2. Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.
touchMoved() es la función de p5.js que se activa sin parar mientras muevo mi dedo en la pantalla, capturando la posición. La variable threshold sirve como filtro: si el movimiento del dedo es muy pequeño (solo un temblor), la app no envía la información al computador. Solo enviamos datos cuando el movimiento es significativo para no saturar la red.

## 3. Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?
Usar la IP local es rápido, pero solo sirve si ambos estamos en el mismo Wi-Fi y mi firewall no molesta. Dev Tunnels es mejor porque me da una URL pública segura (HTTPS) que funciona en cualquier red (incluso con datos móviles), permitiendo probar la app en cualquier sitio.
<img width="1024" height="768" alt="Cuadro comparativo proyecto de investigación ilustrado azul y naranja" src="https://github.com/user-attachments/assets/12b2b9a8-6ab2-4bb3-9f17-76a676195abf" />
<img width="325" height="411" alt="image" src="https://github.com/user-attachments/assets/334a446e-84b0-4c05-9e4d-980fbc876f96" />
<img width="242" height="317" alt="bolita" src="https://github.com/user-attachments/assets/9daf8354-0ff4-4ae6-9c46-1069687d1009" />


# ACTIVIDAD 3:
## 1. Función de express.static('public')
express.static('public') hace que el servidor envíe automáticamente todos los archivos estáticos (HTML, JS, CSS) de la carpeta public sin necesidad de escribir una ruta específica para cada uno. A diferencia de app.get(), que es para rutas específicas, esta función maneja múltiples archivos de golpe, facilitando la carga de nuestra interfaz.

## 2. Flujo de un Mensaje Táctil y Eventos
El mensaje táctil sigue este flujo:

 * Envío desde el móvil: 
El evento touchMoved() en el script de p5.js del móvil detecta el movimiento y, si supera el umbral, usa socket.emit('message', data) para enviarlo.

 * Recepción en el servidor:
El servidor recibe el mensaje con el evento socket.on('message', ...).

 * Acción del servidor:
El servidor registra el mensaje en la consola (console.log) y luego usa socket.broadcast.emit('message', message) para enviarlo de vuelta a todos los demás clientes conectados, excepto al que lo envió (el móvil).

* Envío al escritorio: 
El servidor lo retransmite usando el mismo evento: 'message'.

* Se usa socket.broadcast.emit en lugar de io.emit o socket.emit porque:

* socket.emit enviaría el mensaje solo al cliente que lo envió (el móvil), lo cual no sirve para la retransmisión.

* io.emit enviaría el mensaje a todos los clientes conectados, incluyendo al móvil que lo generó (sería un desperdicio).

* socket.broadcast.emit asegura que el mensaje se retransmita eficientemente a todos los demás clientes, excluyendo al remitente, que es precisamente la función del servidor como "repetidor".

## 3. Escenario de Conexión Múltiple
Si conectamos dos escritorios y un móvil, y el móvil envía el mensaje, solo los dos computadores de escritorio recibirían la señal. El móvil no la recibe porque el servidor usa socket.broadcast.emit, que excluye al cliente que originó el mensaje.

## 4. Información de console.log
Los mensajes console.log son cruciales para depurar: nos avisan cuando un cliente se conecta o se desconecta, y lo más importante, confirman que el servidor recibió los datos del móvil (las coordenadas) justo antes de retransmitirlos.


# ACTIVIDAD 4:
Realiza un diagrama donde muestres el flujo completo de datos y eventos entre los tres componentes: móvil, servidor y escritorio. Puedes ilustrar con un ejemplo de coordenadas táctiles (x, y) y cómo viajan a través del sistema.
<img width="668" height="728" alt="Captura de pantalla 2025-10-17 100029" src="https://github.com/user-attachments/assets/06d55598-d6c7-490c-aa7f-c02ccd5a2cd9" />

# AUTOEVALUACIÓN 
| **Actividad**           | **Estado**     | **Argumento de cumplimiento**                                                                                                                        | **Resultado (valor relativo)** |
| ----------------------- | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| **Actividad 1**         | Completa     | Explica correctamente el uso de **socket ID**, el **type: 'touch'** y el manejo del servidor con varios dispositivos.                                | 5.0                            |
| **Actividad 2**         | Completa     | Describe bien el uso de **Dev Tunnels**, la función **touchMoved()** y la utilidad del **threshold**. Compara de forma clara Dev Tunnels e IP local. | 5.0                            |
| **Actividad 3**         | Completa     | Detalla el flujo del mensaje táctil y el uso de **socket.emit**, **broadcast** y **express.static()**.                                               | 5.0                            |
| **Actividad 4**         | Completa     | Presenta un diagrama del flujo de datos entre **móvil, servidor y escritorio**, con el recorrido de coordenadas.                                     | 5.0                            |
| **Actividad 5 (Apply)** | No realizada | No se hizo la actividad práctica final.                                                                                                              | 0.0                            |
| **Autoevaluación**      | Completa     | Se realizó correctamente.                                                                                                                            | 5.0                            |



