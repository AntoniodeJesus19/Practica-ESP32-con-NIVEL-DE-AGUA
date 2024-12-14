# Practica-ESP32-con-NIVEL-DE-AGUA

Utilizaremos la ESP32 en un entorno de adquisición de datos, le conectaremos un sensor Ultrasónico y una pantalla LCD que nos dirá el nivel de agua de un deposito en porcentaje; todo esto se hará en el simulador [WOKWI](https://wokwi.com/).



## Material Necesario
- [WOKWI](https://wokwi.com/)
- Trajeta ESP32
- Sensor Ultrasónico
- pantalla LCD I2C



## Instrucciones

### Requisitos Previos

Necesitas abrir la la pagina [WOKWI](https://wokwi.com/).


### Preparación del entorno

1. Ya en la plataforma debes seleccionar la tarjeta que usaremos en este caso seria la  ```ESP32```.
![](https://github.com/AntoniodeJesus19/Practica-ESP32-con-DHT22/blob/main/Captura%20de%20pantalla%202024-12-09%20223637.png?raw=true)

2. Luego bajamos un poco el cursor y en ```Starter Templates``` seleccionamos ESP32.
![](https://github.com/AntoniodeJesus19/Practica-ESP32-con-DHT22/blob/main/Captura%20de%20pantalla%202024-12-09%20224130.png?raw=true)

3. En la terminal de programacion borramos todo y colocamos la siguiente programación:
```
// defines pins numbers
const int trigPin = 4;
const int echoPin = 15;
const int led1 = 14;
const int led2 = 12;
const int led3 = 26;
const int led4 = 27;

// defines variables
long duration;
int distance;
int safetyDistance;

#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(led1, OUTPUT);
pinMode(led2, OUTPUT);
pinMode(led3, OUTPUT);
pinMode(led4, OUTPUT);
Serial.begin(9600); // Starts the serial communication
 
 lcd.init();
  lcd.backlight();
}


void loop() {
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);

// Calculating the distance
distance= duration*0.034/2;

safetyDistance = distance;
if (safetyDistance>=2 && safetyDistance<=5)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.setCursor(2, 0);
  lcd.print("TANQUE 90 %");
  delay (2000);
  lcd.clear();
}
else if(safetyDistance>=6 && safetyDistance<=10) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
   lcd.setCursor(2, 0);
  lcd.print("TANQUE 75 %");
  delay (2000);
  lcd.clear();
}
else if(safetyDistance>=11 && safetyDistance<=20) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, LOW);
   lcd.setCursor(2, 0);
  lcd.print("TANQUE 50 %");
  delay (2000);
  lcd.clear();
  }
  else if(safetyDistance>=21 && safetyDistance<=30) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
   lcd.setCursor(2, 0);
  lcd.print("TANQUE 25 %");
  delay (2000);
  lcd.clear();
  }
else
{
 digitalWrite(led1,  LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
}


}


```

4. Instalar la libreria **LiquidCrystal I2C**.

![](https://github.com/AntoniodeJesus19/Practica-ESP32-con-NIVEL-DE-AGUA/blob/main/Captura%20de%20pantalla%202024-12-13%20205419.png?raw=true)

6. Seleccionamos nuestro sensor en la parte de ```Simulacion``` en el boton ```+``` y buscamos **Ultrasonico** y **Relay module**, luego buscamos **LCDI2C** y los conectamos de la siguiente manera.
![](https://github.com/AntoniodeJesus19/Practica-ESP32-con-NIVEL-DE-AGUA/blob/main/Captura%20de%20pantalla%202024-12-13%20205038.png?raw=true)


### Instrucciónes de operación

1. Iniciar simulador.
2. Damos click al sensor ultrasonico para fijar una distancia.
3. Visualizar los textos y los datos en la pantalla LCD.


## Resultados

Cuando haya funcionado, verás los valores y los textos en la pantalla LCD.


Si nivel del agua esta entre 2 y 5 cm nos dira q esta lleno el deposito de agua y encendera 1 led.
![](https://github.com/AntoniodeJesus19/Practica-ESP32-con-NIVEL-DE-AGUA/blob/main/Captura%20de%20pantalla%202024-12-13%20205156.png?raw=true)


Si el nivel esta entre los 6 y 10 cm nos marcará que esta a un 75% y prenderan 2 leds.
![](https://github.com/AntoniodeJesus19/Practica-ESP32-con-NIVEL-DE-AGUA/blob/main/Captura%20de%20pantalla%202024-12-13%20205233.png?raw=true)


Si el nivel esta entre los 11 y los 20 cm nos maracá que está a la mitad el display y aparte prenderan 3 leds. 
![](https://github.com/AntoniodeJesus19/Practica-ESP32-con-NIVEL-DE-AGUA/blob/main/Captura%20de%20pantalla%202024-12-13%20205303.png?raw=true)


Sie el nivel esta entre los 21 y 30 cm nos dira el diplay que esta al 25% en lo minimo y encenderan 4 leds.
![](https://github.com/AntoniodeJesus19/Practica-ESP32-con-NIVEL-DE-AGUA/blob/main/Captura%20de%20pantalla%202024-12-13%20205349.png?raw=true)


# Créditos

Desarrollado por Antonio de Jesús Mentado Huerta.

- [GitHub](https://github.com/AntoniodeJesus19)
