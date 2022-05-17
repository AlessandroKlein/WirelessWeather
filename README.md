## Descripción
Construya su propia estación meteorológica inalámbrica. Esta estación incluye:
- Temperatura
- Humedad
- Presión
- Nivel de lluvia
- Velocidad del viento
- Dirección del viento
- Monitor de batería

Hay tres versiones disponibles:
- Uno usa el módulo ESP8622 y algunos ATTINY
- uno usa ESP32 y solo un ATTINY para la dirección del viento
- se utiliza un Arduino Mini junto con ATTINY24 para la dirección del viento dentro de la estación meteorológica y publicar mensajes por 433 Mhz.

El código y los esquemas para cualquier solución se pueden encontrar en las subcarpetas correspondientes de la carpeta 'código'

## Modo de operación

###ESP8266

La velocidad del viento y la lluvia se detectan mediante la interrupción de cambio de pin de ATTINY.
Hay un dispositivo que consume mucha energía llamado WEMOS D1 mini pro, que duerme profundamente la mayor parte del tiempo.
Cada pocos minutos, se despierta, recopila datos de otros dispositivos mediante I2C, envía todo a su corredor MQTT y vuelve a dormir.

###ESP32

La velocidad del viento y la lluvia se cuentan mediante el coprocesador ULP del módulo ESP32. Cada pocos minutos, ESP32 se despierta del modo de suspensión profunda, lee los valores de conteo de ULP, enciende los dispositivos I2C y envía todo a su corredor MQTT. Luego vuelve a dormir.

### Arduino Pro Mini

Debido a que los dispositivos ESP consumen bastante energía, quería construir algo más ahorrador de energía. Por lo tanto, se utiliza un Arduino Pro Mini dentro de la estación meteorológica. La mayor parte del tiempo duerme y cuenta el viento y la lluvia por interrupciones. Cada x minutos, se activa, enciende los dispositivos I2C (BME280 y ATTINY24 para la dirección del viento), lee los valores y los envía mediante un módulo económico de 433 MHz. Encontrará un ejemplo de trabajo basado en el módulo ESP8266 que actúa como un puente entre 433 Mhz y MQTT, por lo que recibe datos a través de 433 MHz y los publica como antes de usar MQTT.

### Sitio del proyecto

Encuentra todas las piezas impresas en 3D en Thingiverse
https://www.thingiverse.com/thing:3718078

Un video está aquí https://youtu.be/xa0Dt5vs0kM

## Lista de materiales

Este paquete incluye software para los siguientes componentes

###ESP8266

- 2x ATTINY85 (velocidad del viento, lluvia y nivel de batería)
- 1x ATTINY24 (dirección del viento)
- Wemos D1 Mini pro (u otro dispositivo ESP8266)
- 1x BME280
- Busque una lista de materiales completa en el archivo BOM.txt

Además necesitas algún dispositivo para programar ATTINYs. Esto se puede hacer con cualquier dispositivo Arduino. Hay un montón de tutoriales por ahí.

###ESP32

- 1x ATTINY24 (dirección del viento, ver carpeta Wireless Weather)
- ESP32 (DOIT DevKit V1 con 30 GPIO)
- 1x BME280

Para obtener más información, consulte el archivo Léame en la carpeta ESP32

### Arduino Pro Mini

- 1x Arduino Pro Mini
- 1x ATTINY24 (dirección del viento)
- 1x BME280
- 1 receptor de 433 MHz, par de transmisores

También necesita algún código y dispositivo para recibir los datos y procesarlos más. Esto se puede hacer con cualquier dispositivo, como Arduino, ESP8266, ESP32, Raspberry PI, etc. Para obtener un ejemplo de trabajo completo, agregué un código para ESP8266 (WEMOS D1 mini pro) que
actúa como una especie de puente entre 433 MHz y MQTT, lo que significa que recibe los datos enviados por Arduino Pro Mini y los envía mediante el protocolo MQTT.

## Software requerido

Para ATTINYs, necesita este paquete <br>
https://github.com/SpenceKonde/ATTinyCore <br>
https://github.com/rambo/TinyWire <br>

Para ESP8266 y ESP32, usé este <br>
https://arduino.esp8266.com/stable/package_esp8266com_index.json <br>
https://github.com/knolleary/pubsubclient <br>
https://github.com/adafruit/Adafruit_BME280_Library <br>

Al usar Arduino Pro mini, también necesita estos paquetes <br>
https://github.com/rocketscream/Low-Power <br>
https://github.com/PaulStoffregen/RadioHead <br>
https://github.com/adafruit/Adafruit_BME280_Library <br>

## Licencia

<br>Copyright (c) 2019 por Patrick Weber

¡Solo para uso privado! (tienes que pedir un uso comercial)
 

Debería haber recibido una copia de la Licencia Pública General GNU
junto con este programa. Si no, consulte <http://www.gnu.org/licenses/>.

¡Solo para uso privado! (tienes que pedir un uso comercial)

