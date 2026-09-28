# Práctica 2 · Entorno web reproducible guiado con `Docker Compose`

## 1. Qué vas a construir

En esta práctica vas a completar el proyecto `ut1-entorno-web` preparado en la práctica 1 dentro de `unidades/UT1/` para convertirlo en un entorno web reproducible con tres servicios coordinados:

- `nginx`
- `php`
- `db`

 Tendrás que:

- interpretar qué necesita cada servicio;
- buscar información técnica cuando te falte una pieza;
- completar los archivos por tu cuenta;
- comprobar si tus decisiones funcionan de verdad.

El resultado final debe permitir abrir una página en el navegador que confirme estas tres ideas:

1. PHP se está ejecutando correctamente.
2. La aplicación puede conectar con MariaDB.
3. La base de datos contiene un registro inicial cargado desde un script SQL.

---

## 2. Qué demuestra esta práctica

Con esta práctica debes demostrar que sabes:

- montar un stack multicontenedor con `Docker Compose`;
- distinguir el papel de `nginx`, `php` y `db`;
- localizar y añadir la pieza necesaria para que PHP pueda acceder a MariaDB;
- completar una configuración a partir de requisitos técnicos;
- revisar logs y usar evidencia técnica para corregir errores;
- levantar, comprobar, parar y volver a levantar el entorno;
- documentar qué has hecho y qué información has necesitado consultar.

### Criterios del RA1 trabajados

- **CE1**. Software necesario para el funcionamiento.  
- **CE2**. Tecnologías empleadas.  
- **CE3**. Instalación y configuración de servidor web y base de datos.  
- **CE4**. Posibilidades de procesamiento en cliente y servidor.  
- **CE5**. Componentes necesarios para el procesamiento en servidor.  
- **CE6**. Configuración del acceso a bases de datos.  
- **CE7**. Seguridad mínima en accesos.  
- **CE8**. Plataformas integradas orientadas a prueba y desarrollo.  
- **CE9**. Documentación de procedimientos.

---

## 3. Punto de partida obligatorio

Debes continuar desde la carpeta `unidades/UT1/ut1-entorno-web` creada en la práctica 1 dentro de tu repositorio privado del módulo. Debes seguir en la misma rama de git, no crees una rama nueva.

La estructura mínima que debes dejar al final es esta:

```text
ut1-entorno-web/
├── .env.example
├── README.md
├── app/
│   └── index.php
├── compose.yaml
├── nginx/
│   └── default.conf
├── php/
│   └── Dockerfile
└── sql/
    └── init.sql
```

No tienes que inventar una estructura alternativa. En esta práctica el reto está en **completar bien** el entorno, no en rediseñarlo todo.

Esta estructura base ya la has implementado en la práctica anterior. La única novedad en esa práctica es el directorio `php` con su archivo `Dockerfile`. Deberás crear ambos en el proyecto.

---

## 4. Restricciones

Debes respetar estas condiciones:

- el servicio web se llamará `nginx`;
- el servicio PHP se llamará `php`;
- el servicio de base de datos se llamará `db`;
- la web deberá responder en `http://localhost:8080`;
- la base de datos del caso se llamará `ut1db`;
- el usuario de la base de datos será `ut1user`;
- la aplicación debe conectarse usando variables de entorno;
- el script SQL debe crear una tabla llamada `prueba` e insertar un mensaje inicial.

---

## 5. Qué se espera de ti

En esta práctica **se espera** que consultes información técnica. No es una señal de debilidad, sino parte del trabajo normal de implantación.

Debes buscar, como mínimo, información sobre:

- qué imagen base te conviene usar para el servicio PHP;
- qué extensión o módulo necesita PHP para conectarse con MariaDB mediante PDO;
- qué directiva de Nginx reenvía la ejecución de archivos PHP al servicio adecuado;
- qué comandos de Docker Compose te sirven para levantar, revisar y parar el stack.

En el `README.md` final tendrás que anotar al menos **dos fuentes consultadas** y explicar en una línea para qué te han servido.

---

## 6. Tareas obligatorias

### Parte 1. Analizar el punto de partida

Antes de escribir nada, revisa tu proyecto y completa esta tabla dentro del `README.md` que ya empezaste en la práctica anterior.

| Elemento | Qué función crees que tendrá |
|---|---|
| `compose.yaml` |  |
| `nginx/default.conf` |  |
| `app/index.php` |  |
| `.env.example` |  |
| `sql/init.sql` |  |
| `php/Dockerfile` |  |

