# Guía de comandos · UT1

Esta guía recoge los comandos mínimos que conviene tener a mano durante la unidad.  
No sustituye a los apuntes: sirve como **chuleta operativa** para trabajar el entorno, entender qué está ocurriendo y reaccionar ante errores sencillos.

---

## 1. Git

### Comprobar que Git está disponible

```bash
git --version
```

### Qué hace
Muestra la versión de Git instalada.

### Para qué sirve en esta UT
Permite comprobar que el alumno puede trabajar con el repositorio del proyecto y registrar cambios de forma ordenada.

---

### Clonar un repositorio

```bash
git clone URL_DEL_REPO
```

### Cuándo usarlo
Cuando el proyecto ya existe y quieres descargar su contenido a tu equipo.

---

### Ver el estado de trabajo

```bash
git status
```

### Qué debes observar
- archivos modificados;
- archivos no rastreados;
- si hay cambios pendientes de commit.

---

### Añadir cambios

```bash
git add .
```

También puedes añadir un archivo concreto:

```bash
git add README.md
```

---

### Crear un commit

```bash
git commit -m "Describe el cambio"
```

Ejemplo:

```bash
git commit -m "Añade estructura base de la práctica 2"
```

---

### Subir cambios al remoto

```bash
git push
```

### Qué aporta en esta UT
No es solo “guardar código”. Te permite:

- llevar un historial de decisiones;
- volver atrás si algo se rompe;
- compartir el proyecto con el profesor o el grupo;
- documentar el progreso de una práctica.

---

### Crear un repositorio local desde cero

```bash
git init
```

---

### Crear y cambiar a una rama de trabajo

```bash
git checkout -b ut1-ejercicios
```

Si la rama ya está creada, se cambia a dicha rama sin la opción `-b`

```bash
git checkout ut1-ejercicios
```


## 2. Docker

### Comprobar instalación

```bash
docker --version
```

### Ver contenedores activos

```bash
docker ps
```

### Ver todos los contenedores, también los detenidos

```bash
docker ps -a
```

### Ver imágenes disponibles

```bash
docker images
```

### Ver logs de un contenedor

```bash
docker logs NOMBRE_CONTENEDOR
```

Ejemplo:

```bash
docker logs ut1-nginx-1
```

### Para qué sirve en esta UT
Los logs son una de las herramientas más útiles para no trabajar a ciegas. Ayudan a saber si:

- el contenedor ha arrancado;
- Nginx tiene un error de configuración;
- PHP falla al procesar;
- la base de datos no levanta correctamente.

---

## 3. Docker Compose

### Comprobar que Compose está disponible

```bash
docker compose version
```

---

### Levantar los servicios en segundo plano

```bash
docker compose up -d
```

### Qué hace
Construye o arranca los servicios definidos en `compose.yaml` y los deja ejecutándose en segundo plano.

---

### Levantar mostrando la salida en pantalla

```bash
docker compose up
```

### Cuándo conviene usarlo
Cuando estás depurando y quieres ver directamente la salida de los servicios.

---

### Parar y eliminar los servicios del proyecto

```bash
docker compose down
```

---

### Reiniciar servicios

```bash
docker compose restart
```

O un servicio concreto:

```bash
docker compose restart nginx
```

---

### Ver estado de los servicios

```bash
docker compose ps
```

---

### Ver logs de todo el stack

```bash
docker compose logs
```

### Ver logs de un servicio concreto

```bash
docker compose logs nginx
docker compose logs php
docker compose logs db
```

### Seguir logs en tiempo real

```bash
docker compose logs -f php
```

---

### Ejecutar un comando dentro de un servicio

```bash
docker compose exec php sh
```

### Cuándo puede servir
Para inspeccionar el contenedor, comprobar rutas, variables o conectividad.

---

### Reconstruir imágenes al levantar

```bash
docker compose up -d --build
```

### Cuándo tiene sentido
Cuando has cambiado la definición del entorno y necesitas reconstruir la imagen.

---

## 4. Navegación y comprobación básica del servicio

### Probar la URL en navegador

Ejemplo habitual:

```text
http://localhost:8080
```

### Probar cabeceras HTTP desde terminal

```bash
curl -I http://localhost:8080
```

### Qué debes observar
- código de estado;
- si responde el servidor;
- cabeceras básicas.

---

## 5. Comandos de apoyo para el proyecto

### Ver el árbol de archivos de forma simple

```bash
ls -la
```

### Buscar rápidamente una cadena en ficheros

```bash
grep -R "fastcgi_pass" .
```

### Para qué puede servir
Muy útil para localizar una configuración cuando el alumno no recuerda en qué archivo estaba.

---


## 6. Errores típicos y pista rápida

### La web no responde
Revisar:
- `docker compose ps`
- `docker compose logs nginx`

### PHP no se procesa
Revisar:
- configuración de Nginx;
- logs del servicio `php`;
- rutas compartidas por volumen.

### La aplicación no conecta con la base de datos
Revisar:
- nombre del servicio `db`;
- variables de entorno;
- logs del servicio `db`;
- que no se esté usando `localhost` desde otro contenedor.

### El entorno estaba funcionando y deja de hacerlo tras un cambio
Revisar:
- último cambio en `compose.yaml`;
- último cambio en `default.conf`;
- si hace falta recrear con `--build`.

---
