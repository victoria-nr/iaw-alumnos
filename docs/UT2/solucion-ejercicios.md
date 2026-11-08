# Solución de los mini ejercicios · UT2 · Programación web en servidor con PHP

Este documento recoge las soluciones propuestas para los ejercicios breves de `apuntes.md`.

> **Nota didáctica:** en programación suele haber varias soluciones correctas. Las que aparecen aquí no son las únicas posibles, pero sí son claras, válidas y coherentes con el enfoque de la unidad.

---

## Mini ejercicio 1

### 1. ¿Qué significa que un lenguaje sea “de servidor”?
Significa que el código se ejecuta en el servidor web, no en el navegador del usuario, y que el cliente recibe solo el resultado generado.

### 2. Nombra tres lenguajes de servidor distintos de PHP
- Python
- JavaScript en servidor con Node.js
- Java

### 3. ¿Por qué tiene sentido empezar con PHP en esta unidad?
Porque PHP se integra muy bien con HTML, permite hacer ejemplos web funcionales muy rápido y ayuda a entender con claridad el modelo petición-respuesta.

---

## Mini ejercicio 2

Imagina que un formulario pide nombre y correo.

### 1. ¿Quién envía la petición?
La envía el navegador del usuario cuando este rellena el formulario y pulsa el botón de enviar.

### 2. ¿Quién procesa los datos?
Los procesa el servidor, ejecutando el código PHP que recibe la petición.

### 3. ¿Quién muestra la página final?
La página final la muestra el navegador, pero lo hace a partir del HTML que le devuelve el servidor.

---

## Mini ejercicio 3

Crea un archivo `hola.php` que muestre:
- un título con tu nombre,
- un párrafo diciendo que la página se genera en servidor,
- y la fecha del día usando PHP.

### Solución propuesta

```php
<?php
$nombre = 'Victoria';
$fechaHoy = date('d/m/Y');
?>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Hola desde PHP</title>
</head>
<body>
    <h1>Hola, soy <?php echo $nombre ?></h1>
    <p>Esta página se genera en el servidor con PHP.</p>
    <p>Fecha de hoy: <?php echo $fechaHoy ?></p>
</body>
</html>
```

---

## Mini ejercicio 4

Crea un array asociativo con datos de un servicio web:
- nombre,
- precio mensual,
- si incluye dominio,
- si incluye soporte.

Después muestra esos datos dentro de una lista HTML.

### Solución propuesta

```php
<?php
$servicio = [
    'nombre' => 'Hosting Profesional',
    'precio_mensual' => 9,
    'incluye_dominio' => true,
    'incluye_soporte' => true,
];
?>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Servicio web</title>
</head>
<body>
    <h1>Ficha del servicio</h1>
    <ul>
        <li>Nombre: <?php echo $servicio['nombre'] ?></li>
        <li>Precio mensual: <?php echo $servicio['precio_mensual'] ?> €</li>
        <li>Incluye dominio: <?php echo $servicio['incluye_dominio'] ?></li>
        <li>Incluye soporte: <?php echo $servicio['incluye_soporte'] ?></li>
    </ul>
</body>
</html>
```

---

## Mini ejercicio 5

Crea una variable `$espacioLibreGb` con el espacio libre de un servidor y muestra un mensaje según el espacio disponible.

### Solución propuesta

```php
<?php
$espacioLibreGb = 12;

if ($espacioLibreGb < 5) {
    echo 'Espacio crítico';
} elseif ($espacioLibreGb <= 20) {
    echo 'Espacio limitado';
} else {
    echo 'Espacio suficiente';
}
```

---

## Mini ejercicio 6

Muestra si una aplicación está en mantenimiento según el valor booleano de `$mantenimientoActivo`.

### Solución propuesta

```php
<?php
$mantenimientoActivo = true;

if ($mantenimientoActivo) {
    echo 'La aplicación está en mantenimiento';
} else {
    echo 'La aplicación está disponible';
}
```

> Para probar el otro caso, cambia el valor de `$mantenimientoActivo` a `false`.

---

## Mini ejercicio 7

Muestra un mensaje adecuado para un código HTTP usando `switch`.

### Solución propuesta

