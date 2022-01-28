# Informe-Thingsboard-
Aprende a usar Thingsboard 

UNIVERSIDAD DE LAS FUERZAS ARMADAS ESPE

DEPARTAMENTO DE ELECTRICA Y ELECTRÓNICA
FUNDAMENTOS DE CIRCUITOS ELECTRICOS

![image](https://user-images.githubusercontent.com/94182617/151582205-a757e2fa-ea9d-43e3-8b9c-955b0e1fcf62.png)

TEMA:
APRENDIENDO A USAR THINGSBOARD 


MARTÍN AUGUSTO CORONEL MOREIRA

TEMA: Diseño de un ejemplo de interfaz de control con thingsboard.
1.	OBJETIVOS
1.1 Objetivo General
Explicar el funcionamiento básico de la plataforma de thingsboard mediante un ejemplo.

1.2 Objetivos Específicos
*	Comprender el funcionamiento y uso de thingsboard de manera teórica.
*	Emplear un ejemplo básico para poder gestionar su utilidad.
*	Detallar las ventajas de usar thingsboard y la facilidad que brinda el programa para crear diferentes bases de datos.

2.	MARCO TEÓRICO

2.1 Qué es thingsboard?

Es una plataforma de IoT (Internet of things o Internet de las cosas) de código abierto. Está centrada en permitir un rápido desarrollo, gestión y escalado de proyectos relacionados con esta tecnología. Además, en ella tendremos acceso a una solución local o en la nube, que estará lista para usar y que habilitará la infraestructura del lado del servidor para las aplicaciones que vayan a utilizarse.

Es compatible con los protocolos de IoT estándar de la industria: MQTT, CoAP y HTTP. Consigue combinar escalabilidad, tolerancia a los fallos y un buen rendimiento a la hora capturar los datos del dispositivo para su procesamiento y control. Esto es posible gracias a que dispone de un servidor de puerta de enlace que se encarga de la comunicación con los dispositivos conectados a la red. Así se logra una gestión ágil y en permanente actualización.

Está construida alrededor de Netty Framework, que brinda soporte para una amplia variedad de protocolos y aplicaciones. Asimismo, se pueden agregar nuevos protocolos de hardware simplemente añadiendo controladores de canal de entrada y salida.

Es una plataforma de gestión de smart city que pueden aprovechar los ayuntamientos; esto se debe a su naturaleza de código abierto. Así, ante un cambio de proveedor como resultado de una licitación, el nuevo no tendrá problemas para adaptarse, lo que contribuye a limitar las ataduras y a buscar siempre las mejores soluciones disponibles en el mercado. Al final los ciudadanos son los que salen ganando, al disfrutar de una ciudad moderna y eficiente.

![image](https://user-images.githubusercontent.com/94182617/151582399-a5cff0f2-2c37-40da-bcb3-b05ae9eb96e7.png)

-	Procesamiento de datos de medición

![image](https://user-images.githubusercontent.com/94182617/151582438-f1d4a407-1c21-48b0-9fa8-721529ec34b8.png)


Imagen de ejemplo. - Humedad relativa, temperatura, velocidad y dirección del viento en un panel para gestión de parques y jardines.

(ThingsBoard. Plataforma para Monitorización de IoT, 2021)


2.2 Ejemplo de un programa en thingsboard

Para realizar la siguiente práctica se tomará un sensor de temperatura DHT11 y DHT22, antes que nada, es importante entender qué es esto:

![image](https://user-images.githubusercontent.com/94182617/151582476-b0913cde-28f2-4dc1-b379-8774382e07df.png)

A continuación, se puede observar una placa de arduino conectada con una resistencia junto con el sensor de temperatura. Los sensores DHT11 y DHT22 son sensores digitales de Temperatura y Humedad, fáciles de implementar con cualquier microcontrolador. Utiliza un sensor capacitivo de humedad y un termistor para medir el aire circundante y solo un pin para la lectura de los datos. Tal vez la desventaja de estos es la velocidad de las lecturas y el tiempo que hay que esperar para tomar nuevas lecturas (nueva lectura después de 2 segundos), pero esto no es tan importante puesto que la Temperatura y Humedad son variables que no cambian muy rápido en el tiempo.


*	Sensor DHT11: Este sensor trabaja con un rango de medición de temperatura de 0 a 50 °C con precisión de ±2.0 °C y un rango de humedad de 20% a 90% RH con precisión de 4% RH. Los ciclos de lectura deben ser como mínimo 1 o 2 segundos.

*	Sensor DHT22: El rango de medición de temperatura es de  -40°C a 80 °C con precisión de ±0.5 °C y rango de humedad de 0 a 100% RH con precisión de 2% RH, el tiempo entre lecturas debe ser de 2 segundos.
(Damián, 2021)


El proyecto que acabamos de ver en la placa de arduino, será el mismo que veremos en el servicio de thingsboard, siguiendo los pasos a continuación:
1.	Iniciar sesión en el servicio de thingsboard con el usuario y contraseña
2.	Ir a la parte de dispositivos y agregar un nuevo dispositivo y agregar un nombre junto con el tipo de dispositivo que será un sensor, y finalmente presionar agregar.
3.	Una vez creado el dispositivo, abrir los detalles y presionar en Administrar credenciales.

![image](https://user-images.githubusercontent.com/94182617/151582533-b66144f8-e1ad-43c9-9c80-9f25a5543b01.png)

4.	Copiar el token de acceso generado automáticamente y guardarlo en el dispositivo ya que más tarde se lo utilizará.
5.	Descargar el archivo del tablero usando el siguiente enlace: https://thingsboard.io/docs/samples/raspberry/resources/dht22temp dashboard v2.json

* Para poder utilizar diferentes paneles podemos importar o exportar los paneles que se vayan haciendo, en este caso ya hay un panel creado que está diseñado específicamente para este tipo de proyectos como se muestra a continuación:

![image](https://user-images.githubusercontent.com/94182617/151582588-e96f8c3c-c800-4f10-9650-608b1728a804.png)

6.	Navegar a la página de Dashboards y haga clic en el botón grande "+" en la parte inferior derecha de la pantalla y luego haga clic en el botón Importar.

![image](https://user-images.githubusercontent.com/94182617/151582644-91afd5ae-ff6f-45ac-8b01-28b09648c370.png)

7.	Una vez que hemos guardado el panel que vamos a usar entramos a la sección de paneles y lo importamos, una vez que se presiona el botón importar se deberá especificar los alias del dispositivo y guardar.
8.	Luego se deberá instalar la biblioteca MQTT el cual es un protocolo de mensajes de telemetría, una vez instalado ejecutar la siguiente instrucción en la consola, pero estando en la Rasberry con el siguiente comando “sudo pip install paho-matt” como se muestra a continuación:

![image](https://user-images.githubusercontent.com/94182617/151582684-a75f19ca-56a5-4542-95a9-813c13c6432b.png)

También se deberá descargar las librerías de Phyton-dev con el comando “sudo apt-get install python-dev”, finalmente descargar una biblioteca más que se encuentra en el siguiente link: git clone https://github.com/adafruit/Adafruit_Python_DHT.git cd Adafruit Python_DHT, y de igual manera ingresar el comando “sydo python setup. py install”.
9.	Ahora sí, una vez terminado todos los pasos podemos comenzar a hace el programa en Phyton.

2.3	Código del programa

-	Código de manera detallada 
*Primero se cran las librerías que vamos a utilizar 
import os
import time
import sys
import Adafruit DHT as dht
import paho.mqtt.client as mqtt
import json

*Poner un nombre del Host del thingsboard e ingresar el token de acceso que lo guardamos con anterioridad
THINGSBOARD HOST= 'serverthings'
ACCESS_TOKEN = 'XDNEL62jVbTcelfw5ntH'

*Se captura en intervalos de 2 segundos y se leer la temperatura y  humedad, también se deberá decir qué cliente se va a usar
INTERVAL=2
sensor _data = {'temperature': 0, 'humidity' : 0}
next_reading = time.time()
00
client = mqtt.Client()

*Acceder al token a través del método “username” y también se deberá incluir el acceso al token que lo teníamos copiado
client.username_pw_set(ACCESS_TOKEN)

*Después nos vamos a conectar a través del servicio mqtt al host donde está instalado el thingsboard, con el puerto por defecto del mqtt 
client. connect (THINGSBOARD_HOST, 1883, 60)
client.loop_start()

*Iniciar un ciclo que se va a estar ejecutando continuamente en el cual vamos a medir cada cierto tiempo la humedad y temperatura
try:
while True:
humidity, temperature = dht.read_retry(dht.DHT11,4)
humidity = round (humidity, 2)
temperature = round (temperature, 2)
print(u"Temperature:(:9)\uooboc,Humidity:(:g]**.format(temperature,humidity))
sensor_data["temperature” ] = temperature
sensor _data[' humidity']= humidity

*Enviar los datos de humedad y temperature al servidor de thingsboard
client.publish('v1/devices/me/telemetry',json.dumps(sensor_data),1)

next_reading += INTERVAL
sleep_time=next_reading-time.time()
if sleep_time > 0:
time.sleep(sleep_time)

pexcept KeyboardInterrupt:
pass

client.loop_stop()
client.disconnect()

-	Código del programa en Python

![image](https://user-images.githubusercontent.com/94182617/151582885-2cc0e754-eabc-49a9-ac28-aa78b26a41e1.png)

![image](https://user-images.githubusercontent.com/94182617/151582901-e01e26a7-631c-43a5-9964-4d2c6985b4f1.png)


*	Ejecutar con Python con nombre de nuestro archivo

*	Finalmente, abrir la interfaz de usuario web de ThingsBoard, ir a la sección "Dispositivos" y buscar "DHT11", abra los detalles del "DHT", abrir los detalles del dispositivo y cambiar a la pestaña "Última telemetría". Si todo está configurado correctamente, debería poder ver los últimos valores de "temperatura" y "humedad" en la tabla.

2.4	Resultados 

![image](https://user-images.githubusercontent.com/94182617/151582942-1b77c846-eed0-466c-bf6e-88b674f9cac7.png)

o	Como se puede observar está continuamente recibiendo datos del servidor

![image](https://user-images.githubusercontent.com/94182617/151582994-c4d2a997-c89f-48fd-b310-2eaf032dc62b.png)

o	Una vez que lo tengamos podemos entrar a la sección de paneles y abrimos el panel que agregamos un archivo json que descargamos donde ya viene pre configurado el panel que vemos.
o	En este panel podemos ver el cambio de humedad y temperatura que se han dado a través del tiempo, se puede observar que existen variaciones en los datos de cada tabla en tiempo real.
o	Este es llamado panel de visualización de datos en el cual podemos ver que su función es recibir los daros en el servidor de thingsboard en una conexión local que fue establecida en el equipo y los datos que se son enviados son a través de la Rasberry.

![image](https://user-images.githubusercontent.com/94182617/151583077-623742c8-7661-428e-ada3-3af574c4073b.png)

o	En esta sección se puede cambiar el tiempo de visualización como se puede ver en la captura en la cual se modificó la fecha y la hora para obtener los datos de la humedad y temperatura de ese momento en específico.

![image](https://user-images.githubusercontent.com/94182617/151583237-f6554ef4-b430-44df-afd7-c7d6c0f1ee9f.png)

o	Fecha y hora modificada.

![image](https://user-images.githubusercontent.com/94182617/151583294-7fde51f7-e392-42d7-b7e0-50638ec2a22e.png)

o	Otra de las características de thingsboard es que yo puedo obtener diferentes visualizaciones en las cuales yo puedo asignar a diferentes clientes para que puedan visualizar en tablas en caso de que necesite gestionar algún proyecto.

![image](https://user-images.githubusercontent.com/94182617/151583334-fffd25de-723d-4f2e-9879-077134398b08.png)

o	También podemos ver librerías que podemos aplicar a nuestros proyectos, por ejemplo:

![image](https://user-images.githubusercontent.com/94182617/151583398-23ace61d-cea7-48d6-a1c4-15358874c06f.png)

o	Un mapa si queremos que algunos de los sensores tengan algún gps para poder monitorear el lugar en donde se encuentran. 

![image](https://user-images.githubusercontent.com/94182617/151583450-9f33cfc0-5318-48a4-a859-283d809862a8.png)

o	De igual manera otro ejemplo es como se puede ver se puede implementar algún panel de información que nos brinda información importante acerca nuestros proyectos. 

![image](https://user-images.githubusercontent.com/94182617/151583494-13cc815f-9f88-44d8-b176-c4d5b9be91e1.png)

o	Y así, podemos encontrar una gran variedad de opciones y características que podemos implementar a nuestro proyecto de tal manera que se pueda permitir un rápido desarrollo, gestión y escalado de proyectos relacionados con esta tecnología.

¿Cómo crear un proyecto en thingboard?

Paso 1: Iniciar sesión en la página de thingsboard

![image](https://user-images.githubusercontent.com/94182617/151584183-ee4b06e9-4c50-47b0-8cb8-54af3759bda8.png)

Paso 2: En la sección de paneles se podrá encontrar varios ejemplos de paneles que viene en thingsboard.

![image](https://user-images.githubusercontent.com/94182617/151584299-7c714eed-7d45-4d3b-8b14-956b003f4f99.png)

Paso 3: Abrir cualquier panel y dar click en abrir panel.

![image](https://user-images.githubusercontent.com/94182617/151584362-41c0e7cc-4d10-4133-9f1d-862e98841679.png)

Como se puede observar, este panel a continuación, muestra la carga de estación en un mapa y este brinda información en tiempo real con diferentes datos del mismo.

Paso 4: Para crear un panel con widgets hay que regresar a paneles y agregar un nuevo panel.

![image](https://user-images.githubusercontent.com/94182617/151584448-b4355444-c880-48eb-ad2f-88cbc7218fe7.png)

En este caso el nombre del panel es ejemplo y como se puede ver es un panel vacío que hay que poner los widgets.

Paso 5: Presionar en el lápiz que se encuentra que la esquina inferior izquierda y poner en crear un nuevo widget.

![image](https://user-images.githubusercontent.com/94182617/151584555-f140e74c-86b4-4927-9728-1594dcd1900f.png)

Paso 6: Colocar cualquier widget, por ejemplo, un gráfico de series de barra temporal.

![image](https://user-images.githubusercontent.com/94182617/151584641-ba9d47e7-81bf-4a2d-b036-eef4ac82b8d6.png)

Paso 7: Agregar el grafico 

![image](https://user-images.githubusercontent.com/94182617/151584699-43231749-b6b4-4827-aff6-9deb2612e3d2.png)

Paso 8: De igual manera se puede importar otros widgets, regresar a la parte de paneles e ingresar a cualquiera de ellos y guardar el widget que desee utilizar, una vez guardado regresar al panel y dar click en el lápiz, presionar en importar widget.

![image](https://user-images.githubusercontent.com/94182617/151584808-62a3c2a9-1f74-4866-bfd4-43c455e145a6.png)

En este widget descargo el mapa que se observa a la derecha para ponerlo en mi Proyecto.

![image](https://user-images.githubusercontent.com/94182617/151584858-817a7f3f-6d93-4518-9c2e-750b020d1a57.png)

Paso 9: Finalmente presionar en importar y se tendrá el widget que se descargó con anterioridad.

![image](https://user-images.githubusercontent.com/94182617/151584922-6839a146-cadd-4532-8569-480355885747.png)

Y así, se puede ir creando el proyecto con la variedad de widgets que brinda el programa.

3.	Conclusiones:

•	ThingsBoard al ser una plataforma IoT de código abierto se concluye que en este podemos almacenar, visualizar y analizar los datos de nuestros dispositivos, de manera rápida y entretenida.

•	Se pudo determinar que el funcionamiento principal de este programa es unir todas las demás características de Panel de pruebas y permitir configurar y administrar dispositivos de IoT a través de la puerta de enlace usando los widgets y paneles de control de Thingsboard.

•	Como conclusión el programa Thingsboard cumple con su función de recopilación de datos de telemetría: puede recopilar y almacenar datos de telemetría de manera confiable para hacer frente a fallas de red y hardware, se usa un panel web personalizable o una API del lado del servidor para acceder a los datos recopilados. 

4.	Recomendaciones:

•	Para utilizar Thingsboard es importante tomar en cuenta que si el programa se va a utilizar de manera profesional, de preferencia se recomienda instalar el programa pese a ser un procesos engorroso y un poco complejo, sim embargo todos los beneficios que ofrecen el programa vale la pena.

•	Se recomienda tener previo conocimiento acerca del uso y manejo de dicho programa ya que existen gran variedad de funciones, alrededor de 30 widgets que están listos para usar y de igual manera uno mismo los puede crear.

•	Este programa brinda la posibilidad de proporcionar un proyecto integrado con varias herramientas tecnológicas las cuales se recomienda usar para tner un proyecto dinámico y de calidad, en el que no es necesario aprender un lenguaje de programación muy avanzado.

5.	Video:

Parte 1:
https://www.youtube.com/watch?v=gY0_OqnhTro

Parte 2:
https://www.youtube.com/watch?v=7mLttAnU30s


6.	Bibliografías y Referencias: 

G. (2020, 7 mayo). Raspberry Pi 3 - 11 Practica DHT11 Enviar datos a servicio local Thingsboard [Vídeo]. YouTube. https://www.youtube.com/watch?v=mrBB25wCnxM

Introducción a la plataforma en la nube de IoT de código abierto Thingsboard. (2020). programador click. Recuperado 20 de enero de 2022, de https://programmerclick.com/article/89841896174/

Nueva plataforma IoT de código abierto. (2018, 14 enero). soloelectronicos. Recuperado 20 de enero de 2022, de https://soloelectronicos.com/2018/01/14/nueva-plataforma-iot-de-codigo-abierto/
