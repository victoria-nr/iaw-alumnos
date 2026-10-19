# Solución de los mini ejercicios · UT1 · Entorno reproducible de implantación web

Este documento recoge las posibles soluciones de los mini ejercicios de los apuntes.

---

## Mini ejercicio 1

| Aplicación web | ¿El usuario ve HTML, datos o ambas cosas? | Explicación breve |
|---|---|---|
| Aules | ambas cosas | El navegador recibe HTML para la interfaz y también datos generados por la aplicación según el usuario y la asignatura. |
| Gmail web | ambas cosas | La bandeja se muestra como interfaz web, pero el contenido procede de datos dinámicos del correo del usuario. |
| OpenStreetMap | ambas cosas | La página carga interfaz HTML y después muestra datos cartográficos que se solicitan al servidor. |

Respuesta en dos frases:

Una aplicación web funciona con un modelo cliente-servidor en el que el navegador pide recursos a un sistema remoto. Un programa de escritorio ejecuta la mayor parte de su lógica directamente en el equipo del usuario y no depende de HTTP para funcionar.

---

## Mini ejercicio 2

1. `https://intranet-centro.example/assets/logo-centro.png` → **estático**. Es un archivo de imagen que el servidor entrega tal como está guardado.
2. `https://ut1.example/index.html` → **estático**. Es un archivo HTML fijo que no necesita generar contenido en tiempo real.
3. `https://ut1.example/noticias.php?id=8` → **dinámico**. La respuesta depende de código servidor y del parámetro `id=8`.
4. `https://api.ut1.example/productos` → **dinámico**. La API genera y devuelve datos en función de la lógica de la aplicación.
5. `https://ut1.example/catalogo.html` con carga posterior desde `/api/productos` → **mixto**. El HTML inicial es estático, pero los productos se incorporan después mediante una llamada dinámica.

---

## Mini ejercicio 3

| Herramienta | Tipo de componente | Tarea principal |
|---|---|---|
| Nginx | servidor web | Recibir peticiones HTTP y servir recursos o delegar el procesamiento. |
| Apache HTTP Server | servidor web | Recibir peticiones HTTP y entregar contenido web. |
| Caddy | servidor web | Servir sitios web y actuar como servidor o proxy. |
| PHP-FPM | runtime o servidor de aplicaciones | Ejecutar código PHP del lado servidor. |
| Node.js | runtime o servidor de aplicaciones | Ejecutar aplicaciones JavaScript en servidor. |
| Tomcat | servidor de aplicaciones | Ejecutar aplicaciones web Java. |
| MariaDB | base de datos | Guardar y recuperar datos persistentes. |
| PostgreSQL | base de datos | Guardar y consultar datos relacionales. |
| MongoDB | base de datos | Guardar y consultar documentos no relacionales. |

1. El alumno estaría confundiendo un servidor web con una base de datos, porque Nginx no almacena registros ni ejecuta consultas SQL.
2. La tienda online no podría conservar usuarios, productos, pedidos ni carritos entre una petición y la siguiente.

---

## Mini ejercicio 4

1. `http://localhost:8080/logo.png`:

```text
navegador -> Nginx -> navegador
```

2. `http://localhost:8080/index.php?seccion=inicio`:

```text
navegador -> Nginx -> PHP-FPM -> Nginx -> navegador
```

3. `POST http://localhost:8080/crear.php` con inserción en base de datos:

```text
navegador -> Nginx -> PHP-FPM -> MariaDB -> PHP-FPM -> Nginx -> navegador
```

---

## Mini ejercicio 5

1. Método HTTP: `GET`
2. Ruta pedida: `/productos`
3. Código de estado: `200 OK`
4. Cabeceras:
	- petición: `User-Agent: curl/8.7.1`
	- respuesta: `Content-Type: application/json`
5. El servidor está devolviendo **datos**, en concreto JSON.

---

## Mini ejercicio 6

| Situación | Opción correcta |
|---|---|
| Cada alumno instala manualmente Apache, PHP y MariaDB en su sistema operativo. | LAMP clásico |
| Todo el grupo usa el mismo `compose.yaml` y los mismos nombres de servicio. | Entorno reproducible con Git + Docker Compose |
| Cambiar de ordenador obliga a repetir la instalación paso a paso. | LAMP clásico |
| El proyecto se puede clonar y levantar con `docker compose up -d`. | Entorno reproducible con Git + Docker Compose |
| Dos alumnos pueden tener versiones distintas de PHP sin darse cuenta. | LAMP clásico |
| La configuración principal del entorno queda descrita en ficheros del proyecto. | Entorno reproducible con Git + Docker Compose |

Conclusión en una frase:

El entorno reproducible con Git y Docker Compose encaja mejor con esta UT porque permite que toda la clase trabaje con la misma configuración y reduce diferencias entre equipos.

---

## Mini ejercicio 7

Comandos exactos:

```bash
mkdir ut1-git-prueba
cd ut1-git-prueba
git init
cat > README.md <<'EOF'
# UT1 entorno de prueba

Proyecto de prueba para practicar Git en Implantación de Aplicaciones Web.
EOF
git add README.md
git commit -m "Inicializa entorno de prueba UT1"
cat >> README.md <<'EOF'

Estado actual: repositorio listo para la práctica.
EOF
git status
```

Resultado esperado de `git status` después de modificar el archivo y antes de hacer otro `git add`:

- Archivos preparados para commit: ninguno.
- Archivos modificados: `README.md`.

---

## Mini ejercicio 8

Comandos exactos:

```bash
docker run --name ut1-nginx-prueba -d -p 8081:80 nginx:stable
docker ps
docker stop ut1-nginx-prueba
docker rm ut1-nginx-prueba
```

1. Imagen usada: `nginx:stable`
2. Nombre del contenedor: `ut1-nginx-prueba`
3. Puerto publicado en el equipo: `8081`
4. Frase correcta: una imagen es la plantilla `nginx:stable` a partir de la que se crea el servicio, y el contenedor es la instancia ejecutada con el nombre `ut1-nginx-prueba`.

---

## Mini ejercicio 9

1. Imagen: `nginx:stable`. Nombre del contenedor: `web-prueba`. Se abriría `http://localhost:8090`.
2. `8090` es el puerto del equipo desde el que se accede; `80` es el puerto en el que Nginx escucha dentro del contenedor.
3. No. Docker no podrá publicar un puerto que ya está ocupado. Se puede cambiar, por ejemplo, a `-p 8091:80`.
4. Comando exacto:

```bash
docker logs web-prueba
```

---

## Mini ejercicio 10

1. Nginx obtiene `index.html` de la carpeta local actual, representada por `$PWD` en el comando.
2. La carpeta aparece en `/usr/share/nginx/html` dentro del contenedor.
3. `:ro` evita que el contenedor modifique los archivos de la carpeta local montada.
4. El archivo se comparte mediante el volumen: Nginx lee directamente la versión actual de la carpeta local. Por eso basta guardar el cambio en `index.html` y recargar el navegador.

---

## Mini ejercicio 11

1. Hay **3 servicios**: `nginx`, `php` y `db`.
2. Imágenes:
	- `nginx` usa `nginx:stable`
	- `php` usa `php:8.3-fpm`
	- `db` usa `mariadb:11`
3. Puerto publicado: `8080:80` en el servicio `nginx`.
4. Si cambias el nombre del servicio `db` y no actualizas la conexión en PHP, la aplicación no encontrará el host de base de datos y fallará la conexión.
5. Comandos exactos:

```bash
docker compose up -d
docker compose down
docker compose up -d
```

Se usa `docker compose down` y no `docker compose stop` porque aquí interesa desmontar el stack y volver a crearlo para comprobar mejor la reproducibilidad del entorno. `stop` solo detiene los contenedores, mientras que `down` detiene y elimina los contenedores y la red del proyecto.

---

## Mini ejercicio 12

1. Servidor web:
	- Caso A: `Nginx`
	- Caso B: `Apache`
2. Runtime o servidor de aplicaciones:
	- Caso A: `PHP-FPM`
	- Caso B: `Apache` + `PHP` integrado mediante un módulo
3. Base de datos:
	- Caso A: `MariaDB`
	- Caso B: `MariaDB`
4. Comparación con el stack de la UT:

El caso A coincide exactamente con el stack de la UT porque usa `Nginx + PHP-FPM + MariaDB`. El caso B se parece en que sigue usando PHP y MariaDB, pero se diferencia en que sustituye Nginx por Apache y no separa el runtime como `PHP-FPM`.

La diferencia importante es que Apache puede ejecutar PHP directamente mediante un módulo, mientras que Nginx necesita un servicio adicional (PHP-FPM) para ejecutar código PHP.

---

## Mini ejercicio 13

1. Cambiar el puerto web: `ut1-entorno-web/compose.yaml`
2. Modificar el comportamiento de Nginx: `ut1-entorno-web/nginx/default.conf`
3. Cambiar una variable de conexión: `ut1-entorno-web/.env.example`
4. Editar la aplicación: `ut1-entorno-web/app/index.php`
5. Frase correcta: separar configuración, código y datos en carpetas distintas permite localizar antes cada cambio y reduce errores de mantenimiento.

---

## Mini ejercicio 14

1. `404 Not Found` al abrir `http://localhost:8080/logo.png` → `docker compose logs nginx`. La petición la recibe Nginx y el problema suele estar en la ruta o en la publicación del recurso estático.
2. Error PHP al abrir `http://localhost:8080/index.php` → `docker compose logs php`. El código se ejecuta en PHP-FPM y ahí aparecerá el error de ejecución.
3. Mensaje `SQLSTATE[HY000] [2002] Connection refused` → `docker compose logs`. La visión global permite comprobar rápidamente si el fallo viene de la aplicación, del arranque de la base de datos o de ambos servicios.
4. El servicio `db` se detiene nada más arrancar → `docker compose logs db`. El primer lugar donde mirar es el propio servicio de base de datos que está fallando al iniciar.

---

## Mini ejercicio 15

1. No subiría  `DB_PASSWORD=ut1pass` ni `DB_ROOT_PASSWORD=rootpass`, porque son credenciales de acceso.
2. Se están publicando los puertos `8080:80` para `nginx` y `3307:3306` para `db`.
3. No hace falta publicar todos esos puertos al exterior: para la mayoría de prácticas basta con publicar la web y mantener la base de datos accesible solo dentro del stack.
4. Ventaja concreta: una documentación clara permite reproducir el entorno, saber qué servicio expone cada puerto y localizar antes dónde modificar la configuración.

---
