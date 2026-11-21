Pantalla de carga de introducción de GTA VI

Este proyecto recrea la icónica pantalla de carga de GTA VI en una M5 Cardputer, con barra de progreso animada, gráficos temáticos
y los característicos efectos de audio del juego. La guía incluye un diagrama de cableado para conectar la Cardputer ADV,
una lista completa de componentes y el firmware de Arduino necesario para mostrar la secuencia de introducción animada con efectos de sonido.

Los desarrolladores aprenderán a trabajar con las capacidades de pantalla y altavoz del M5Cardputer, implementar animaciones temporizadas y
transiciones de estado, y crear gráficos personalizados mediante la manipulación del color. El proyecto demuestra técnicas prácticas 
para crear pantallas de carga interactivas y sistemas de menú en plataformas integradas compactas.

direccion del proyecto subido a:
https://www.schematik.io/projects/gta-vi-intro-loading-screen-h2wt<img width="3000" height="4000" alt="IMG_20261120_215342" src="https://github.com/user-attachments/assets/44d318eb-82b7-444c-a38b-68fbeacf8f74" />


Codigo fuente Esta escrito en C++ (utilizando el framework de Arduino) Ojo: odio C++ y amo C
----------------------------------------------------------------------------------------------------------------------
El código es una broma que simula la pantalla de carga de GTA VI en un dispositivo M5Stack Cardputer.
Al ejecutarse en esta pequeña computadora de bolsillo basada en ESP32, realiza la siguiente secuencia:

1. Pantalla de inicio (Setup)

• Dibuja un paisaje estilo Vice City: Crea un cielo con degradado púrpura/naranja, un sol brillante en el centro y siluetas de edificios en la parte inferior.
• Muestra el título: Escribe "GTA VI" en letras blancas grandes sobre el paisaje.
• Prepara la barra de carga: Dibuja el contorno vacío de una barra de progreso en la parte inferior y ajusta el volumen del altavoz integrado.

2. Animación y música de carga (Loop)

• Llena la barra: Durante 15 segundos (15000 ms), avanza el porcentaje desde 0% hasta 100% con el texto "CARGANDO X%".
• Reproduce una melodía: Mientras la barra sube, el altavoz emite una secuencia repetitiva de 16 notas musicales (melody) cada 300 milisegundos.

3. El remate o broma final

• Falso error: Apenas llega al 100% (tras esperar 0.35 segundos), la pantalla se pone negra y muestra en rojo: "ERROR CRITICO DE MEMORIA".
• Mensaje motivacional: 2.5 segundos después, borra el error y muestra el mensaje final en blanco: "TRABAJA DURO, COMPRA PS5, JUEGALO!".
Si quieres, puedo ayudarte a:
• Modificar los textos o los tiempos de la broma
• Adaptar el código para otra pantalla o placa Arduino/ESP32
• Explicar línea por línea alguna parte específica del código
