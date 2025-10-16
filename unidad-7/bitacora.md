
# Evidencias de la unidad 7

# ACTIVIDAD 2:
## 1. ¿Por qué es necesario Dev Tunnels y cómo funciona conceptualmente?
Dev Tunnels es necesario porque mi servidor (localhost:3000) es privado y mi celular no puede verlo. Dev Tunnels crea un enlace público (una URL) en internet que redirige de forma segura las peticiones que vienen de mi celular directamente al puerto 3000 de mi computadora. Así, mi servidor local se vuelve accesible desde cualquier lugar.

## 2. Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.
touchMoved() es la función de p5.js que se activa sin parar mientras muevo mi dedo en la pantalla, capturando la posición. La variable threshold sirve como filtro: si el movimiento del dedo es muy pequeño (solo un temblor), la app no envía la información al computador. Solo enviamos datos cuando el movimiento es significativo para no saturar la red.

## 3. Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?
Usar la IP local es rápido, pero solo sirve si ambos estamos en el mismo Wi-Fi y mi firewall no molesta. Dev Tunnels es mejor porque me da una URL pública segura (HTTPS) que funciona en cualquier red (incluso con datos móviles), permitiendo probar la app en cualquier sitio.
<img width="1024" height="768" alt="Cuadro comparativo proyecto de investigación ilustrado azul y naranja" src="https://github.com/user-attachments/assets/12b2b9a8-6ab2-4bb3-9f17-76a676195abf" />


