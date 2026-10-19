# Estructuras de control: if-elseif-else

## Ejercicio 1

Sabiendo que la función `rand()` retorna un valor aleatorio entre un rango de dos enteros, generar un valor aleatorio entre 1 y 3 para luego visualizar el número en letra (ej. si se genera el 3, mostrar en la página el string `"tres"`).

## Ejercicio 2

Sabiendo que la función `rand()` retorna un valor aleatorio entre un rango de dos enteros, generar un valor aleatorio entre 1 y 100 y realizar un programa que muestre por pantalla el valor generado indicando si es mayor, menor o igual a 50.

## Ejercicio 3

La función `date()` con el parámetro `'D'` nos devuelve las tres primeras letras del día de la semana en inglés: `Mon`, `Tue`, `Wed`, `Thu`, `Fri`, `Sat`, `Sun`.

Con este pequeño código `$dia_ingles = date('D');` tendremos el día en la variable `$dia_ingles`.

Mostrar el día en español por pantalla con el mensaje: `"El día de la semana es: XXXX"`.

Puedes utilizar la sentencia `if/else` para ir traduciendo de inglés a español.

## Ejercicio 4

En una web de compras nos piden mostrar diferentes mensajes dependiendo del importe de una compra.

- Si la compra es inferior a 30 €, mostraremos un mensaje en negrita diciendo: **"Compra más o te cobraremos 8,95 € de gastos de envío"**.
- Si la compra es superior a 30 € pero inferior a 90 €, debemos mostrar el siguiente mensaje: **"Con sólo X € más podrás tener gastos de envío gratuitos"**, donde X es la cantidad que le falta para llegar a 90 €.
- Si la compra alcanza los 90 €, mostraremos en negrita: **"Gastos de envío incluidos"**.

Genera el importe total de la cesta de forma aleatoria y con 1 decimal, de manera que esté entre 1 y 200 €, y almacénalo en la variable `$total_compra`.

## Ejercicio 5

Escribe un programa que cada vez que se ejecute muestre la tirada de dos dados al azar (número aleatorio entre 1 y 6) y diga si se ha conseguido el objetivo de paridad (queremos sacar primero un valor par y después un valor impar).

## Ejercicio 6

Escribe un programa que cada vez que se ejecute muestre un año al azar (a partir de 1582, fecha de introducción del calendario gregoriano, hasta el año 2100, por ejemplo) y diga si ese año es bisiesto.

Se recuerda que los años bisiestos son múltiplos de 4, pero los múltiplos de 100 no lo son, aunque los múltiplos de 400 sí.

## Ejercicio 7

Escribe un programa que cada vez que se ejecute muestre la tirada de tres dados al azar (3 números aleatorios entre 1 y 6) y diga si ha salido un trío, una pareja o el mayor de los valores obtenidos.

# Estructuras de control: for

## Ejercicio 8

Mostrar la tabla de multiplicar del número 2. Emplea el bucle `for`.

El resultado debe tener el siguiente formato:

```text
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
...
2 x 10 = 20
```

## Ejercicio 9

Escribe un programa que cada vez que se ejecute muestre la tirada de entre 1 y 10 dados al azar y diga el total de puntos obtenidos.

## Ejercicio 10

Escribe un programa que cada vez que se ejecute muestre la tirada de entre 1 y 10 dados al azar y diga el número de valores pares e impares obtenidos.

## Ejercicio 11

Escribe un programa que cada vez que se ejecute muestre la tirada de entre 1 y 10 dados al azar y diga el valor máximo obtenido y el número de veces que se ha obtenido.

## Ejercicio 12

Mostrar en pantalla una tabla de 10 por 10 con los números del 1 al 100.

<table border=1>
<tr><td>1<td>2<td>3<td>4<td>5<td>6<td>7<td>8<td>9<td>10
<tr><td>11<td>12<td>13<td>14<td>15<td>16<td>17<td>18<td>19<td>20
<tr><td>21<td>22<td>23<td>24<td>25<td>26<td>27<td>28<td>29<td>30
<tr><td>31<td>32<td>33<td>34<td>35<td>36<td>37<td>38<td>39<td>40
<tr><td>41<td>42<td>43<td>44<td>45<td>46<td>47<td>48<td>49<td>50
<tr><td>51<td>52<td>53<td>54<td>55<td>56<td>57<td>58<td>59<td>60
<tr><td>61<td>62<td>63<td>64<td>65<td>66<td>67<td>68<td>69<td>70
<tr><td>71<td>72<td>73<td>74<td>75<td>76<td>77<td>78<td>79<td>80
<tr><td>81<td>82<td>83<td>84<td>85<td>86<td>87<td>88<td>89<td>90
<tr><td>91<td>92<td>93<td>94<td>95<td>96<td>97<td>98<td>99<td>100
</table>

## Ejercicio 13

Modifica el ejercicio anterior para que el número de filas y columnas de la tabla estén almacenadas en una constante y, además, se coloreen las filas alternando gris y blanco.

## Ejercicio 14

Imprime una tabla de 4 por 4 que muestre las primeras 4 potencias de los números del 1 al 4 utilizando la función `pow()`.

<table border=1>
<tr><td>1<td>1<td>1<td>1
<tr><td>2<td>4<td>8<td>16
<tr><td>3<td>9<td>27<td>81
<tr><td>4<td>16<td>64<td>256
</table>