```php
<?php
$estadoHttp = 404;

switch ($estadoHttp) {
    case 200:
        echo 'La petición se ha procesado correctamente.';
        break;
    case 404:
        echo 'No se ha encontrado el recurso solicitado.';
        break;
    case 500:
        echo 'El servidor ha tenido un error interno.';
        break;
    default:
        echo 'Código de estado no previsto.';
}
```

---

## Mini ejercicio 8

Muestra qué hace el sistema con un servicio web según una acción de administración.

### Solución propuesta

```php
<?php
$accion = 'reiniciar';

switch ($accion) {
    case 'reiniciar':
        echo 'El servicio web se reiniciará.';
        break;
    case 'detener':
        echo 'El servicio web se detendrá.';
        break;
    case 'estado':
        echo 'Se comprobará el estado del servicio web.';
        break;
    default:
        echo 'La acción indicada no es válida.';
}
```

---

## Mini ejercicio 9

Muestra cinco nombres de copias de seguridad con un bucle `for`.

### Solución propuesta

```php
<?php
echo '<ul>';

for ($numero = 1; $numero <= 5; $numero++) {
    echo "<li>backup-$numero.sql</li>";
}

echo '</ul>';
```

---

## Mini ejercicio 10

Muestra tres usuarios de prueba con un bucle `for`.

### Solución propuesta

```php
<?php
for ($numero = 1; $numero <= 3; $numero++) {
    echo "<p>usuario$numero</p>";
}
```

---

## Mini ejercicio 11

Simula tres intentos de conexión a una base de datos con `while`.

### Solución propuesta

```php
<?php
$intento = 1;

while ($intento <= 3) {
    echo "<p>Intento de conexión $intento</p>";
    $intento++;
}
```

---

## Mini ejercicio 12

Muestra el espacio disponible después de cada copia de seguridad hasta que queden 20 GB o menos.

### Solución propuesta

```php
<?php
$espacioLibreGb = 100;

while ($espacioLibreGb > 20) {
    $espacioLibreGb -= 20;
    echo "<p>Espacio disponible: $espacioLibreGb GB</p>";
}
```

---

## Mini ejercicio 13

Crea un array con tres mensajes de error y muéstralos dentro de una lista HTML usando `foreach`.

### Solución propuesta

```php
<?php
$errores = [
    'El nombre es obligatorio.',
    'El correo no es válido.',
    'Debes seleccionar un plan.',
];
?>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Errores del formulario</title>
</head>
<body>
    <h1>Errores detectados</h1>
    <ul>
        <?php 
            foreach ($errores as $error){
                echo "<li>$error</li>";
            }
        ?>
    </ul>
</body>
</html>
```

---

## Mini ejercicio 14

Crea un array asociativo con la configuración de una aplicación web y muestra cada clave y su valor con `foreach`.

### Solución propuesta

```php
<?php
$configuracion = [
    'entorno' => 'producción',
    'depuracion' => false,
    'puerto' => 8080,
];

foreach ($configuracion as $clave => $valor) {
    if( is_bool($valor)){
        $valor = $valor ? "Si" : "No";
    }
    echo "<p>$clave: $valor</p>";
}
```

---

## Mini ejercicio 15

Escribe una función llamada `obtenerMensajePlan()` que reciba el nombre de un plan y devuelva un texto distinto para:
- Básico,
- Profesional,
- Empresa.

### Solución propuesta

```php
<?php
function obtenerMensajePlan(string $plan): string
{
    switch ($plan) {
        case 'Básico':
            return 'El plan Básico es adecuado para proyectos sencillos.';
        case 'Profesional':
            return 'El plan Profesional ofrece más recursos y mejor soporte.';
        case 'Empresa':
            return 'El plan Empresa está pensado para proyectos con mayores necesidades.';
        default:
            return 'El plan indicado no existe.';
    }
}

echo obtenerMensajePlan('Profesional');
```

---

## Mini ejercicio 16

Amplía el ejemplo anterior con un nuevo campo `meses` y valida que sea un número entre 1 y 24.

### Solución propuesta