### Parte 2. Completar `compose.yaml`

Debes construir un `compose.yaml` funcional que cumpla estos requisitos:

- define los servicios `nginx`, `php` y `db`;
- publica el puerto `8080` del host hacia el servicio web;
- monta la carpeta `app/` dentro del servicio web y del servicio PHP;
- haz que Nginx use el archivo `nginx/default.conf` del proyecto;
- haz que el servicio PHP reciba por variables de entorno los datos de conexión;
- haz que MariaDB inicialice la base de datos usando `sql/init.sql`;
- usa un volumen para persistir los datos de MariaDB.

No copies un `compose.yaml` completo de esta práctica desde otro documento. Puedes apoyarte en tus apuntes y en documentación, pero debes completarlo tú mismo.

### Parte 3. Investigar y crear `php/Dockerfile`

El servicio PHP debe ser capaz de ejecutar código PHP y de conectar con MariaDB desde PDO.

Tu tarea es:

1. elegir una imagen base adecuada para PHP-FPM;
2. investigar qué extensión necesitas para PDO con MariaDB/MySQL;
3. dejar un `Dockerfile` mínimo que resuelva esa necesidad.

Pista: no basta con poner una imagen oficial de PHP si esa imagen no trae activa la extensión que necesitas.

### Parte 4. Completar `nginx/default.conf`

Debes dejar una configuración funcional de Nginx que cumpla esto:

- atiende por el puerto 80 dentro del contenedor;
- usa `/var/www/html` como raíz del proyecto;
- sirve `index.php` como documento principal;
- intenta servir recursos estáticos cuando existan;
- reenvía los archivos `.php` al servicio `php`.

Puedes partir de este esqueleto y completarlo:

```nginx
server {
    listen ____;
    server_name ____;

    root ____;
    index ____;

    location / {
        try_files ____ ____ ____;
    }

    location ~ \.php$ {
        include ____;
        fastcgi_pass ____;
        fastcgi_param ____;
    }
}
```

### Parte 5. Completar `sql/init.sql`

Debes crear un script SQL que:

- cree una tabla llamada `prueba` si no existe;
- use una clave primaria autoincremental llamada `id`;
- tenga una columna `mensaje` de texto corto VARCHAR(100);
- inserte exactamente un registro con el texto:

```text
Entorno inicial creado correctamente
```

Puedes usar el siguiente fichero:

```sql
CREATE TABLE IF NOT EXISTS prueba (
    id INT AUTO_INCREMENT PRIMARY KEY,
    mensaje VARCHAR(100) NOT NULL
);

INSERT INTO prueba (mensaje) VALUES ('Entorno inicial creado correctamente');
```

### Parte 6. Completar `app/index.php`

Debes crear una página PHP que:

- lea `DB_HOST`, `DB_NAME`, `DB_USER` y `DB_PASSWORD` desde variables de entorno;
- intente conectar con MariaDB usando PDO;
- consulte cuántos registros hay en la tabla `prueba`;
- muestre mensajes distintos según la conexión funcione o falle.

La página debe mostrar estas tres ideas finales, aunque el texto exacto puede variar ligeramente si mantiene el mismo sentido:

- PHP se está ejecutando correctamente.
- La conexión con la base de datos está bien o mal.
- El número de registros iniciales disponibles en `prueba`.

Puedes usar el siguiente código. Leélo atentamente y asegúrate de que lo entiendes. Recuerda en el HTML sustituir `NOMBRE` y `APELLIDO` por tu nombre y apellido:

```php
<?php
$host = getenv('DB_HOST') ?: 'db';
$dbname = getenv('DB_NAME') ?: 'ut1db';
$user = getenv('DB_USER') ?: 'ut1user';
$password = getenv('DB_PASSWORD') ?: 'ut1pass';

$estadoConexion = 'Conexión con la base de datos: KO';
$estadoRegistros = 'Registros en tabla prueba: no disponibles';

try {
    $pdo = new PDO("mysql:host=$host;dbname=$dbname;charset=utf8mb4", $user, $password);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

    $total = (int) $pdo->query('SELECT COUNT(*) FROM prueba')->fetchColumn();

    $estadoConexion = 'Conexión con la base de datos: OK';
    $estadoRegistros = 'Registros en tabla prueba: ' . $total;
} catch (Throwable $e) {
    $estadoConexion = 'Conexión con la base de datos: KO';
    $estadoRegistros = 'Registros en tabla prueba: no disponibles';
}
?>
<!doctype html>
<html lang="es">
<head>
    <meta charset="utf-8">
    <title>UT1 - Entorno reproducible</title>
</head>
<body>
    <h1>UT1 - Entorno reproducible de implantación web de NOMBRE y APELLIDO</h1>
    <p>PHP se está ejecutando correctamente.</p>
    <p><?= htmlspecialchars($estadoConexion, ENT_QUOTES, 'UTF-8') ?></p>
    <p><?= htmlspecialchars($estadoRegistros, ENT_QUOTES, 'UTF-8') ?></p>
</body>
</html>
```

