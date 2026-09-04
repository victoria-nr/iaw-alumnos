# Tutorial previo: Git y GitHub para tu repositorio de entregas

Si nunca has usado Git ni GitHub, lee esta guía antes de empezar con [Entregas del curso](entregas.md).

El objetivo no es que te conviertas en experto en Git, sino que seas capaz de:

- crear tu repositorio privado desde una plantilla;
- mantener una copia en tu ordenador;
- guardar tu trabajo con commits pequeños;
- subirlo a GitHub sin perder cambios;
- abrir Pull Requests para que el profesor pueda revisarlo.

!!! info "Qué leer después"
    Cuando termines esta guía, continúa con [Entregas del curso](entregas.md), donde se explican las normas concretas del trabajo durante el curso.

!!! warning "Idea importante"
    Git no guarda automáticamente tus cambios en el historial. Hasta que no haces `commit`, el trabajo solo está en tus archivos locales. Hasta que no haces `push`, GitHub no ve esos cambios.

## 1. Qué es Git y qué es GitHub

- **Git** es la herramienta que registra cambios en tus archivos.
- **GitHub** es la plataforma web donde alojarás tu repositorio privado y compartirás ese trabajo con el profesor.

Piensa en ello así:

- Git trabaja sobre todo en tu ordenador.
- GitHub muestra una copia remota de tu repositorio en Internet.

## 2. Vocabulario mínimo que necesitas

| Concepto | Significado |
|---|---|
| Repositorio | Carpeta de trabajo controlada por Git. Guarda archivos e historial de cambios. |
| Repositorio remoto | La copia del repositorio en GitHub. |
| Clonar | Descargar en tu ordenador una copia completa del repositorio remoto. |
| `main` | Rama principal del repositorio. |
| Rama | Línea de trabajo separada dentro del mismo repositorio. |
| Commit | Punto de guardado con mensaje. Explica qué has cambiado. |
| `push` | Subir commits desde tu ordenador a GitHub. |
| `pull` | Traer cambios desde GitHub a tu ordenador. |
| Pull Request | Solicitud para revisar una rama antes de integrarla en `main`. |
| Repositorio privado | Repositorio que no puede ver cualquiera. Solo acceden las personas invitadas. |
| Colaborador | Persona con permiso para entrar en tu repositorio privado. |

No necesitas memorizar términos más avanzados para seguir el curso.

## 3. Preparación inicial en tu ordenador

Si todavía no has instalado Git, revisa primero [Instalación](instalacion.md).

Una vez instalado, abre una terminal y configura tu nombre y correo una sola vez:

```bash
git config --global user.name "Nombre Apellido"
git config --global user.email "tu_correo@example.com"
```

Puedes comprobarlo con:

```bash
git config --global --list
```

Usa un correo que reconozcas y que puedas asociar con tu cuenta de GitHub.

Si al clonar o al hacer `push` GitHub te pide iniciar sesión, es normal. Sigue la ventana del navegador o de Visual Studio Code y completa el acceso.

## 4. Qué harás una sola vez al principio del curso

### 4.1. Crear el repositorio desde la plantilla

1. Entra en el repositorio plantilla indicado por el profesor.
2. Pulsa **Use this template**.
3. Elige **Create a new repository**.
4. Asigna un nombre con este patrón:

```text
iaw-entregas-nombre-apellido
```

5. Marca el repositorio como **Private**.
6. Crea el repositorio.

No uses **Fork** salvo que el profesor te lo pida expresamente. En este curso el flujo previsto es crear un repositorio nuevo a partir de la plantilla.

### 4.2. Invitar al profesor como colaborador

1. Entra en tu repositorio.
2. Ve a **Settings**.
3. Entra en **Collaborators** o **Collaborators and teams**.
4. Pulsa **Add people**.
5. Busca el usuario de GitHub del profesor.
6. Envía la invitación.

Mientras el profesor no tenga acceso, no podrá revisar tu trabajo en un repositorio privado.

### 4.3. Clonar el repositorio en tu ordenador

Clonar significa descargar una copia completa del repositorio para trabajar localmente.

Esto se hace una sola vez:

```bash
git clone URL_DE_TU_REPOSITORIO
cd iaw-entregas-nombre-apellido
```

Después, abre esa carpeta con Visual Studio Code.