```php
<?php
$errores = [];
$nombre = '';
$correo = '';
$plan = '';
$meses = '';

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $nombre = trim($_POST['nombre'] ?? '');
    $correo = trim($_POST['correo'] ?? '');
    $plan = $_POST['plan'] ?? '';
    $meses = trim($_POST['meses'] ?? '');

    if ($nombre === '') {
        $errores[] = 'Debes indicar el nombre.';
    }

    if (!filter_var($correo, FILTER_VALIDATE_EMAIL)) {
        $errores[] = 'Debes indicar un correo válido.';
    }

    if (!in_array($plan, ['Básico', 'Profesional', 'Empresa'], true)) {
        $errores[] = 'Debes elegir un plan válido.';
    }
    if ($meses === '' || !ctype_digit($meses)) {
        $errores[] = 'Debes indicar un número de meses válido.';
    } elseif ((int) $meses < 1 || (int) $meses > 24) {
        $errores[] = 'El número de meses debe estar entre 1 y 24.';
    }
}
?>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Formulario PHP con meses</title>
</head>
<body>
    <h1>Solicitud de plan</h1>

    <?php 
    if (!empty($errores)) { 
        echo '<ul>';
        foreach ($errores as $error) {
            echo '<li>' . $error . '</li>';
        }
        echo '</ul>';
    } 
    ?>

    <form method="post">
        <label>
            Nombre
            <input type="text" name="nombre" value="<?php echo htmlspecialchars($nombre); ?>">
        </label>
        <br>
        <label>
            Correo
            <input type="email" name="correo" value="<?php echo htmlspecialchars($correo); ?>">
        </label>
        <br>
        <label>
            Plan
            <select name="plan">
                <option value="">-- Selecciona --</option>
                <option value="Básico" <?php if ($plan === 'Básico') { echo 'selected'; } ?>>Básico</option>
                <option value="Profesional" <?php if ($plan === 'Profesional') { echo 'selected'; } ?>>Profesional</option>
                <option value="Empresa" <?php if ($plan === 'Empresa') { echo 'selected'; } ?>>Empresa</option>
            </select>
        </label>
        <br>
        <label>
            Meses
            <input type="number" name="meses" min="1" max="24" value="<?= htmlspecialchars($meses) ?>">
        </label>
        <br>        
        <button type="submit">Enviar</button>
    </form>

    <?php 
    if ($_SERVER['REQUEST_METHOD'] === 'POST' && empty($errores)) { 
        echo '<h2>Resumen</h2>';
        echo '<p>Nombre: ' . htmlspecialchars($nombre) . '</p>';
        echo '<p>Correo: ' . htmlspecialchars($correo) . '</p>';
        echo '<p>Plan: ' . htmlspecialchars($plan) . '</p>';
        echo '<p>Meses: ' . htmlspecialchars($meses) . '</p>';
    } 
    ?>
</body>
</html>
```

---

## Mini ejercicio 17

1. En la primera visita, `$_SESSION['contador']` todavía no existe. Se inicializa a `0` y, justo después, se incrementa a `1`, por lo que aparece:

    ```text
    Has entrado en esta página 1 veces.
    ```

    Cada pulsación del enlace **Nueva visita** genera otra petición y recupera la misma sesión. Tras seguir el enlace tres veces, el contador mostrará sucesivamente `2`, `3` y `4`. Por tanto, al final aparecerá `4`.

2. Otra pestaña del mismo navegador normalmente continúa el contador, porque comparte las cookies de sesión con la primera pestaña. Al abrir `contador.php` desde esa pestaña, PHP recupera el mismo `$_SESSION['contador']` y vuelve a incrementarlo.

3. Otro navegador, una ventana de incógnito o un perfil distinto suelen crear un contexto de navegación independiente. Al no enviar la misma cookie de sesión, el servidor crea o recupera otra sesión y el contador empieza en `1` para ese contexto.

4. Al pulsar **Reiniciar contador**, la petición `POST` contiene `reiniciar`, por lo que el código asigna primero `0` a `$_SESSION['contador']`. Después se ejecuta igualmente esta línea:

    ```php
    $_SESSION['contador']++;
    ```

    Por eso el valor final de esa misma petición es `1`, no `0`.

5. Si se sustituyera la inicialización condicional:

    ```php
    if (!isset($_SESSION['contador'])) {
         $_SESSION['contador'] = 0;
    }
    ```

    por una asignación directa en todas las peticiones:

    ```php
    $_SESSION['contador'] = 0;
    ```

    el valor recuperado de la sesión se borraría antes de incrementarlo. En cada visita pasaría de `0` a `1`, por lo que el contador dejaría de acumular visitas. La condición `!isset(...)` es la que permite inicializar solo la primera vez y conservar el estado en las peticiones posteriores.

