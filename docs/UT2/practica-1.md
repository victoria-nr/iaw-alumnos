# Práctica 1 · Formulario de presupuesto de alojamiento web

## 1. Qué vas a construir

Vas a desarrollar una miniaplicación PHP que muestre un formulario, reciba los datos enviados por `POST`, los valide en el servidor y genere una respuesta dinámica con un presupuesto orientativo de alojamiento web.

La práctica sirve para trabajar lo que hemos visto hasta ahora:

- formularios HTML;
- envío de datos mediante `POST`;
- lectura de `$_POST`;
- variables;
- condicionales `if`, `elseif` y `else`;
- una función sencilla;
- un array y un `foreach`;
- generación de HTML usando PHP.

**No se busca una aplicación avanzada.** Se valorará especialmente que el código sea sencillo, ordenado y que seas capaz de explicarlo.

---

## 2. Qué demuestra esta práctica

Con esta práctica debes demostrar que sabes:

- relacionar HTML y PHP en una misma aplicación;
- procesar formularios en servidor;
- usar estructuras de control;
- definir y utilizar funciones;
- validar datos de entrada;
- generar una salida dinámica comprensible.

### Criterios del RA5 trabajados

- **CE2**. Relación entre lenguaje de servidor y lenguaje de marcas.
- **CE3**. Sintaxis básica del lenguaje.
- **CE4**. Estructuras de control.
- **CE5**. Definición y uso de funciones.
- **CE6**. Uso de formularios para introducir información.

---

## 3. Contexto funcional

Una pequeña empresa quiere una página sencilla para que un posible cliente pida un presupuesto inicial de alojamiento web.

La página mostrará un formulario y el usuario debe indicar:

- nombre de contacto;
- correo electrónico;
- tipo de plan;
- meses de contratación;
- si quiere copia de seguridad avanzada (extra);
- si quiere soporte prioritario (extra).

Cuando pulse el botón **Calcular presupuesto**, PHP deberá:

1. recoger los datos del formulario;
2. comprobar que son correctos;
3. mostrar los errores si los hay;
4. si todo es correcto, calcular el precio;
5. mostrar el presupuesto final.

La aplicación no contrata nada ni guarda todavía los datos en base de datos. 

A continuación se muestran los planes y extras, acompañado de un ejemplo:

Planes:

| Plan | Precio mensual |
|---|---:|
| Básico | 5 € |
| Profesional | 9 € |
| Empresa | 15 € |

Extras:

| Extra | Precio mensual |
|---|---:|
| Copia de seguridad avanzada | +2 € |
| Soporte prioritario | +3 € |

Ejemplo:

- Plan Profesional: 9 €/mes
- Copia de seguridad: +2 €/mes
- Soporte prioritario: +3 €/mes
- Total mensual: 14 €/mes
- Para 6 meses: **84 €**


---

## 4. Requisitos obligatorios

Tu aplicación debe:

1. usar un formulario con `method="post"`;
2. procesar el formulario con PHP;
3. comprobar que la petición se ha enviado por `POST`;
4. validar como mínimo:
   1.  que el nombre no esté vacío;
   2.  que el correo no esté vacío y tenga un formato válido;
   3.  que se haya elegido un plan correcto;
   4.  que los meses sean un número entero entre 1 y 24;
  
5. mostrar mensajes de error claros;
6. conservar los valores introducidos si existe algún error;
7. calcular:
   1. precio del plan;
   2. precio de los extras;
   3. total mensual;
   4. total final;
  
8.  utilizar al menos:
    1.  un `if` / `elseif` / `else`;
    2.  un array para guardar errores;
    3.  un `foreach` para mostrar esos errores;
    4.  **una función propia sencilla**.

---

## 5. Estructura recomendada

Para esta práctica puedes hacerlo todo en un único archivo:

```text
practica-1/
└── index.php
```

En esta primera práctica es preferible que el código sea fácil de seguir antes que dividirlo en muchos archivos.

Dentro del repositorio privado del módulo, esta práctica debe quedar en `unidades/UT2/practica-1/`.


---

## 6. Orden recomendado para programarla

No intentes hacer todo de golpe.

### Paso 1. Crea el formulario HTML

Empieza únicamente con el formulario.

Ejemplo de comienzo:

```html
<form action="index.php" method="post">
    ...
</form>
```

Comprueba que tienes correctamente los atributos `name` de cada campo.

### Paso 2. Comprueba si se ha enviado

Antes de leer `$_POST`, comprueba el método de la petición.

Pista:

```php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Aquí procesaremos el formulario
}
```

### Paso 3. Recoge los datos

Guarda cada dato en una variable.

Por ejemplo:

```php
$nombre = trim($_POST["nombre"]);
```

En los `checkbox`, recuerda que el campo puede no existir en `$_POST` cuando no está marcado.