## 5. Flujo de trabajo habitual durante el curso

Este será el ciclo que repetirás muchas veces.

### 5.1. Antes de empezar, actualiza `main`

```bash
git checkout main
git pull
```

Con esto te aseguras de partir de la rama principal actualizada.

### 5.2. Crea una rama para el bloque en el que vas a trabajar

Ejemplo para el documento de ejercicios de la UT1:

```bash
git checkout -b ut1-ejercicios
```

Ejemplo para una práctica concreta:

```bash
git checkout -b ut2-practica-1-presupuesto
```

Si esa rama ya existe porque vas a continuar trabajo anterior, no la crees otra vez. Entra directamente en ella:

```bash
git checkout ut2-practica-1-presupuesto
```

### 5.3. Trabaja en la carpeta correcta

Ejemplos habituales:

```text
unidades/UT1/ejercicios.md
unidades/UT1/ut1-entorno-web/
unidades/UT2/practica-1/
unidades/UT3/practica-ut3-incidencias/
```

Guarda los archivos normalmente desde VS Code.

Si una práctica convive con otras aplicaciones dentro del mismo repositorio, no pasa nada: cada proyecto debe estar aislado dentro de su carpeta y su `README.md` debe indicar cómo arrancarlo.

### 5.4. Revisa qué ha cambiado

```bash
git status
```

Este comando te dice:

- en qué rama estás;
- qué archivos han cambiado;
- qué archivos están preparados para commit;
- si te falta hacer `push`.

Si solo aprendes un comando para orientarte cuando algo te confunde, que sea `git status`.

### 5.5. Haz un commit con un mensaje claro

Cuando completes una parte pequeña del trabajo:

```bash
git add .
git commit -m "Completa mini ejercicios de UT1"
```

Si prefieres ser más preciso, puedes añadir solo un archivo o carpeta concretos:

```bash
git add unidades/UT2/ejercicios.md
git add unidades/UT3/practica-ut3-agenda/
```

Haz commits pequeños y frecuentes. Un commit debe representar un avance reconocible.

### 5.6. Sube la rama a GitHub

La primera vez que subes una rama:

```bash
git push -u origin ut2-practica-1-presupuesto
```

Después, normalmente bastará con:

```bash
git push
```

### 5.7. Abre o actualiza una Pull Request (PR)

Una Pull Request es una solicitud de revisión: sirve para decir "Profesor, revisa esta rama antes de incorporarla a `main`".

#### Cuándo debes abrirla

Abre una Pull Request cuando hayas terminado un bloque claro de trabajo, por ejemplo:

- el `ejercicios.md` de una unidad;
- una práctica completa;
- una corrección importante pedida por el profesor.

La norma general es simple:

- una rama para un bloque de trabajo;
- una Pull Request para esa rama.

No hace falta abrir una Pull Request nueva por cada commit.

#### Qué debes hacer antes de abrirla

Antes de entrar en GitHub, comprueba que:

- estás en la rama correcta;
- has guardado tus archivos;
- has hecho al menos un `commit`;
- has subido esa rama con `git push`.

Si no haces `push`, GitHub no verá tus cambios.

#### Cómo abrirla en GitHub

1. Entra en tu repositorio en GitHub.
2. Si aparece el aviso **Compare & pull request**, púlsalo.
3. Si no aparece, entra en **Pull requests** y pulsa **New pull request**.
4. En la Pull Request → panel derecho → Reviewers → selecciona el usuario de tu profesor. Este paso es muy importante.
5. Revisa que la rama base sea `main` y que la rama de comparación sea tu rama, por ejemplo `ut2-practica-1-presupuesto`.
6. Comprueba que en la vista previa aparecen los archivos correctos.
7. Pulsa **Create pull request**.

#### Qué escribir en la Pull Request

El título y la descripción deben dejar claro qué estás entregando.

Ejemplo de título para ejercicios:

```text
UT2 ejercicios: formularios y validación
```

Ejemplo de descripción:

```md
Unidad: UT2
Bloque: ejercicios
Ruta: unidades/UT2/ejercicios.md
Uso de IA: sí, para contrastar una validación y entender un error con POST
Comprobaciones: casos correctos y caso con errores de validación
```

Ejemplo de título para una práctica:

```text
UT3 práctica 2: gestor de incidencias con MariaDB
```

Ejemplo de descripción:

```md
Unidad: UT3
Bloque: práctica 2
Ruta: unidades/UT3/practica-ut3-incidencias/
Ejecución: docker compose up -d --build
URL o puerto: http://localhost:8084
Uso de IA: no
```

No hace falta escribir mucho, pero sí lo suficiente para que el profesor entienda qué está revisando y cómo comprobarlo.

#### Qué pasa después de abrirla

Cuando abres la Pull Request empieza la revisión:

1. El profesor entra en la Pull Request y revisa archivos, commits y comentarios.
2. Si hace falta, te pedirá correcciones.
3. Tú corriges en la misma rama, haces `commit` y `push`.
4. La misma Pull Request se actualiza sola.
5. Cuando el trabajo ya está correcto, el profesor decide si se da por válido y qué hacer después.

Mientras la entrega siga en revisión, la Pull Request debe quedarse abierta.


#### Qué hacer cuando el profesor solicita cambios (Request changes)

Si el profesor revisa tu Pull Request y selecciona **Request changes**, significa que la entrega necesita algunas correcciones antes de darse por válida.

No debes crear una nueva Pull Request. Debes seguir trabajando sobre la misma.

##### 1. Lee los comentarios del profesor

En GitHub, entra en tu Pull Request y revisa los comentarios recibidos.

Los comentarios pueden aparecer:

- En la pestaña **Conversation**.
- Sobre líneas concretas de código en la pestaña **Files changed**.

Lee todos los comentarios antes de empezar a modificar el código.

##### 2. Corrige el código en tu ordenador

Las correcciones deben realizarse normalmente en tu copia local del proyecto utilizando tu editor habitual (VS Code, IntelliJ, Eclipse, etc.).

No es necesario modificar el código desde la web de GitHub.

Realiza los cambios solicitados y comprueba que el programa sigue funcionando correctamente.

##### 3. Haz commit y push

Cuando hayas terminado las correcciones:

```bash
git add .
git commit -m "Corrige comentarios de la revisión"
git push
```

Debes hacer el `push` a la misma rama que utilizaste para crear la Pull Request.

##### 4. La Pull Request se actualiza automáticamente

No necesitas crear una nueva Pull Request.

Cuando haces `push`, GitHub añade automáticamente los nuevos commits a la Pull Request que ya estaba abierta.

El profesor podrá revisar los cambios realizados.

##### 5. Responde a los comentarios

Después de subir los cambios, vuelve a la Pull Request y responde a los comentarios indicando qué has corregido.

Por ejemplo:

> Corregido en el último commit.

o

> He modificado el método para controlar el caso indicado en la revisión.

Esto ayuda al profesor a localizar rápidamente las correcciones realizadas.

##### 6. Espera una nueva revisión

El profesor volverá a revisar la misma Pull Request.

Puede ocurrir que:

- La entrega quede aprobada.
- Se soliciten nuevas correcciones.

En este último caso, simplemente repite el mismo proceso: corregir → commit → push → revisión.

> **Importante:** mientras la entrega esté siendo revisada o corregida, la Pull Request debe permanecer abierta. No cierres la Pull Request ni crees una nueva para la misma entrega.

#### Qué es un merge y qué significa cerrar una Pull Request

Hacer **merge** significa pasar los cambios de tu rama a `main`, es decir, incorporarlos a la versión principal del repositorio.

Si en una Pull Request se hace merge:

- los cambios pasan a `main`;
- GitHub la marca como completada;
- normalmente se cierra automáticamente.

Cerrar una Pull Request **sin merge** significa terminar esa revisión sin pasar los cambios a `main`. Eso puede ocurrir, por ejemplo, si la Pull Request se abrió por error, usa la rama equivocada o el profesor solo quería revisar el progreso.

Si se cierra sin merge, tus cambios no desaparecen: siguen en tu rama.

#### Qué debes hacer tú en este curso

La regla práctica es esta:

1. Abre la Pull Request cuando el bloque esté listo para revisión.
2. Déjala abierta.
3. Si el profesor pide cambios, corrígelos en la misma rama y haz `push`.
4. No hagas merge tú mismo, salvo que el profesor lo indique.
5. No la cierres por tu cuenta, salvo que el profesor te lo diga.

#### Cuándo seguir con la misma Pull Request y cuándo abrir otra