### Parte 7. Preparar `.env.example` y `.env`

Debes definir en `.env.example` las variables de entorno:

- nombre de base de datos;
- usuario;
- contraseña;
- contraseña de `root`;
- host de la base de datos.

Después crea `.env` a partir de ese archivo para poder arrancar el proyecto.

### Parte 8. Levantar y comprobar el stack

Debes decidir y ejecutar, al menos, los comandos necesarios para:

- construir o reconstruir el servicio PHP si hace falta;
- arrancar el stack;
- comprobar qué servicios están activos;
- ver logs cuando algo falle;
- parar el stack;
- volver a levantarlo para comprobar reproducibilidad.

En el `README.md` debes anotar los comandos exactos que finalmente has usado.

---

## 7. Evidencias mínimas que debes obtener

Antes de dar la práctica por terminada, debes poder demostrar todo esto:

1. `docker compose ps` muestra los tres servicios en funcionamiento.
2. `http://localhost:8080` responde en el navegador.
3. La página confirma que PHP se ejecuta.
4. La página confirma que la conexión con la base de datos funciona.
5. La página muestra que existe 1 registro inicial en la tabla `prueba`.
6. Sabes decir qué archivo tocarías si fallara:
   - la conexión con la base de datos;
   - el reenvío de PHP;
   - la inicialización SQL.

---

## 8. Entrega

Debes subir los cambios al mismo repositorio privado del módulo usado en la práctica 1, manteniendo el proyecto dentro de `unidades/UT1/ut1-entorno-web/`.

La entrega mínima debe incluir:

- el proyecto `unidades/UT1/ut1-entorno-web/` actualizado;
- los archivos completados por ti;
- el `README.md` ampliado con:
  - Fuentes consultadas
  - Tabla con ficheros y su función
  - Ejecución (explicado en Parte 8)
  - Uso de la IA
- al menos tres commits adicionales explicativos sobre la práctica 2;
- los cambios subidos a la rama de trabajo correspondientes y listos para revisión.

---

## 9. Errores típicos a evitar

### Usar `localhost` entre contenedores
Dentro del stack, PHP no debe conectarse a MariaDB usando `localhost`, sino el nombre del servicio `db`.

### Limitarte a copiar sin verificar
Aunque consultes documentación o ejemplos, si no compruebas qué hace cada línea, no podrás corregir el entorno cuando falle.

### No mirar logs
Si el stack no arranca o la web no responde, la reacción esperable es revisar `docker compose logs`, no probar cambios al azar.

### Documentar solo el resultado final
En implantación web también cuenta dejar rastro de qué problema hubo y cómo se resolvió.

---

## 10. Cómo se evaluará esta práctica

El profesor valorará especialmente estas evidencias:

1. que el stack funciona de verdad;
2. que sabes explicar por qué has completado así cada archivo clave;
3. que has consultado información útil y la has integrado con criterio;
4. que sabes localizar el origen de un error básico;
5. que tu documentación permite reconstruir el proceso seguido.

No se busca que memorices una receta, sino que seas capaz de montar un entorno guiado con comprensión técnica.

---

## 11. Checklist rápido del alumno

- [ ] He completado `compose.yaml` sin copiar una solución cerrada línea por línea.
- [ ] He investigado qué necesita PHP para conectar con MariaDB.
- [ ] He creado `php/Dockerfile` con criterio.
- [ ] He completado `nginx/default.conf` y entiendo qué hace.
- [ ] He creado `sql/init.sql` con la tabla y el registro pedido.
- [ ] He completado `app/index.php` y sé explicar su flujo.
- [ ] He arrancado el stack y he revisado logs cuando ha hecho falta.
- [ ] Mi `README.md` documenta comandos, fuentes y problemas resueltos.
- [ ] He subido los cambios al repositorio privado del módulo.

---