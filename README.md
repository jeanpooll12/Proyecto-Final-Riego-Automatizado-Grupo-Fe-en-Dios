# Proyecto-Final-Riego-Automatizado-Grupo-Fe-en-Dios
Confiamos en Dios todo poderoso

Proyecto de huerto sostenible <br>
Fundamentos de programación <br>
<br>
Jose Mario Ramos Araujo - 000552420 <br>
Jean Pooll Noriega Navas - 000552072 <br>
Benjamín de Jesús Petro Ramírez - 000547015 <br>
Sebastián julio Villalba - 000 <br>
<br><br>
UNIVERSIDAD PONTIFICIA BOLOBARIANA <br>
FACULTAD DE INGENIERIA Y ARQUITECTURA
<br><br>
Fundamentos De Programación
<br>
MONTERIA<br>
2024<br><br>
##Descripción del problema<br>
Desarrolla un sistema de riego automatizado para una planta que opere en función de la humedad del suelo y el nivel de un suministro de agua. El sistema debe activar la motobomba para regar la planta cuando la humedad del suelo esté por debajo de cierto umbral y el nivel del agua en el recipiente sea suficiente. Además, el sistema debe generar una alerta cuando el nivel del agua en el recipiente esté por debajo de un valor crítico para evitar la activación de la motobomba y prevenir daños al sistema.

##Análisis<br>
El proyecto trata de desarrollar un sistema de riego automatizado que funcione en función de la humedad del suelo y el nivel del agua en un suministro. Este sistema debe activar una motobomba cuando la humedad del suelo esté por debajo de un umbral específico, siempre que el nivel del agua en el recipiente sea suficiente. Además, debe generar una alerta cuando el nivel del agua esté por debajo de un valor crítico para evitar la activación de la motobomba para prevenir daños al sistema.<br><br>
##Componentes y Presupuesto<br>

###Componente<br>
Planta<br>1<br>$7.000 

###componente<br>
Sensor de humedad<br>1<br>$7.800<br>

###componente<br>
Sensor de nivel de agua (Ultrasonido HC-sr04)<br>1<br>$14.000<br>

###componente<br>
Mini bomba de agua sumergible<br>1<br> $10.000<br>

###componente<br>

Microcontrolador (Arduino UNO)<br>1<br>$28.000<br>

###componente<br>

leds verdes, amarillos, rojos<br>5<br>$2.000

###componente<br>

Recipiente para la planta (Maceta)<br>1<br>$3.000

###Componente<br>

Cables (Jumper) hembra + macho<br>15<br>$9.800

###Componente<br>

Caja Plástica Con Tornillos (9x15cmx15cm)<br>1<br>$15.000

###Componentes<br>
Depósito de agua<br>1<br>$5.000

###Componetes<br>
Módulo relay (relé eléctrico)<br>1<br>$10.000

###Componentes<br>
Resistencia 220Ω<br>3<br>$3.000

###Componentes<br>
Modulo bluetooth HC-06<br>1<br>$17.500

###Presupuesto total $200.000 <br>

Total gastado:$131.600<br>


##Componentes del Sistema:<br>
**Planta:**  Duranta, Planta de clima cálido.<br><br>
Fuente de alimentación: conexión de 5v (Voltios) a corriente alterna.<br><br>
**Arduino:** Actúa como el cerebro del sistema. Recibe la información del sensor de humedad del suelo, procesa los datos y controla la activación y desactivación del motor de riego en función de las lecturas de humedad.<br><br>
**Leds:** Estos indican cuando el proyecto esta encendido y dependiendo lo que detecte el ultrasonido indica que la cantidad de agua se encuentra en el recipiente del agua<br><br>
Rele: Se utiliza para controlar la activación del motor de riego.<br><br>
**Motor de riego:** Este componente es responsable de bombear el agua desde un depósito hacia la planta. Se activa cuando el nivel de humedad del suelo cae por debajo de un umbral predefinido y se desactiva después de un período de tiempo determinado.<br><br>
**Ultrasonido:** se utiliza para detectar el nivel del agua el cual detecta a base de hondas el cual cuenta con un emisor que emite ráfagas de ultrasonido en forma de ondas y el receptor recibe las ondas y determina a que distancia máxima de 30cm (Centímetros)<br><br>
**Sensor de Humedad:** se utiliza para medir continuamente el nivel de humedad en el suelo donde se encuentra la planta. Este sensor detectará el nivel actual de humedad y enviará esta información al microcontrolador del sistema.<br><br>
**Depósito de Agua:** Contiene el agua que se utilizará para regar la planta. Debe ser lo suficientemente grande para mantener un suministro adecuado durante un período de tiempo prolongado.<br><br>
**Modulo bluetooth:** Nos permite realizar un enlace entre nuestro portátil o teléfono.<br><br>
**Caja Plástica Con Tornillos** Lo que se encuentra dentro de esta lo que es el arduino, módulo relé, PCB, Modulo bluetooth, conexiones del sensor de humedad, conexiones del motor de riego.<br><br>