# Arrays y arrays asociativos

## Ejercicio 15

Escribe un programa que muestre una tirada de dado al azar y escriba en letras el valor obtenido. Debes almacenar los posibles valores en un array.

## Ejercicio 16

Escribe un programa que muestre una tirada de un número de dados al azar entre 2 y 7. Para guardar los valores debes usar un array. Para imprimir el array utiliza `foreach`.

## Ejercicio 17

Crea un array que almacene los 10 primeros números pares generados mediante un bucle `for`. Imprímelos cada uno en una línea utilizando la estructura de control `foreach`.

## Ejercicio 18

Crea el array asociativo `$v`, en donde se asocia una cadena a un valor numérico generado aleatoriamente, e imprime el resultado usando la estructura de control `foreach`.

Un ejemplo de la impresión sería:

```text
$v[a]=90;
$v[b]=7;
$v[c]=99;
$v[d]=43;
```

## Ejercicio 19

Escribe un programa que genere y muestre por pantalla tres secuencias aleatorias de 10 bits. A continuación, deberá mostrar una cuarta secuencia que indique cuál es el bit más común en esa posición.

Debes usar un array para cada secuencia y `foreach` para imprimirla.

## Ejercicio 20

Crea el código PHP necesario para que el navegador muestre la siguiente tabla (intenta utilizar las mínimas líneas de código posible).

**Ayuda:** Debes utilizar un bucle anidado. Puedes poner en arrays las distintas cadenas que tengas que imprimir (los días de la semana, los tipos de comida, etc.).

<table border=1>
<tr><th></th><th>Lunes</th><th>Martes</th><th>Miércoles</th><th>Jueves</th><th>Viernes</th><th>Sábado</th><th>Domingo</th>
<tr><th>Desayuno</th><td>Desayuno 1</td><td>Desayuno 2</td><td>Desayuno 3</td><td>Desayuno 4</td><td>Desayuno 5</td><td>Desayuno 6</td><td>Desayuno 7</td>
<tr><th>Comida</th><td>Comida 1</td><td>Comida 2</td><td>Comida 3</td><td>Comida 4</td><td>Comida 5</td><td>Comida 6</td><td>Comida 7</td>
<tr><th>Cena</th><td>Cena 1</td><td>Cena 2</td><td>Cena 3</td><td>Cena 4</td><td>Cena 5</td><td>Cena 6</td><td>Cena 7</td>
</table>

## Ejercicio 21

Escribe un programa que muestre la traducción de una palabra al azar a un idioma al azar, empleando dos arrays.

En un array de dimensión 1 almacenarás 5 idiomas, siendo el primero el español, y en otro array de dimensión 2 almacenarás en cada fila la misma palabra traducida en los diferentes idiomas del array de idiomas.

El programa funcionará del siguiente modo:

> La palabra "Monday" en "Inglés" significa "Lunes" en español.

## Ejercicio 22

Escribe un programa:

- Que muestre primero un grupo de entre 5 y 10 números al azar entre 1 y 10 (los valores se pueden repetir).
- Que indique cuál es el número más alto y el más bajo. Utiliza funciones sobre arrays.

## Ejercicio 23

Escribe un programa:

- Que muestre primero un grupo de entre 7 y 20 números al azar.
- Que indique cuántas veces ha aparecido cada número. Utiliza funciones sobre arrays.

## Ejercicio 24

Escribe un programa que muestre una tirada de un número de dados al azar entre 2 y 7 y los ordene de menor a mayor.

Utiliza una función para ordenar.

## Ejercicio 25

**Ejercicio de recorrido de arrays:** Realiza un programa para procesar una estructura de datos (array asociativo) con información sobre la clasificación de los pilotos de F1 en las diferentes carreras.

Los resultados de las carreras son los siguientes:

```php
$clasificacion['Alonso']['Valencia'] = 1;
$clasificacion['Hamilton']['Valencia'] = 4;
$clasificacion['Massa']['Valencia'] = 2;
$clasificacion['Raikonen']['Valencia'] = 3;

$clasificacion['Alonso']['China'] = 1;
$clasificacion['Hamilton']['China'] = 4;
$clasificacion['Massa']['China'] = 2;
$clasificacion['Raikonen']['China'] = 3;

$clasificacion['Alonso']['Brasil'] = 1;
$clasificacion['Hamilton']['Brasil'] = 4;
$clasificacion['Massa']['Brasil'] = 2;
$clasificacion['Raikonen']['Brasil'] = 3;
```

Para la clasificación final, los pilotos puntúan de la siguiente forma (te será más fácil manejar estos datos si los guardas en otro array):

| Posición | Puntos |
|---|---:|
| 1.º | 10 |
| 2.º | 8 |
| 3.º | 7 |
| 4.º | 6 |
| 5.º | 4 |
| 6.º | 3 |
| 7.º | 2 |
| 8.º | 1 |

Realiza un programa que recorra el array y muestre la clasificación final, es decir, el total de puntos obtenido por cada piloto. El resultado debe ser el siguiente:

### Clasificación del Mundial de Fórmula 1

| Piloto | Puntos |
|---|---:|
| Alonso | 30 |
| Massa | 24 |
| Raikonen | 21 |
| Hamilton | 18 |