# Práctica 1 · Preparación exacta del proyecto base de la UT1

## 1. Qué vas a hacer

En esta práctica vamos a preparar el proyecto base para la siguiente práctica. El proyecto se llamará `ut1-entorno-web`, que será la base de la práctica 2 y quedará dentro de `unidades/UT1/` en tu repositorio privado del módulo.

El objetivo es crear toda la estructura del proyecto, integrarlo en tu repositorio Git del módulo y documentar de forma mínima y útil qué contiene y para qué servirá.

---

## 2. Qué demuestra esta práctica

Con esta práctica debes demostrar que sabes:

- preparar un proyecto base;
- verificar qué herramientas forman parte del entorno de trabajo;
- usar y revisar Git dentro del repositorio del módulo;
- documentar el punto de partida del proyecto.

### Criterios del RA1 trabajados

- **CE1**. Identificación del software necesario.  
- **CE2**. Identificación de tecnologías empleadas.  
- **CE8**. Uso de plataformas orientadas a prueba y desarrollo.  
- **CE9**. Documentación de procedimientos.

---

## 3. Caso de trabajo

Dentro de la carpeta `unidades/UT1/` de tu repositorio privado del módulo vas a crear un proyecto con estos elementos iniciales:

```text
ut1-entorno-web/
├── .env.example
├── compose.yaml
├── app/
│   └── index.php
├── nginx/
│   └── default.conf
└── sql/
	└── init.sql
```

Tu tarea consiste en crear esta estructura de carpetas y ficheros dentro de `unidades/UT1/ut1-entorno-web`, dejarla versionada en tu repositorio del módulo y lista para continuar con la práctica 2.

---

## 4. Resultado exacto que debes obtener

Al finalizar esta práctica, tu carpeta `unidades/UT1/ut1-entorno-web` debe incluir al menos:

- la estructura anterior;
- el proyecto versionado dentro de tu repositorio Git del módulo;
- un archivo `README.md` con el contenido indicado en esta práctica;
- un archivo `estado_entorno.txt` con los comandos de comprobación indicados;
- un commit con el mensaje exacto especificado.

---

## 5. Tareas obligatorias

### Parte 1. Crea nueva rama de trabajo para esta práctica

Crea una rama específica para esta práctica llamada `ut1-practica-entorno-web` 
y sitúate en ella.


### Parte 2. Crear estructura del proyecto dentro del repo del módulo

Crea la estructura de ficheros y carpetas dentro de la carpeta correspondiente, `ut1-entorno-web`. Si has creado el repositorio desde la plantilla, no debes ejecutar `git init` dentro del proyecto, porque el repositorio Git ya existe en la raíz del módulo.


### Parte 3. Crear el `README.md`

Crea un archivo `README.md` con este contenido (debes rellenar donde corresponda)o actualiza el archivo si ya existe:

```md
# UT1 · Proyecto base del entorno reproducible

## Objetivo
Preparar la base del proyecto de la UT1 para continuar con la práctica de despliegue reproducible.

## Archivos localizados
- compose.yaml
- .env.example
- app/index.php
- nginx/default.conf
- sql/init.sql

## Papel de cada herramienta en esta UT
- Git: (rellenar)
- Docker: (rellenar)
- Docker Compose: (rellenar)

## Estado final
Repositorio inicializado y proyecto listo para la práctica 2.
```

En este `README.md` puedes mantener esa frase final, aunque el repositorio Git del módulo ya exista previamente.


### Parte 4. Crear el archivo `estado_entorno.txt`

Crea un archivo `estado_entorno.txt` con el resultado de ejecutar los siguientes comandos:

```text
git --version
docker --version
docker compose version
git status
```

### Parte 5. Revisar la estructura del proyecto

Comprueba que en tu repositorio existen y se pueden localizar rápidamente estos archivos:

- `compose.yaml`
- `.env.example`
- `app/index.php`
- `nginx/default.conf`
- `sql/init.sql`

### Parte 6. Registrar el estado inicial de esta práctica y subir cambios.

En la rama correspondiente, haz un commit con el siguiente mensaje: `"Base del proyecto UT1 preparada"`. Recuerda subir los cambios a GitHub.



## 6. Criterios de éxito

La práctica se considerará correcta si se cumple todo esto:

- la estructura de carpetas y ficheros coincide con la indicada;
- el `README.md` contiene el texto pedido;
- `estado_entorno.txt` contiene el resultado de los cuatro comandos exactos;
- el proyecto está versionado dentro del repositorio del módulo en la rama correspondiente;
- el commit inicial usa el mensaje exacto solicitado.
- se han subido los cambios al repositorio privado del módulo.

---