SoftwareSerial BTSerial(10, 11); // Configura los pines de Arduino para comunicación serial con el módulo Bluetooth

int trig = 2<br>
int echo = 3<br>
long duracion<br>
long distancia<br>

int verde = 9<br>
int amarillo = 7<br>
int rojo = 6<br>

int bomba = 8<br>
int humedadPin = A0<br>

void setup() {
  Serial.begin(9600)<br>
  BTSerial.begin(9600)<br>

  pinMode(trig, OUTPUT)<br>
  pinMode(echo, INPUT)<br>

  pinMode(verde, OUTPUT)<br>
  pinMode(amarillo, OUTPUT)<br>
  pinMode(rojo, OUTPUT)<br>

  pinMode(bomba, OUTPUT)<br>
}

void loop() {
  digitalWrite(trig, LOW)<br>
  delayMicroseconds(2)<br>
  digitalWrite(trig, HIGH)<br>
  delayMicroseconds(10)<br>
  digitalWrite(trig, LOW)<br>
  
  duracion = pulseIn(echo, HIGH)<br>
  duracion = duracion / 2<br>
  distancia = duracion / 29.15<br>

  if (distancia <= 10) {
        digitalWrite(verde, HIGH) <br>
        digitalWrite(amarillo, LOW)<br>
        digitalWrite(rojo, LOW)<br>
  } else if (distancia <= 20) {
        digitalWrite(verde, LOW)<br>
        digitalWrite(amarillo, HIGH)<br>
        digitalWrite(rojo, LOW)<br>
  } else if (distancia <= 30) {
        digitalWrite(verde, LOW)<br>
        digitalWrite(amarillo, LOW)<br>
        digitalWrite(rojo, HIGH)<br>
  } else {
        digitalWrite(verde, LOW)<br>
        digitalWrite(amarillo, LOW)<br>
        digitalWrite(rojo, LOW)<br>
  }

  int humedadLectura = analogRead(humedadPin)<br>
  int humedad = map(humedadLectura, 0, 1023, 0, 100)<br>

  if (humedad > 60) {
     digitalWrite(bomba, LOW)<br>
  } else {
        digitalWrite(bomba, HIGH)<br>
  }


  BTSerial.print("Distancia: ")<br>
  BTSerial.print(distancia)<br>
  BTSerial.print(" cm, Humedad: ")<br>
  BTSerial.print(humedad)<br>
  BTSerial.println(" %")<br>

  Serial.print("Distancia: ")<br>
  Serial.print(distancia)<br>
  Serial.print(" cm, Humedad: ")<br>
  Serial.print(humedad)<br>
  Serial.println(" %")<br>

delay(1000)<br>
}
------------------------------------------------------------------------
Pseudocódigo<br><br>
START

int trig = 2<br>
int echo = 3<br>
long duracion<br>
long distancia<br>

int verde = 7<br>
int amarillo = 6<br>
int rojo = 9<br>
int bomba = 8<br>
int humedad = 200<br>

void setup()<br>
Serial.begin(9600)<br>

pinMode(trig, OUTPUT)<br>
pinMode(echo, INPUT)<br>
pinMode(verde, OUTPUT) <br>
pinMode(amarillo, OUTPUT) <br>
pinMode(rojo, OUTPUT) <br>
pinMode(bomba, OUTPUT) <br>

void loop()<br>
 digitalWrite(trig, LOW)<br>
 delayMicroseconds(2)<br>
  	digitalWrite(trig, HIGH)<br>
 	 delayMicroseconds(10)<br>
  digitalWrite(trig, LOW)<br>
  
  duracion = pulseIn(echo, HIGH)<br>
  duracion = duracion / 2<br>
  distancia = duracion / 29.15<br>

  Serial.print("La distancia es:   ")<br>
  Serial.print(distancia)<br>
  Serial.println(" cm")<br>

if (distancia <= 6)<br>
digitalWrite(verde, HIGH)<br>
digitalWrite(amarillo, LOW)<br>
digitalWrite(rojo, LOW)  <br>
else if (distancia <= 15)<br>
digitalWrite(verde, LOW)<br>
digitalWrite(amarillo, HIGH)<br>
digitalWrite(rojo, LOW)<br>
else if (distancia <= 30)<br>
digitalWrite(verde, LOW)<br>
digitalWrite(amarillo, LOW)
 	   digitalWrite(rojo, HIGH)<br>
        else<br>
   	 digitalWrite(verde, LOW)<br>
  	  digitalWrite(amarillo, LOW)<br>
                digitalWrite(rojo, LOW)<br>

  humedad = analogRead(A0)<br>
  if (humedad >= 721  humedad <= 1024)<br>
digitalWrite(bomba, LOW)  <br>
  	  digitalWrite(bomba, HIGH)<br>
  
Serial.print("Humedad: ")<br>
Serial.println(humedad)<br>
delay(1000)<br>


STOP<br><br>

