
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

# ACTIVIDAD 3:
## Experimenta:
### ¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas?
La prueba demuestra que el servidor es súper estricto con las direcciones. O sea que el router solo funciona si se pone exactamente la URL que está escrita en el codigo (/pagina_uno). Si le cambiamos una letra aunque sea una mayúscula (/page1), manda error de que no existe.

### Asegúrate de que el servidor esté corriendo (npm start).

### Abre http://localhost:3000/page1 en una pestaña. Observa la terminal del servidor. ¿Qué mensaje ves? Anota el ID.
```
A user connected - ID: J8kWxZpQyH2tL7vC9nMdAAB
```
### Abre http://localhost:3000/page2 en OTRA pestaña. Observa la terminal. ¿Qué mensaje ves? ¿El ID es diferente?
```
A user connected - ID: P9rVtQzLmE1bGfD3cJ0yXXX
```
Es distinto
### Cierra la pestaña de page1. Observa la terminal. ¿Qué mensaje ves? ¿Coincide el ID con el que anotaste?
```
A user connected - ID: J8kWxZpQyH2tL7vC9nMdAAB
```
Es el mismo que anote 
### Inicia el servidor y abre page1 y page2
### Mueve la ventana de page1. Observa la terminal del servidor. ¿Qué evento se registra (win1update o win2update)? ¿Qué datos (Data:) ves?
```
Received win1update from ID: J8kWxZpQyH2tL7vC9nMdAAB Data: { x: 350, y: 55, width: 1280, height: 720 }
```
### Mueve la ventana de page2. Observa la terminal. ¿Qué evento se registra ahora? ¿Qué datos ves?
```
Received win2update from ID: P9rVtQzLmE1bGfD3cJ0yXXX Data: { x: 80, y: 400, width: 1024, height: 768 }
```

### Detén el servidor.

### Cambia const port = 3000; a const port = 3001;.

### Inicia el servidor. ¿Qué mensaje ves en la consola? ¿En qué puerto dice que está escuchando?

### Intenta abrir http://localhost:3000/page1. ¿Funciona?
En este no funciona
### Intenta abrir http://localhost:3001/page1. ¿Funciona?
Este si
### ¿Qué aprendiste sobre la variable port y la función listen? Restaura el puerto a 3000.
El experimento me enseño que la variable port es como el numero de canal que le asignas al servidor. La función listen lo que hace es encender el servidor en ese canal exacto. Si lo cambias a 3001 la pagina vieja en 3000 ya no carga y tocaria ir al canal 3001 a buscarlo.
# ACTIVIDAD 5:
En esta actividad, la idea principal consistía en recrear una especie de eclipse solar. Durante el desarrollo se presentaron varios problemas evidentes; dos de los más importantes se pueden observar en el video que adjunto. Además, tuve dificultades para comprender cómo hacer que los dos servidores (ventanas) generaran ese "puente" necesario para que la bolita o bolitas cumplieran el objetivo planteado. Aun así, dejo registrado el proceso con los avances que logré alcanzar.
[Enlace video](https://youtube.com/shorts/vUBZzBKCwV0)

## REDENCIÓN:
Al final decidi empezar de nuevo con otra cosa, asi que arme un servidor que conecta en tiempo real dos ventanas del navegador, donde cada una representa a un jugador. Yo controlo mi paleta con el mouse y la otra persona controla la suya en su ventana mientras compartimos una sola bola que rebota en las paredes y en las paletas, en pocas palabras hice un pong.
Aca dejare un video con algunas de las pruebas que realice:



https://github.com/user-attachments/assets/cfb7ca11-9e01-4de1-a0dc-2d6d5f5ca1cf


### Códigos:

```
const express = require("express");
const app = express();
const http = require("http").createServer(app);
const io = require("socket.io")(http);

app.use(express.static("public"));

const PORT = 3000;

let CANVAS = { width: 1200, height: 600 };

let players = {};
let scores = { left: 0, right: 0 };

let ball = { x: CANVAS.width / 2, y: CANVAS.height / 2, vx: 5, vy: 3, r: 10 };

function resetBall(side) {
  ball.x = CANVAS.width / 2;
  ball.y = CANVAS.height / 2;
  ball.vx = side === "left" ? 5 : -5;
  ball.vy = 3;
}

io.on("connection", (socket) => {
  console.log("Jugador conectado:", socket.id);

  players[socket.id] = {
    side: Object.keys(players).length === 0 ? "left" : "right",
    y: CANVAS.height / 2,
    h: 100,
    w: 15,
  };

  socket.on("move", (y) => {
    if (players[socket.id]) {
      players[socket.id].y = y;
    }
  });

  socket.on("disconnect", () => {
    delete players[socket.id];
  });
});

setInterval(() => {
  // mover pelota
  ball.x += ball.vx;
  ball.y += ball.vy;

  if (ball.y - ball.r < 0 || ball.y + ball.r > CANVAS.height) {
    ball.vy *= -1;
  }

  for (let id in players) {
    let p = players[id];

    if (p.side === "left") {

      if (
        ball.x - ball.r <= p.w &&
        ball.y >= p.y - p.h / 2 &&
        ball.y <= p.y + p.h / 2
      ) {
        ball.vx = Math.abs(ball.vx);      
        ball.x = p.w + ball.r;            
      }
    }

    if (p.side === "right") {
      // Paleta derecha está en x = CANVAS.width - p.w/2
      if (
        ball.x + ball.r >= CANVAS.width - p.w &&
        ball.y >= p.y - p.h / 2 &&
        ball.y <= p.y + p.h / 2
      ) {
        ball.vx = -Math.abs(ball.vx);     // rebote hacia la izquierda
        ball.x = CANVAS.width - p.w - ball.r;
      }
    }
  }

  // puntos
  if (ball.x - ball.r < 0) {
    scores.right++;
    resetBall("right");
  }
  if (ball.x + ball.r > CANVAS.width) {
    scores.left++;
    resetBall("left");
  }

  io.emit("gameState", { ball, players, scores });
}, 1000 / 60);

http.listen(PORT, () => {
  console.log(`Servidor en http://localhost:${PORT}`);
});
```
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Pong Multiplayer</title>
    <script src="https://cdn.jsdelivr.net/npm/p5@1.4.2/lib/p5.min.js"></script>
    <script src="/socket.io/socket.io.js"></script>
    <script src="sketch.js"></script>
  </head>
  <body style="margin:0; padding:0; overflow:hidden;"></body>
</html>
```
```
let socket;
let ball;
let players = {};
let scores = {};

let side = null; // izquierda o derecha

function setup() {
  createCanvas(windowWidth, windowHeight);
  socket = io();

  socket.on("gameState", (state) => {
    ball = state.ball;
    players = state.players;
    scores = state.scores;
    if (socket.id in players) {
      side = players[socket.id].side;
    }
  });
}

function draw() {
  background(0);

  if (!ball) return;

  stroke(255);
  strokeWeight(2);
  for (let y = 0; y < height; y += 20) {
    line(width / 2, y, width / 2, y + 10);
  }

  noStroke();
  fill(255);

  ellipse(ball.x * (width / 1200), ball.y * (height / 600), 20);

  for (let id in players) {
    let p = players[id];
    let px =
      p.side === "left" ? 20 : width - 20;
    rectMode(CENTER);
    rect(
      px,
      p.y * (height / 600),
      15,
      p.h
    );
  }

  textSize(48);
  textAlign(CENTER, TOP);
  fill(255);
  text(scores.left, width / 4, 20);
  text(scores.right, (3 * width) / 4, 20);
}

function mouseMoved() {
  socket.emit("move", mouseY * (600 / height));
}
```



