
# Evidencias de la unidad 6
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