##Desarrollo del sistema<br><br>
Paso 1:<br>
•	Conexión del Terminal Emisor (E) del Transistor: Conecta el terminal emisor (E) del transistor a uno de los pines GND (tierra) del Arduino.<br>
•	Conexión del Terminal Colector (C) del Transistor: Conecta el terminal colector (C) del transistor al terminal negativo del motor.<br>
•	Conexión de la Resistencia: Conecta un extremo de una resistencia de 220Ω al terminal base (B) del transistor.<br><br>
Paso 2:<br>
•	Conexión del Otro Extremo de la Resistencia: Conecta el otro extremo de la resistencia al pin digital 8 del Arduino. Este pin controlará la activación del transistor.<br>
•	Conexión del Polo Positivo del Motor: Conecta el polo positivo del motor al polo positivo de la batería de 9V.<br>
•	Conexión del Polo Negativo del Motor: Conecta el polo negativo del motor al colector del transistor.<br><br>
Paso 3:<br>
•	Conexión del Sensor de Humedad:<br>
Conecta el sensor de humedad al pin analógico (A0) del Arduino.<br><br>
Paso 4:<br>
•	Carga del Código:<br>
Se utiliza el código previamente. Se debe asegurar que el código sea cargado correctamente en el arduino.<br><br>
Paso 5:<br>
•	Prueba del Sistema:<br>
Verifica que el sistema funcione correctamente. La motobomba debe activarse cuando la humedad del suelo esté por debajo del umbral y debe desactivarse si el nivel del agua es crítico.<br>
Asegúrate de que las conexiones de la motobomba estén correctas: un cable al terminal base del transistor y el otro al positivo de la batería.<br><br><br>







##Pruebas de funcionamiento<br><br>
Objetivo: verificar que el sistema responde correctamente al código<br><br>
•	Programar el sistema para que se active y desactive dependiendo de la humedad del suelo.<br>
•	Detectar si el sistema se activa y desactiva según la humedad del suelo<br>

Pruebas de precisión: verificar la humedad con la cual encenderá y apagará la bomba<br><br>
•	Insertar el sensor de humedad en cual quien lugar de la maceta para que detecte el nivel<br>
•	Utilizar un método de referencia (medidor de humedad de suelo manual) para medir la humedad en el mismo punto<br>
•	Guardar las lecturas del sensor y del método de referencia
Nota: las lecturas del sensor deben estar dentro de un margen de error aceptable (ejemplo 720)<br><br>
•	Insertar el sensor de humedad en el mismo lugar varias veces, asegurando condiciones constantes<br>
•	Registrar múltiples lecturas del sensor<br>
•	Analizar la variabilidad de las lecturas<br>
Nota: las lecturas deben ser consistentes, con la variabilidad mínima (desviación estándar baja)<br><br>
Pruebas de fiabilidad: Verificar que el sensor de humedad sea capas de soportar largas horas encendido mientras se recopilan los datos.<br><br>
•	Se deja el sensor en el suelo operando durante un periodo prolongado (2 días)<br>
•	Registrar las lecturas del sensor en intervalos de una hora<br>
•	Se identifica cualquier fallo que se haya detectado<br>
Nota: el sensor debe proporcionar lecturas consistentes y precisas durante todo el periodo de prueba y sin fallos.<br><br>
Prueba de los cambios ambientales: el sensor responde a cambios en las condiciones ambientales (temperatura, humedad del aire).<br><br>
•	Se expuso el sensor de humedad a diferentes condiciones ambientales, cambios de temperatura, humedad de aire.<br>
•	Registrar las lecturas del sensor de humedad del suelo antes, durante y después de los cambios ambientales.<br>
•	Analizar la estabilidad y precisión de las lecturas bajo deferentes condiciones.<br>
Nota: El sensor debe mantener una precisión adecuada y no mostrar variaciones significativas debido a los cambias ambientales.<br><br>
Prueba de activación del sistema: El sensor de humedad debe activar y desactivar el sistema de riego según los datos recopilados por la humedad del suelo.<br><br>
•	Programar el sistema de riego para que se active a un umbral de humedad especifico.<br>
•	Comprobar si el sistema de riego activa cuando la humedad del suelo cae por debajo del umbral.<br>
•	Comprobar si el sistema de riego desactiva cuando la humedad está por debajo del umbral.<br>
Nota: El sistema de riego debe activarse y desactivarse correctamente según las lecturas del sensor de humedad.<br><br>
Optimización del consumo de agua: El sensor para optimizar el uso del agua en el sistema de riego.<br><br>
•	Registrar el consumo de humedad durante varios ciclos de riego controlados por el sensor de humedad.<br>
•	Comparar el consumo de agua con y sin el sensor de humedad.<br><br>
Nota: el sensor de humedad debe resultar de una optimización del consumo de agua, si no hay suficiente agua, se bebe generar una alerta de tipo leds en el cual no encienda la motobomba hasta que se vuelva a detectar que hay suficiente agua y asi reduciendo el eso innecesario y asegurando en riego eficiente.<br><br>