Pista:

```php
$backup = isset($_POST["backup"]);
```

### Paso 4. Valida los datos

Crea un array vacío:

```php
$errores = [];
```

Cada vez que encuentres un problema, añade un mensaje:

```php
if ($nombre == "") {
    $errores[] = "Debes escribir un nombre.";
}
```

Puedes validar el correo con:

```php
filter_var($correo, FILTER_VALIDATE_EMAIL)
```

### Paso 5. Muestra los errores

Si existen errores, muéstralos mediante un `foreach`.

No es necesario crear una función para hacerlo.

### Paso 6. Crea una función sencilla

Crea **una única función** que reciba el plan y devuelva su precio mensual.

Por ejemplo, su cabecera podría ser:

```php
function obtenerPrecioPlan($plan)
{
    // ...
}
```

Dentro puedes utilizar `if`, `elseif` y `else`.

### Paso 7. Calcula el presupuesto

Solo debes calcularlo cuando el array de errores esté vacío.

Pista:

```php
if (count($errores) == 0) {
    // calcular presupuesto
}
```

Una posible secuencia es:

```text
precio del plan
+ precio de extras
= total mensual

 total mensual × meses
= total final
```

### Paso 8. Conserva los valores del formulario

Si hay un error, el usuario no debería tener que rellenarlo todo otra vez.

En un campo de texto puedes volver a mostrar su valor mediante PHP.

En los `select` y `checkbox` puedes usar pequeños `if` para escribir `selected` o `checked` cuando corresponda.

---

## 7. Resultado esperado

### Si hay errores

La página debe volver a mostrar el formulario e indicar claramente qué hay que corregir.

Ejemplo:

```text
Hay errores en el formulario:
- Debes escribir un nombre.
- El correo electrónico no es válido.
```

### Si todo es correcto

Debe aparecer un resumen similar a este:

```text
Plan: Profesional
Meses: 6

Copia de seguridad: +2 €/mes
Soporte prioritario: +3 €/mes

Precio del plan: 9 €/mes
Precio de extras: 5 €/mes
Total mensual: 14 €/mes
Total final: 84 €
```

---

## 8. Qué NO necesitas hacer

Para esta práctica **no necesitas**:

- clases;
- programación orientada a objetos;
- bases de datos;
- sesiones;
- separar la aplicación en muchos archivos;
- crear funciones para cada pequeña operación;
- utilizar `declare(strict_types=1)`;
- usar tipos en los parámetros o valores devueltos de las funciones;
- crear una función que genere todo el formulario HTML.

Si sabes hacerlo, puedes utilizar alguna de estas técnicas, pero **no aportarán más nota** por sí mismas. Al contrario, se valorará la sencillez y que el código sea lo más didáctico posible.

---

## 9. Entrega

Debes entregar esta práctica dentro de tu repositorio privado del módulo, en la ruta `unidades/UT2/practica-1/`.

Debes entregar:

- `index.php`;
- un `README.md` breve indicando cómo ejecutar la práctica;
- una captura del formulario;
- una captura de un resultado correcto;
- una captura mostrando errores de validación.



## 10. Ampliaciones opcionales

Si acabas antes, puedes añadir alguna mejora:

- descuento por contratación anual;
- mensaje distinto según el plan;
- desglose más detallado del cálculo;
- CSS básico;
- validación más estricta del correo.

---

## 11. Validación de autoría y comprensión

Después de entregar la práctica se te puede pedir que expliques brevemente tu código y hagas una modificación pequeña.

Por ejemplo:

- cambiar el precio de un plan;
- añadir un plan nuevo;
- cambiar el precio de un extra;
- exigir un mínimo de 3 meses;
- mostrar un mensaje si el total supera 100 €.

El objetivo no es memorizar el código: es demostrar que entiendes lo que has programado.


## 12. Cómo se evaluará esta práctica

El profesor valorará dos cosas:

1. **el producto entregado y su funcionamiento**, según las indicaciones de esta práctica.
2. **una validación breve de autoría y comprensión**, que podrá hacerse en clase o por videollamada.


---

## 13. Checklist del alumno antes de entregar


- [ ] El formulario utiliza `POST`.
- [ ] Compruebo `$_SERVER["REQUEST_METHOD"]`.
- [ ] Recojo los datos de `$_POST`.
- [ ] Compruebo los `checkbox` con `isset()`.
- [ ] Tengo un array `$errores`.
- [ ] Valido nombre, correo, plan y meses.
- [ ] Muestro los errores con `foreach`.
- [ ] Tengo una única función sencilla para obtener el precio del plan.
- [ ] Solo calculo el presupuesto si no hay errores.
- [ ] Si hay errores, se conservan los valores escritos.
- [ ] Puedo explicar cada parte de mi código.
