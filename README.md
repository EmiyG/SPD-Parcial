# Repo Parcial SPD Arduino

![](https://github.com/EmiyG/PacialSpd/blob/main/ArduinoTinkercad.jpg)
# Alumno 
- Emiliano Garcia

# Proyecto Final

![image](https://github.com/EmiyG/PacialSpd/blob/main/Arduino.png)

### 	:computer: Link del Proyecto

[Tinkercard](https://www.tinkercad.com/things/8ZVkhZwQT12)

# Este proyecto esta separado en 3 partes:
### Parte 1: Contador de 0 a 99 con Display 7 Segmentos y Multiplexación
Empiezo diseñando un contador del 0 al 99 utilizando 2 displays de 7 segmentos y 3 botones, 
estos 3 botones permiten sumar, restar y reiniciar el contador.

>**note**
> En este código utilizo la multiplexación para encender los leds de los dos displays a través una misma conexion.

### Parte 2: Modificación con Interruptor Deslizante y Números Primos
Con la base de la primer parte debo agregar un SWITCH con el que dependiendo de la posición del mismo, el display debe 
mostrar o bien el contador (como en la Parte 1) o los números primos en el rango de 0 a 99.

>**note**
> Ahora el codigo cambia, teniendo un interruptor deslizante que te permite optar por mostrar únicamente numeros primos o contar en el orden correcto.

### Parte 2: Investigar
En la parte 2 debí investigar 2 componentes y agregarlos a mi ARDUINO:
-Sensor de temperatura 
-Motor de cc 

Estos mismos tienen cada uno una funcion pero a la vez funcionan juntos, ya que el motor cambia sus revoluciones por minuto dependiendo el valor
del sensor de temperatura.

### Parte 3: Modificación de la parte 2
En esta parte agregue un Fotodiodo el cual tiene la posibilidad de apagar los displays 7 segmentos por completo dependiendo la luz que este mismo reciba.

### MOTOR DE CC

#### Definición
> Motor CC: Los motores de corriente continua a menudo se usan con una caja de engranajes para aumentar el torque mientras se mantienen las pequeñas dimensiones. El motor DC es bastante simple de usar. Para que funcione, lo único que hay que hacer es aplicarle voltaje. La señal y el nivel de voltaje determinarán la velocidad y la dirección de rotación.

### SENSOR DE TEMPERATURA

#### Definicón
>  Un sensor de temperatura es un equipo diseñado para medir la temperatura, para ello trasforma el valor de la temperatura en una señal eléctrica para que pueda ser leída sin dificultad. Estos dispositivos también son conocidos con el nombre de termosensor o sonda de temperatura.

### FOTODIODO

#### Definicón
>  Los fotodiodos se utilizan en instrumentos científicos e industriales para medir la intensidad de la luz, ya sea por sí misma o como medida de alguna otra propiedad

# FUNCIONES

## Funcion Numeros Display
Esta función configura los pines (A, B, C, D, E, F, G) para mostrar un número específico en los display de siete segmentos.
~~~ C (lenguaje en el que esta escrito)
void numerosDisplay(int numero)
{

  switch (numero)
  {
  case 0:
    digitalWrite(A, 1);
    digitalWrite(B, 1);
    digitalWrite(C, 1);
    digitalWrite(D, 1);
    digitalWrite(E, 1);
    digitalWrite(F, 1);
    break;
  case 1:
    digitalWrite(B, 1);
    digitalWrite(C, 1);
    break;
  case 2:
    digitalWrite(A, 1);
    digitalWrite(B, 1);
    digitalWrite(G, 1);
    digitalWrite(E, 1);
    digitalWrite(D, 1);
    break;
  case 3:
    digitalWrite(A, 1);
    digitalWrite(B, 1);
    digitalWrite(G, 1);
    digitalWrite(C, 1);
    digitalWrite(D, 1);
    break;
  case 4:
    digitalWrite(F, 1);
    digitalWrite(B, 1);
    digitalWrite(G, 1);
    digitalWrite(C, 1);
    break;
  case 5:
    digitalWrite(A, 1);
    digitalWrite(F, 1);
    digitalWrite(G, 1);
    digitalWrite(C, 1);
    digitalWrite(D, 1);
    break;
  case 6:
    digitalWrite(A, 1);
    digitalWrite(F, 1);
    digitalWrite(G, 1);
    digitalWrite(C, 1);
    digitalWrite(E, 1);
    digitalWrite(D, 1);
    break;
  case 7:
    digitalWrite(A, 1);
    digitalWrite(B, 1);
    digitalWrite(C, 1);
    break;
  case 8:
    digitalWrite(A, 1);
    digitalWrite(B, 1);
    digitalWrite(C, 1);
    digitalWrite(D, 1);
    digitalWrite(E, 1);
    digitalWrite(F, 1);
    digitalWrite(G, 1);
    break;
  case 9:
    digitalWrite(A, 1);
    digitalWrite(B, 1);
    digitalWrite(C, 1);
    digitalWrite(F, 1);
    digitalWrite(G, 1);
    break;
  default:
    break;
  }
}
~~~

## Funcion Prender Display
Esta función controla la activación o desactivación de dos displays.
~~~ C (lenguaje en el que esta escrito)
void prenderDisplay(int display1, int display2)
{
  digitalWrite(A5, display1);
  digitalWrite(A4, display2);
}
~~~

## Funcion Manejar Display
esta función está diseñada para mostrar un número de dos dígitos en un display de siete segmentos.
~~~ C (lenguaje en el que esta escrito)
void manejarDisplay(int contadorNumeros)
{
  numerosDisplay(contadorNumeros / 10);
  prenderDisplay(1, 0);
  delay(50);
  numerosDisplay(contadorNumeros - 10 * (contadorNumeros / 10));
  prenderDisplay(0, 1);
  delay(50);
}
~~~

## Funcion Tecla Presionada
esta función esta diseñada para detectar si se ha presionado alguno de tres botones específicos.
~~~ C (lenguaje en el que esta escrito)
int teclaPresionada(void)
{
  leerReiniciar = digitalRead(btnReinicio);
  leerSumar = digitalRead(btnSumar);
  leerRestar = digitalRead(btnRestar);

  if (leerSumar == 1)
  {
    sumarAnterior = 1;
  }

  if (leerRestar == 1)
  {
    restarAnterior = 1;
  }
  if (leerReiniciar == 1)
  {
    reiniciarAnterior = 1;
  }

  if (leerSumar == 0 && leerSumar != sumarAnterior)
  {
    sumarAnterior = leerSumar;
    return btnSumar;
  }

  if (leerRestar == 0 && leerRestar != restarAnterior)
  {
    restarAnterior = leerRestar;
    return btnRestar;
  }

  if (leerReiniciar == 0 && leerReiniciar != reiniciarAnterior)
  {
    reiniciarAnterior = leerReiniciar;
    return btnReinicio;
  }
  return 0;
}
~~~


## Funcion Mostrar Numeros Primos
Esta función muestra los numeros primos del 0 al 99
~~~ C (lenguaje en el que esta escrito)
void mostrarNumerosPrimos()
{
  mostrarPrimos = true;
  for (int i = ultimoPrimo + 1; i <= 99; ++i)
  {
    if (esPrimo(i))
    {
      contadorNumeros = i;
      manejarDisplay(contadorNumeros);
      ultimoPrimo = i;
      delay(777);
      if (!mostrarPrimos || teclaPresionada() == btnReinicio)
      {
        mostrarPrimos = false;
        return;
      }
    }
  }
}
~~~

## Funcion Numero Primo
Esta función determina si un número es primo o no
~~~ C (lenguaje en el que esta escrito)
bool esPrimo(int num)
{
  if (num <= 1)
    return false;
  for (int i = 2; i <= num / 2; ++i)
  {
    if (num % i == 0)
      return false;
  }
  return true;
}
~~~


## Funcion Motor
Esta se encarga de regular la velocidad del motor por el sensor de temperatura.
~~~ C (lenguaje en el que esta escrito)
void ajustarVelocidadMotor(int sensorValue)
{
  int velocidad = map(sensorValue, 0, 1023, 0, 255);
  analogWrite(motorPin, velocidad);
}
~~~
