# Funciones

## Ejercicio 1

Escribe un programa que, dada una edad en años, diga si esa persona es mayor de edad o no. Para generar la edad utiliza un número aleatorio entre 1 y 99.

Deberás también definir la función que hace la comprobación:

```php
esMayorDeEdad(int $edad): bool
```

## Ejercicio 2

Escribe un programa que genere 2 números aleatorios entre 2 y 10 y cree una tabla HTML que tenga tantas filas como indique el primer número y tantas columnas como indique el segundo número.

El contenido de cada celda será un número que empezará por 1 en la primera celda y se irá incrementando en uno en las celdas siguientes.

Para crear la tabla define la siguiente función:

```php
creaTabla(int $filas, int $cols): string
```

## Ejercicio 3

Escribe un programa que calcule la letra del NIF a partir del número. Para ello, define las siguientes funciones:

- `generaNumero(): int`: para generar el número del NIF puedes utilizar un número aleatorio entre 1 y 99999999.
- `calculaLetraNIF(int $num): string`: para calcular la letra del NIF se divide el número del DNI entre 23 y, según el resto (0..22), se elegirá una letra de la siguiente cadena: `"TRWAGMYFPDXBNJZSQVHLCKEW"`.

Para imprimir el DNI, recuerda que debes imprimir un número con 8 cifras enteras, es decir, deberás rellenar con ceros por la izquierda. Para ello utiliza la función `str_pad()`.

## Ejercicio 4

Escribe un programa que muestre entre 5 y 10 tiradas de dados (números entre el 1 y el 6), primero sin ordenar, después ordenados y, por último, eliminando los dados repetidos.

Para ello, define las siguientes funciones:

```php
generaMatrizEnterosRand(int $n, int $min, int $max): array
```

Los argumentos `$n`, `$min` y `$max` son números enteros.

La función devuelve una matriz de `$n` valores enteros aleatorios entre `$min` y `$max`, ambos incluidos.

```php
escribeValoresDados(array $m): void
```

El argumento `$m` es una matriz de valores de dados (como la que genera la función `generaMatrizEnterosRand()` anterior).

## Ejercicio 5

Escribe un programa que defina la función siguiente y muestre su funcionamiento:

```php
miArraySum(array $array): int|float
```

Esta función devuelve la suma de todos los valores de una matriz. Deberás probar la función tanto con una matriz de enteros como con una matriz de decimales.

La matriz de números enteros puede tener de 3 a 7 valores y los valores pueden estar entre 1 y 10. Para ello, puedes utilizar la función `generaMatrizEnterosRand(int $n, int $min, int $max): array` del ejercicio 4.

La matriz de números decimales puede tener de 3 a 7 valores y los valores pueden estar entre 1 y 10 (con un número decimal que puede ser 0). Para ello, crea la función `generaMatrizDecimalRand(int $n, int $min, int $max): array`, similar a la anterior pero que rellene la matriz con números decimales (con un decimal).

Para obtener un número decimal con un decimal, basta con dividir un número entero por 10.

# 2. Formularios

## Ejercicio 6

Crea en una página un formulario que solicite el nombre de una persona y su edad. Luego ha de mostrar en otra página un mensaje indicando si la persona es mayor de edad o no.

Reutiliza la función `esMayorDeEdad(int $edad): bool` del ejercicio 1. 

Además, en la segunda página hay que informar de los errores cometidos:

- Se mostrará un aviso si no se escribe alguno de los dos campos (nombre o edad).
- Se mostrará un aviso si la edad se deja vacía, si no se escribe un número, si no se escribe un número entero positivo o si se escribe un número que no esté comprendido entre 5 y 130.

## Ejercicio 7

Crea en una página un formulario que solicite un número de filas y un número de columnas. En otra página se creará una tabla HTML que tenga tantas filas como indique el primer número y tantas columnas como indique el segundo número.

El contenido de cada celda será un número que empezará por 1 en la primera celda y se irá incrementando en uno en las celdas siguientes.

Reutiliza la función `creaTabla(int $filas, int $cols): string` del ejercicio 2. 

Además, en la segunda página hay que informar de los errores cometidos:

- Se mostrará un aviso si no se escribe alguno de los dos campos (filas o columnas).
- Tanto las filas como las columnas deben ser valores mayores o iguales a 1 y menores o iguales a 10.

## Ejercicio 8

Crea una página con un formulario que pida el número de DNI. En otra página deberás procesar ese número y calcular su letra.

Para ello, puedes reutilizar la función `calculaLetraNIF(int $num): string` del ejercicio 3. 

Además, en la segunda página hay que informar de los errores cometidos:

- Se mostrará un aviso si no se escribe ningún número.
- Se mostrará un aviso si no se escribe un número, si no se escribe un número entero positivo o si el número no está comprendido entre 1 y 99999999.

## Ejercicio 9

Crea una página con un formulario con los siguientes datos:

- Dirección de correo electrónico (usar la función `filter_var()` para validarla).
- Confirmación de la dirección de correo electrónico (no es necesario validar; simplemente comprobar si coincide con la primera dirección).
- Indicar si se quiere recibir correos. Para ello puedes utilizar un `select` con un valor nulo por defecto (`-`), opción Sí y opción No.

En otra página, genera los avisos correspondientes si alguno de los campos no tiene valor o el valor no es correcto.

## Ejercicio 10

Crea una página con un formulario con los siguientes datos:

- **Nombre y apellidos:** cada uno en un `input` de tipo texto.
- **Edad:** en un `select` con 4 posibles rangos de edad para elegir (por ejemplo, Menos de 20 años, Entre 20 y 39, Entre 40 y 59, 60 o más).
- **Peso:** `input` de tipo numérico.
- **Sexo:** `input` de tipo `radio` con las opciones que consideres.
- **Estado civil:** `input` de tipo `radio` con las opciones que consideres.
- **Aficiones:** `input` de tipo `checkbox` con las opciones que consideres.

En otra página, genera los avisos correspondientes si alguno de los campos no tiene valor o el valor no es correcto.