---

## Ejercicios guiados: comprender las sesiones

### 1. Sin sesión

El formulario inicializa `$texto` con una cadena vacía. El procesamiento obtiene el texto de `$_POST`, enviado por el formulario. Al seguir el enlace a `procesar.php`, la nueva petición es GET y no contiene ese POST: vuelve a mostrarse que no se ha recibido texto.

Al volver al formulario, su variable vuelve a inicializarse. El nombre común `$texto` no conecta las dos ejecuciones. `?? ''` aporta una cadena vacía cuando no existe el dato o es nulo.

### 2. Con sesión

`session_start()` inicia o recupera la sesión. La asignación a `$_SESSION['textoSesion']` conserva el texto entre peticiones. El servidor lo recupera en otra petición del mismo contexto de navegación, aunque esa nueva petición no incluya el texto.

Un segundo texto sustituye al primero porque se asigna a la misma clave. Un envío vacío produce un aviso y no modifica el anterior.

Otra pestaña del mismo contexto comparte normalmente la cookie identificadora de sesión. Un navegador o contexto independiente empieza sin esos datos. La sesión no se crea por fichero ni por pestaña.

No presentar dos ventanas privadas del mismo navegador como dos sesiones independientes: pueden compartir las cookies privadas mientras esas ventanas permanezcan abiertas.

### 3. Contador

En una sesión nueva se muestra 1. Después de tres visitas por enlace se muestra 4; abrir otra pestaña del mismo contexto suma una visita más. El valor exacto cambia si se realizan peticiones adicionales.

Reiniciar asigna 0 y, después, la misma petición ejecuta el incremento: se muestra 1. Al seguir el enlace posterior se muestra 2.

Si se asigna 0 en cada petición sin comprobar `isset()`, siempre se muestra 1. La condición permite inicializar solo cuando el dato aún no existe.

### 4. Validación

Suponiendo que se sigue el orden indicado:

| Después de… | Valor del campo | Error visible | Última palabra válida |
| --- | --- | --- | --- |
| Enviar HOLA | HOLA | No | HOLA |
| Enviar hola | hola | Sí | HOLA |
| Enviar vacío | Vacío | Sí | HOLA |
| Enviar ADIOS | ADIOS | No | ADIOS |
| Seguir el enlace sin enviar | Vacío | No | ADIOS |

La asignación a la sesión solo se hace en la rama válida. Si se asignara antes de validar, un intento incorrecto sustituiría al último dato válido.

El error y el contenido del campo pertenecen a la petición actual: no hay redirección ni otra página que necesite recuperarlos. Guardarlos en sesión añadiría estado y obligaría a decidir cuándo limpiarlo. La palabra válida sí debe persistir y por eso se guarda.

Se mantiene `ctype_upper()` para no introducir otra técnica de validación. No tratarla como una comprobación Unicode general: las pruebas usan A-Z.

### 5. Cerrar sesión

El usuario pasa de invitado a Ana. Sigue apareciendo tras una petición GET porque se recupera de sesión.

`$_SESSION = [];` vacía los datos accesibles en la petición actual. `session_destroy();` destruye los datos de la sesión del servidor. Este ejemplo no elimina explícitamente la cookie identificadora del navegador; la comprobación didáctica consiste en verificar que los datos anteriores ya no se recuperan. Al volver a una página que ejecuta `session_start()`, PHP puede iniciar de nuevo una sesión sin los datos anteriores.

El usuario vuelve a invitado, el texto desaparece, la palabra válida desaparece y el contador vuelve a 1 en su siguiente visita.

Los cinco ejercicios se ejecutan bajo el mismo servidor y configuración habitual de sesión, sin nombres de sesión separados. Sus claves son distintas, pero pertenecen a la misma sesión. Vaciarla afecta a todas esas claves, aunque los archivos estén en carpetas distintas.

La ampliación con `unset($_SESSION['usuario']);` elimina solo el nombre. El resto de las claves se conserva.

## Preguntas finales: ideas que deben aparecer

