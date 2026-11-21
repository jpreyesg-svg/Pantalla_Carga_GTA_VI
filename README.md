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
#include <Arduino.h>
#include <M5Cardputer.h>

uint32_t start;
int last = -1, beat = -1;
const uint16_t melody[] = {220,330,440,392,196,294,392,330,175,262,349,330,196,294,392,440};
void setup() {
  auto cfg = M5.config();
  M5Cardputer.begin(cfg, false);
  auto &d = M5Cardputer.Display;
  d.setRotation(1);
  if (d.width() < d.height()) d.setRotation(0);
  d.setTextDatum(textdatum_t::middle_center);
  for (int y=0;y<135;++y)
    d.drawFastHLine(0,y,240,d.color565(30+y,8+y/5,78+y/3));
  d.fillCircle(120,62,34,d.color565(255,145,105));
  for(int x=0;x<240;x+=13){
    int h=7+(x*17)%27;
    d.fillRect(x,101-h,11,h,0x180C);
  }
  d.setTextColor(TFT_WHITE);
  d.setTextSize(4);
  d.drawString("GTA VI",120,49);
  d.fillRect(0,101,240,34,0x180C);
  d.drawRect(4,121,232,10,TFT_WHITE);
  M5Cardputer.Speaker.setVolume(80);
  start=millis();
}
void loop(){
  constexpr unsigned long loadMs = 15000;
  auto &d = M5Cardputer.Display;
  if(last==100){
    static int screen=0;
    static unsigned long changed=millis();
    unsigned long elapsed=millis()-changed;
    if(screen==0 && elapsed>=350){
      d.fillScreen(TFT_BLACK);
      d.setTextSize(2);
      d.setTextColor(TFT_RED);
      d.drawString("ERROR CRITICO",120,52);
      d.drawString("DE MEMORIA",120,82);
      screen=1;
      changed=millis();
    } else if(screen==1 && elapsed>=2500){
      d.fillScreen(TFT_BLACK);
      d.setTextColor(TFT_WHITE);
      d.drawString("TRABAJA DURO,",120,36);
      d.drawString("COMPRA PS5,",120,67);
      d.drawString("JUEGALO!",120,98);
      screen=2;
    }
    delay(20);
    return;
  }
  unsigned long t=millis()-start;
  int p=t>=loadMs?100:t/(loadMs/100);
  int b=t/300;
  if(p<100 && b!=beat){beat=b; M5Cardputer.Speaker.tone(melody[b%16],190);}
  if(p!=last){
    last=p;
    int w=230*p/100;
    if(w) d.fillRect(5,122,w,8,0xFF38);
    d.fillRect(0,102,240,18,0x180C);
    d.setTextSize(1);
    if(p==100) d.drawString("100%",120,111);
    else d.drawString(String("CARGANDO  ")+p+"%",120,111);
  }
  delay(8);
}
-----------------------------------------------------------------------------------------------------------------------------------------------
Este código es una broma que simula la pantalla de carga de GTA VI en un dispositivo M5Stack Cardputer.
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