Sigue con la misma Pull Request si sigues trabajando en el mismo bloque y en la misma rama.

Abre una Pull Request nueva si empiezas otro bloque, creas otra rama o cambias de unidad o de práctica.

#### Qué no debes hacer

- No abras una Pull Request desde `main` hacia `main`.
- No abras varias Pull Requests para la misma rama salvo que te lo pidan.
- No cierres la Pull Request solo porque luego hayas hecho otro commit.

#### Ejemplo completo

Ana termina el archivo `unidades/UT2/ejercicios.md` en la rama `ut2-ejercicios`. Hace `commit`, hace `push` y abre una Pull Request hacia `main`. El profesor la revisa. Si ve errores, deja comentarios; Ana corrige en esa misma rama, hace otro `commit` y otro `push`, y la misma Pull Request se actualiza. Si el trabajo ya es correcto, el profesor la da por válida y, si corresponde, te pide que hagas  merge. En ese momento GitHub cierra la Pull Request automáticamente.

## 6. Qué harás muchas veces y qué solo harás una vez

Solo una vez al principio:

- crear el repositorio desde la plantilla;
- invitar al profesor;
- clonar el repositorio en tu ordenador.

Muchas veces durante el curso:

- `git checkout main`;
- `git pull`;
- `git checkout -b ...` o `git checkout ...`;
- `git status`;
- `git add ...`;
- `git commit -m "..."`;
- `git push`;
- abrir o actualizar Pull Requests.

## 7. Problemas habituales y qué significan

### 7.1. "nothing to commit, working tree clean"

Significa que Git no ve cambios pendientes.

Puede deberse a una de estas causas:

- no has modificado nada todavía;
- has olvidado guardar el archivo en VS Code;
- ya hiciste el commit antes.

### 7.2. "a branch named ... already exists"

Significa que esa rama ya la creaste en otro momento.

En ese caso entra en ella, en lugar de volver a crearla:

```bash
git checkout NOMBRE_DE_LA_RAMA
```

### 7.3. He hecho commit, pero no veo los cambios en GitHub

Lo más probable es que te falte hacer:

```bash
git push
```

Recuerda: `commit` guarda en tu ordenador; `push` sube a GitHub.

### 7.4. He empezado a trabajar por error en `main`

Si todavía no has hecho commit, puedes crear la rama en ese momento y tus cambios pasarán a ella:

```bash
git checkout -b NOMBRE_DE_LA_RAMA
```

Haz esto cuanto antes, antes de seguir trabajando.

### 7.5. Git me muestra un conflicto

Un conflicto aparece cuando Git no sabe combinar dos cambios automáticamente.

Si no entiendes lo que ha pasado:

- no uses `git push --force`;
- no borres archivos al azar;
- revisa `git status`;
- pide ayuda al profesor mostrando el mensaje exacto.

## 8. Normas para no romper tu repositorio

- No trabajes los ejercicios en el repositorio público de apuntes.
- No borres ni renombres carpetas base de unidades si no se te pide.
- No subas contraseñas, tokens ni datos sensibles.
- No uses `git push --force` salvo que el profesor te lo indique.
- No dejes todos los cambios para un único commit final.
- Mantén el repositorio como **privado**.
- Documenta en cada práctica cómo se arranca y qué puerto usa si convive con otras aplicaciones en el mismo repositorio.

## 9. Chuleta mínima de comandos

```bash
git clone URL
```

Descarga el repositorio por primera vez.

```bash
git checkout main
git pull
```

Te coloca en la rama principal y la actualiza.

```bash
git checkout -b nombre-rama
```

Crea una rama nueva y entra en ella.

```bash
git status
```

Muestra el estado actual del repositorio.

```bash
git add .
git commit -m "mensaje claro"
```

Prepara cambios y crea un commit.

```bash
git push -u origin nombre-rama
```

Sube la rama por primera vez.

```bash
git push
```

Sube nuevos commits de una rama ya conectada con GitHub.

## 10. Qué información debes dar si pides ayuda

Si algo falla, no digas solo "Git no va".

Da siempre estos datos:

- el comando exacto que has ejecutado;
- el mensaje de error completo;
- la salida de `git status`;
- la rama en la que estabas;
- qué querías hacer exactamente.

Con eso será mucho más fácil ayudarte sin tocar tu repositorio a ciegas.