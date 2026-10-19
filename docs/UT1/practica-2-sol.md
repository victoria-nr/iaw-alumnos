# Práctica 2 (posible solución) · Entorno web reproducible guiado con `Docker Compose`


## 1. Posible solución (archivos)

### `compose.yaml`

```yaml
services:
    nginx:
        image: nginx:stable-alpine
        ports:
            - "8080:80"
        volumes:
            - ./app:/var/www/html
            - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
        depends_on:
            - php

    php:
        build: ./php
        working_dir: /var/www/html
        volumes:
            - ./app:/var/www/html
        environment:
            DB_HOST: ${DB_HOST}
            DB_NAME: ${DB_NAME}
            DB_USER: ${DB_USER}
            DB_PASSWORD: ${DB_PASSWORD}
        depends_on:
            - db

    db:
        image: mariadb:11
        environment:
            MARIADB_DATABASE: ${DB_NAME}
            MARIADB_USER: ${DB_USER}
            MARIADB_PASSWORD: ${DB_PASSWORD}
            MARIADB_ROOT_PASSWORD: ${DB_ROOT_PASSWORD}
        ports:
            - "3307:3306"
        volumes:
            - db_data:/var/lib/mysql
            - ./sql/init.sql:/docker-entrypoint-initdb.d/init.sql:ro

volumes:
    db_data:
```

### `.env.example`

```env
DB_NAME=ut1db
DB_USER=ut1user
DB_PASSWORD=ut1pass
DB_ROOT_PASSWORD=rootpass
DB_HOST=db
```

### `php/Dockerfile`

```dockerfile
FROM php:8.3-fpm-alpine

RUN docker-php-ext-install pdo_mysql
```

### `nginx/default.conf`

```nginx
server {
        listen 80;
        server_name localhost;

        root /var/www/html;
        index index.php index.html;

        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }

        location ~ \.php$ {
                include fastcgi_params;
                fastcgi_pass php:9000;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
}
```

### `sql/init.sql`

```sql
CREATE TABLE IF NOT EXISTS prueba (
    id INT AUTO_INCREMENT PRIMARY KEY,
    mensaje VARCHAR(100) NOT NULL
);

INSERT INTO prueba (mensaje) VALUES ('Entorno inicial creado correctamente');
```

### `app/index.php`

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

### `README.md`

````md
# UT1 · Entorno reproducible con Docker Compose

## Requisitos previos
- Docker
- Docker Compose

## Preparación inicial
```bash
cp .env.example .env
```

## Arranque del entorno
```bash
docker compose up -d --build
```

## Parada del entorno
```bash
docker compose down
```

## Servicios del proyecto
- nginx
- php
- db

## Puertos publicados
- http://localhost:8080
- MariaDB en el puerto 3307 del equipo anfitrión

## Verificación esperada
La página principal debe mostrar que PHP funciona, que la conexión con la base de datos es correcta y que existe 1 registro inicial en la tabla `prueba`.
````

---

## 2. Secuencia exacta de trabajo

Dentro de `ut1-entorno-web`, ejecuta estos pasos en este orden:

1. Crea la carpeta `php` si todavía no existe.
2. Deja todos los archivos anteriores con el contenido exacto indicado.
3. Copia `.env.example` a `.env` con este comando:

```bash
cp .env.example .env
```

4. Levanta el entorno:

```bash
docker compose up -d --build
```

5. Comprueba el estado de los servicios:

```bash
docker compose ps
```

6. Comprueba la página principal en `http://localhost:8080`.
7. Revisa logs básicos:

```bash
docker compose logs nginx --tail=20
docker compose logs php --tail=20
docker compose logs db --tail=20
```

8. Para y vuelve a levantar el stack para comprobar reproducibilidad:

```bash
docker compose down
docker compose up -d
```

---

## 3. Resultado exacto que debe verse en el navegador

Al abrir `http://localhost:8080`, la página debe mostrar estas tres líneas de verificación:

- `PHP se está ejecutando correctamente.`
- `Conexión con la base de datos: OK`
- `Registros en tabla prueba: 1`

