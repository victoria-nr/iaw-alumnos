# Guía de comandos · PHP en la UT2

Esta guía recoge los comandos mínimos que conviene tener a mano durante la unidad.  
No pretende sustituir a los apuntes: sirve como chuleta rápida para trabajar con el entorno de la UT1 y depurar problemas habituales.

---

## 1. Comprobar que PHP está disponible

```bash
php -v
```

### Qué hace
Muestra la versión de PHP instalada o disponible en el contenedor/entorno.

### Para qué sirve en esta UT
Permite verificar que el entorno realmente puede ejecutar scripts PHP.

### Qué debes observar
- que el comando responde;
- que no aparece “command not found”;
- que estás usando el PHP del entorno previsto.

---

## 2. Validar sintaxis de un archivo PHP

```bash
php -l archivo.php
```

Ejemplo:

```bash
php -l index.php
```

### Qué hace
Comprueba la sintaxis del archivo sin ejecutarlo.

### Cuándo usarlo
Cuando un script falla y sospechas de:
- llaves sin cerrar;
- paréntesis mal puestos;
- `;` olvidados;
- comillas desparejadas.

---

## 3. Levantar el entorno de la UT1 con contenedores

Si en la UT1 se dejó preparado un `docker-compose.yml` o un `compose.yml`, lo habitual será:

```bash
docker compose up -d
```

Para detenerlo:

```bash
docker compose down
```

Para reconstruir si ha habido cambios importantes:

```bash
docker compose up -d --build
```

### Para qué sirve en esta UT
Permite ejecutar PHP dentro de un entorno reproducible y estable, especialmente útil si el alumnado no tiene PHP instalado de forma nativa.

---

## 4. Ver logs del contenedor

```bash
docker compose logs
```

Para seguirlos en tiempo real:

```bash
docker compose logs -f
```

Para un servicio concreto, por ejemplo `web`:

```bash
docker compose logs -f web
```

### Qué problemas ayuda a detectar
- error al arrancar el contenedor;
- puerto ocupado;
- fallo de configuración;
- script que genera errores visibles en el log.

---

## 5. Entrar en un contenedor para revisar archivos

```bash
docker compose exec web sh
```

o, si dispone de bash:

```bash
docker compose exec web bash
```

### Para qué sirve
- inspeccionar rutas;
- comprobar que el código está donde debe;
- lanzar `php -l`;
- revisar permisos;
- localizar logs.

---

## 6. Revisar errores de PHP en pantalla durante desarrollo

En un entorno de desarrollo, puede ser útil activar la visualización de errores al principio del script:

```php
<?php
declare(strict_types=1);

error_reporting(E_ALL);
ini_set('display_errors', '1');
```

### Importante
Esto está bien **solo en desarrollo**.  
En producción, los errores no deben mostrarse al usuario final.

---

## 7. Localizar errores de cabeceras

Si aparece algo parecido a:

```text
Warning: Cannot modify header information - headers already sent...
```

### Significado habitual
Has intentado usar:
- `header()`,
- `setcookie()`,
- o iniciar/redirigir una sesión

**después** de haber enviado salida al navegador.

### Qué revisar
- espacios o líneas antes de `<?php`;
- `echo` prematuros;
- HTML antes de `session_start()` o `setcookie()`.

---

## 8. Probar rápidamente una redirección

```php
<?php
header('Location: panel.php');
exit;
```

### Recomendación
Después de `header('Location: ...')`, utiliza siempre `exit;`.

### Por qué
Evita que el script siga ejecutando código innecesario.

---

## 9. Comprobar qué llega por GET o POST

Durante las primeras pruebas, es útil inspeccionar el contenido recibido:

```php
<?php
echo '<pre>';
var_dump($_GET);
echo '</pre>';
```

o:

```php
<?php
echo '<pre>';
print_r($_POST);
echo '</pre>';
```

### Cuándo usarlo
- cuando un formulario “no llega”;
- cuando el nombre de los campos no coincide;
- cuando dudas de qué estructura estás recibiendo.

---

## 10. Comprobar sesiones

Inicio básico:

```php
<?php
session_start();
var_dump($_SESSION);
```

### Qué permite ver
- si la sesión se está creando;
- si realmente se guardan datos;
- si los valores esperados existen.

---

## 11. Borrar una sesión correctamente

```php
<?php
session_start();
$_SESSION = [];
session_destroy();
header('Location: login.php');
exit;
```

### Cuándo usarlo
En el cierre de sesión (`logout`).

---

## 12. Generar un hash de contraseña rápido para pruebas

En consola:

```bash
php -r "echo password_hash('ClaveSegura123', PASSWORD_DEFAULT) . PHP_EOL;"
```

### Para qué sirve
Crear un hash real para incluirlo en una práctica sin guardar la contraseña en texto plano.

---

## 13. Comprobar puertos escuchando

En algunos sistemas:

```bash
lsof -i :8000
```

o:

```bash
ss -ltnp
```

### Cuándo tiene sentido
Cuando el entorno con contenedores no arranca porque el puerto configurado ya está en uso.

---

## 14. Qué revisar cuando “la página sale en blanco”

Una página en blanco suele significar una de estas cosas:

1. hay un error de PHP y no se está mostrando;
2. el archivo no se está ejecutando donde crees;
3. has redirigido a otra ruta inexistente;
4. hay un `exit;` o `die;` antes de tiempo.

### Checklist rápido
- ¿has activado errores en desarrollo?
- ¿has mirado logs?
- ¿el archivo termina en `.php` y se está sirviendo como PHP?
- ¿la ruta del formulario `action` es correcta?
- ¿el servidor está leyendo la carpeta correcta?

---

## 15. Flujo mínimo recomendado de trabajo

```bash
# 1. Entrar en la carpeta del proyecto
cd ruta/del/proyecto

# 2. Levantar el entorno reproducible
docker compose up -d

# 3. Validar archivos clave desde el contenedor
docker compose exec web php -l index.php
docker compose exec web php -l login.php
docker compose exec web php -l panel.php

# 4. Si falla algo, revisar logs
docker compose logs -f
```

---

## 16. Recomendaciones de depuración en esta UT

Orden recomendado de comprobación:

1. **Sintaxis**  
   Usa `php -l`.

2. **Llegada de datos**  
   Inspecciona `$_GET`, `$_POST` o `$_SESSION`.

3. **Flujo del programa**  
   Introduce mensajes de prueba muy controlados o `var_dump()` puntuales.

4. **Cabeceras y sesión**  
   Revisa si estás llamando a `session_start()`, `setcookie()` o `header()` demasiado tarde.

5. **Logs**  
   Si algo sigue sin cuadrar, revisa el log del servidor o del contenedor.

---

## 17. Recordatorio final

Esta UT no va de memorizar comandos.  
Va de saber usar los **mínimos comandos útiles** para comprobar que:

- el entorno funciona;
- el script tiene buena sintaxis;
- el formulario envía lo que debe;
- la sesión realmente guarda datos;
- los errores se entienden y se corrigen.