1. Mostrar un dato inmediatamente tras un POST no demuestra persistencia: podría mostrarse directamente desde POST.
2. Seguir un enlace GET que no transporte el dato permite comprobar si se recupera de sesión.
3. Cada petición ejecuta el PHP de nuevo, también cuando apunta al mismo fichero.
4. El campo pertenece al formulario; una variable normal pertenece a la ejecución actual; un dato de sesión puede recuperarse en otras peticiones.
5. No todos los errores requieren sesión. En el ejercicio 4 se muestran en la misma respuesta que procesa el formulario.

---


## Mini ejercicio 18

Diseña una mini zona privada que guarde en sesión un contador de accesos y el nombre del usuario autenticado.

### Solución propuesta

```php
<?php
session_start();

if (!isset($_SESSION['usuario'])) {
    $_SESSION['usuario'] = 'ana';
    $_SESSION['nombre'] = 'Ana';
    $_SESSION['contador'] = 0;
}

$_SESSION['contador']++;
?>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Zona privada</title>
</head>
<body>
    <h1>Zona privada</h1>
    <p>Usuario autenticado: <?= htmlspecialchars($_SESSION['nombre']) ?></p>
    <p>Número de accesos al panel: <?= $_SESSION['contador'] ?></p>
</body>
</html>
```

> En una aplicación más completa, el usuario no se fijaría manualmente, sino a partir de un login previo.

---

## Mini ejercicio 19

Busca y corrige al menos dos errores en este fragmento:

```php
<?php
if ($_SERVER['REQUEST_METHOD'] = 'POST') {
    $nombre = $_POST['nombre'];
    echo 'Hola ' . $nombre
    header('Location: final.php');
}
```

### Errores principales
1. Se usa `=` en lugar de `===` al comparar el método HTTP.
2. Falta el punto y coma al final de `echo 'Hola ' . $nombre`.
3. Se intenta hacer un `header()` después de haber enviado salida con `echo`.
4. Se lee `$_POST['nombre']` sin valor por defecto.

### Solución propuesta

```php
<?php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $nombre = trim($_POST['nombre'] ?? '');

    header('Location: final.php?nombre=' . urlencode($nombre));
    exit;
}
```

> Otra posibilidad sería no redirigir y mostrar directamente el saludo, pero entonces habría que eliminar `header()`.

---

## Actividades finales de repaso (solución orientativa)


### Actividad 20
**Explica la diferencia entre una variable normal, una cookie y una sesión.**

- Una **variable normal** solo existe durante la ejecución actual del script.
- Una **cookie** es un dato pequeño que el navegador guarda y reenvía al servidor en peticiones posteriores.
- Una **sesión** permite que el servidor mantenga estado asociado a un usuario entre varias peticiones.

### Actividad 21
**Describe el flujo completo de un login sencillo con tus palabras.**

El usuario abre `login.php`, escribe usuario y contraseña y envía el formulario. El navegador manda una petición `POST` al servidor. PHP comprueba las credenciales. Si son correctas, guarda datos del usuario en `$_SESSION` y redirige al panel. Si no son correctas, vuelve al login con un error.

### Actividad 22
**Indica tres errores típicos que pueden romper una aplicación PHP con formularios.**

- Leer `$_POST` sin comprobar si la clave existe.
- Usar `header()` después de haber enviado HTML o `echo`.
- Confiar solo en la validación del navegador y no validar en servidor.

### Actividad 23
**Crea una tabla de dos columnas donde compares validación en cliente y validación en servidor.**

| Validación en cliente | Validación en servidor |
|---|---|
| Se ejecuta en el navegador | Se ejecuta en el servidor |
| Mejora la experiencia del usuario | Garantiza el control real de los datos |
| Puede saltarse o manipularse | Es obligatoria para seguridad y consistencia |
| Da feedback rápido | Decide si la aplicación acepta o rechaza la petición |

### Actividad 24
**Haz un esquema visual, aunque sea simple, del camino que sigue un formulario desde el navegador hasta la respuesta final.**

```text
Usuario
   ↓
Navegador
   ↓  envía formulario HTTP
Servidor web
   ↓
Script PHP
   ↓  valida y procesa datos
Genera HTML
   ↓
Respuesta HTTP
   ↓
Navegador muestra el resultado
```
