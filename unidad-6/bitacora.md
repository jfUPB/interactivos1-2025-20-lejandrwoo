
# Evidencias de la unidad 6
# ACTIVIDAD 1
## ¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?
<img width="715" height="256" alt="image" src="https://github.com/user-attachments/assets/3b35d5da-1937-47d3-b5bc-fd8d68099d13" />
<img width="252" height="112" alt="image" src="https://github.com/user-attachments/assets/307056b1-94e3-41c9-8dd8-2fd266a57143" />

* Ahi lo que pasa es para descargar un archivo ya que tengo entendido que npm es para administrar librerias y paquetes.

## ¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?
<img width="295" height="53" alt="image" src="https://github.com/user-attachments/assets/ea3e3cf7-94c3-470f-906c-d0f37e1f54c3" />

* El mensaje confirma que se ha iniciado la aplicación. El comando npm start está activando el script start en el package.json, el cual ejecuta el archivo server.js con Node.js.

## Describe lo que ves inicialmente en page1 y page2 en tu navegador.
Hay una bolita roja en cada ventana y estas mismas son unidas por una cuerda que atraviesa la ventana de al lado para llegar a la bolita vecina.
## ¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?
```
Server is listening on http://localhost:3000
A user connected - ID: A6gD9-j2sXhT7mK8wRzYvB5uE3pL
```
## Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? 
Los cambios es que sin importar para donde uno mueva una ventana las bolitas rojas seguiran unidas por la cuerda, ya sea que esten cerca o muy lejos, osea que la ubicación esta constantemente actualizandose para que se vea ese efecto por asi decirlo.

# ACTIVIDAD 2

## 1. Conexión a Internet

En mi casa/universidad me conecto a Internet usando Wi-Fi (a veces también con cable de red). Esa conexión es como mi rampa de acceso a la red. Si esa rampa se corta, no podría entrar a Internet: no abriría páginas web, no cargarían videos ni podría comunicarme por aplicaciones. Básicamente quedo desconectado de la “carretera principal”.

## 2. Ejemplos de Cliente-Servidor en la vida diaria

### Restaurante: 
Yo soy el cliente que pide la comida, el mesero es el servidor que la trae desde la cocina.

### Biblioteca: 
El lector es el cliente, y el bibliotecario es el servidor que entrega el libro solicitado.

### Supermercado: 
Yo pido un producto y el cajero/tienda me lo entrega.

### 3. Analizando una URL

Ejemplo: https://www.youtube.com/watch?v=F6VfsJ7LAlE&list=RDF6VfsJ7LAlE&start_radio=1

Protocolo: https://

Nombre de dominio: www.youtube.com

Ruta: watch?v=F6VfsJ7LAlE&list=RDF6VfsJ7LAlE&start_radio=1

Si solo escribo www.youtube.com, el servidor me envía la página por defecto, que normalmente es la página principal.

## 4. Comparación HTTP vs protocolos seriales

HTTP y los protocolos seriales son reglas de comunicación. La diferencia es que HTTP es más complejo porque maneja códigos de estado, tipos de contenido y seguridad, mientras que el serial solo envía bytes o caracteres.

## 5. HTML, CSS y JavaScript en un formulario de login

### HTML: 
Campos de usuario, contraseña y botón.

### CSS: 
Colores, fuentes y tamaños.

### JavaScript: 
Validación de datos y mensajes de error sin recargar la página.

### 6. Bucle draw() vs modelo basado en eventos

El bucle draw() redibuja todo el tiempo aunque no haya cambios. El modelo de eventos solo actúa cuando ocurre algo, lo que lo hace más eficiente para páginas web.

## 7. Node.js

Node.js permite usar JavaScript en cliente y servidor, lo que facilita el desarrollo y evita aprender dos lenguajes distintos.

# HTTP vs WebSockets/Socket.IO

HTTP funciona como una carta: el navegador envía una petición y espera la respuesta del servidor. En cambio, WebSockets o Socket.IO mantienen una conexión abierta, como una llamada, permitiendo el envío de datos en tiempo real. Esto es útil en aplicaciones donde se necesita velocidad e interacción constante, como chats, videojuegos online, videollamadas, editores colaborativos (como Google Docs), notificaciones en redes sociales o apps de transporte donde ves la ubicación en vivo. Mientras HTTP es ideal para páginas estáticas o formularios, WebSockets se usa cuando la rapidez y la comunicación continua son clave.

# ACTIVIDAD 5:
En esta actividad, la idea principal consistía en recrear una especie de eclipse solar. Durante el desarrollo se presentaron varios problemas evidentes; dos de los más importantes se pueden observar en el video que adjunto. Además, tuve dificultades para comprender cómo hacer que los dos servidores (ventanas) generaran ese "puente" necesario para que la bolita o bolitas cumplieran el objetivo planteado. Aun así, dejo registrado el proceso con los avances que logré alcanzar.
[Enlace video](https://youtube.com/shorts/vUBZzBKCwV0)




