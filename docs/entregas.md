# Entregas del curso: repositorio privado del módulo

Durante el curso usarás un único repositorio privado de GitHub para entregar **todo tu trabajo del módulo de Implantación de Aplicaciones Web**.

Ese repositorio será tu cuaderno técnico del módulo: ahí irás documentando los ejercicios de cada unidad y subiendo las prácticas completas con su código, sus README y sus evidencias.

!!! info "Si es tu primera vez con Git"
    Antes de seguir, lee [Tutorial previo: Git y GitHub para tu repositorio de entregas](git-github-entregas.md). Ahí tienes el vocabulario básico y el flujo de trabajo paso a paso.

## 1. Idea general

Durante el curso crearás e irás manteniendo y ampliando tu **repositorio de entregas del módulo**. A continuación se explican sus características de forma más detallada:

* Este repositorio lo crearás en GitHub a partir de un repositorio plantilla que te proporcionará el profesor y lo marcarás como privado.
* El profesor tendrá acceso a tu repositorio privado como colaborador.
* Cada unidad tendrá su propia carpeta.
* Los mini ejercicios y ejercicios finales de una misma unidad se documentarán en un único archivo `ejercicios.md`.
* Cada práctica se entregará como un proyecto independiente dentro de la carpeta de su unidad.
* Deberás hacer commits frecuentes, no subir todo el trabajo de golpe al final.
* El profesor podrá revisar tu progreso, tus cambios, tus Pull Requests y tu historial de commits.

No debes entregar ejercicios modificando el repositorio público de apuntes. Las entregas se realizarán únicamente en tu repositorio privado personal.

---

## 2. Crear el repositorio desde la plantilla

1. Entra en el repositorio plantilla indicado por el profesor.
2. Pulsa **Use this template**.
3. Elige **Create a new repository**.
4. Ponle este nombre:

```text
iaw-entregas-nombre-apellido
```

Ejemplo:

```text
iaw-entregas-ana-garcia
```

5. Marca el repositorio como **Private**.
6. Crea el repositorio.

---

## 3. Invitar al profesor

Después de crear el repositorio privado, debes invitar al profesor como colaborador.

En GitHub:

1. Entra en tu repositorio privado.
2. Ve a **Settings**.
3. Entra en **Collaborators** o **Collaborators and teams**.
4. Pulsa **Add people**.
5. Busca el usuario de GitHub del profesor.
6. Envía la invitación.

El profesor indicará en clase cuál es su usuario de GitHub.

---

## 4. Clonar tu repositorio

Copia la URL de tu repositorio y clónalo en tu ordenador:

```bash
git clone URL_DE_TU_REPOSITORIO
cd iaw-entregas-nombre-apellido
```

Abre esa carpeta con Visual Studio Code.

---

## 5. Estructura esperada del repositorio

Tu repositorio tendrá una estructura similar a esta:

```text
iaw-entregas-ana-garcia/
├── README.md
└── unidades/
    ├── UT1/
    │   ├── ejercicios.md
    │   └── ut1-entorno-web/
    │       └── README.md
    ├── UT2/
    │   ├── ejercicios.md
    │   ├── practica-1/
    │   │   └── README.md
    │   └── practica-2/
    │       └── README.md
    ├── UT3/
    │   ├── ejercicios.md
    │   ├── practica-ut3-agenda/
    │   │   └── README.md
    │   └── practica-ut3-incidencias/
    │       └── README.md
    ├── UT4/
    │   ├── ejercicios.md
    │   └── practicas/
    │       └── README.md
    ├── UT5/
    │   ├── ejercicios.md
    │   └── practicas/
    │       └── README.md
    └── UT6/
        ├── ejercicios.md
        └── practicas/
            └── README.md
```

Puntos importantes:

* Cada unidad tendrá su propia carpeta.
* Dentro de cada unidad habrá un único `ejercicios.md` para recoger los mini ejercicios y ejercicios finales que aparezcan en `apuntes.md`.
* Cada práctica tendrá su propia carpeta de proyecto.
* La práctica 1 y la práctica 2 de la UT1 comparten el mismo proyecto: `ut1-entorno-web`.
* Cuando una práctica necesite reproducibilidad técnica, deberá incluir dentro de su carpeta los archivos necesarios para ejecutarse de forma autónoma, por ejemplo `compose.yaml`, `.env.example`, scripts de inicialización o una estructura equivalente bien documentada.

Por ejemplo, en la UT2 trabajarás normalmente en una de estas rutas:

```text
unidades/UT2/ejercicios.md
unidades/UT2/practica-1/
unidades/UT2/practica-2/
```

---

## 6. Forma de trabajo recomendada

Antes de empezar a trabajar en un bloque, asegúrate de estar en la rama principal y tener el repositorio actualizado:

```bash
git checkout main
git pull
```

Después, crea una rama nueva según el bloque que vayas a trabajar. Algunos ejemplos razonables son:

```bash
git checkout -b ut1-ejercicios
git checkout -b ut1-practica-entorno-web
git checkout -b ut2-practica-1-presupuesto
git checkout -b ut3-practica-2-incidencias
```

Trabaja en la carpeta o archivo correspondiente:

```text
unidades/UT1/ejercicios.md
unidades/UT1/ut1-entorno-web/
unidades/UT2/practica-1/
```

Si una rama ya existe porque vas a continuar trabajo anterior, no la crees otra vez. Entra directamente en ella:

```bash
git checkout ut2-practica-1-presupuesto
```

---

## 7. Hacer commits frecuentes

No subas todo el trabajo de golpe al final.

Haz commits pequeños cada vez que completes una parte:

```bash
git status
git add .
git commit -m "Completa mini ejercicios de formularios de UT2"
git push -u origin ut2-ejercicios
```

Ejemplos de buenos mensajes de commit:

```text
Completa ejercicios iniciales de UT1
Añade README y compose de la práctica de UT1
Implementa validación del formulario de presupuesto
Documenta prueba de aislamiento de la práctica 2 de UT2
Corrige DSN y filtro por estado de la práctica 2 de UT3
```

Ejemplos de malos mensajes de commit:

```text
cosas
final
cambios
arreglo
```

Un historial de commits razonable forma parte del trabajo. No se valorará igual una entrega construida poco a poco que una entrega subida completa en un único commit final.

---

## 8. Abrir una Pull Request

Cuando termines un bloque de trabajo, por ejemplo el `ejercicios.md` de una unidad o una práctica concreta:

1. Entra en GitHub.
2. Abre una **Pull Request** desde tu rama hacia `main`.
3. En la descripción indica qué bloque has completado, en qué ruta está y cómo se comprueba.
4. Indica si has usado IA y para qué.
5. No hagas merge hasta que el profesor lo indique.

La Pull Request permite al profesor ver los cambios realizados, revisar el código y dejar comentarios si es necesario.

Mientras la Pull Request esté abierta, el profesor podrá revisarla y pedir correcciones. Si eso ocurre, debes seguir trabajando en la misma rama, hacer nuevos commits y subirlos con `git push`; la Pull Request se actualizará sola. No la cierres ni hagas merge por tu cuenta salvo que el profesor te lo indique.

Si no tienes claro cómo abrirla exactamente o cuándo reutilizar una ya abierta, consulta [Tutorial previo: Git y GitHub para tu repositorio de entregas](git-github-entregas.md#57-abre-o-actualiza-una-pull-request).

---

## 9. Cómo documentar `ejercicios.md`

Cada unidad tendrá un archivo llamado:

```text
ejercicios.md
```

Debes usarlo para recoger los mini ejercicios y ejercicios finales que vayan apareciendo en `apuntes.md`.

Ese archivo debe dejar claro, como mínimo:

* qué ejercicios has resuelto;
* qué comandos, fragmentos de código o respuestas has usado;
* qué comprobaciones has hecho;
* qué dificultades has tenido;
* si has usado IA y para qué.

Una estructura sencilla y recomendable es esta:

```md
# Ejercicios de la UT2

## Mini ejercicios

### Ejercicio 1
Enunciado breve o referencia al apartado.

Solución o comandos usados.

### Ejercicio 2
...

## Ejercicios finales

### Ejercicio final 1
...

## Comprobaciones realizadas
- caso correcto
- caso con error

## Dificultades encontradas
- ...

## Uso de IA
- La he usado para ...
```

No hace falta escribir texto de relleno. Lo importante es que el documento permita seguir tu trabajo con claridad.

---

## 10. Qué debe incluir una práctica

Cada práctica debe entregarse dentro de su carpeta de proyecto y debe permitir al profesor entender rápidamente:

* qué archivos forman el proyecto;
* cómo se ejecuta;
* qué puerto o URL debe probar;
* qué credenciales o datos de prueba necesita, si procede;
* qué decisiones técnicas has tomado;
* qué evidencias mínimas demuestran que funciona.

Como norma general, cada práctica debe incluir:

* código fuente completo;
* `README.md` propio;
* capturas o evidencias cuando la práctica las pida;
* `compose.yaml` y `.env.example` cuando hagan falta para la reproducibilidad;
* cualquier archivo adicional imprescindible para arrancarla.

Si en el repositorio conviven varias aplicaciones web, cada una debe poder arrancarse desde su propia carpeta. Si dos prácticas usan Docker Compose, documenta en cada `README.md` qué puerto usa cada una.

---

## 11. Normas sobre el uso de IA

Puedes usar IA como apoyo para aprender, pero no para sustituir tu trabajo.

Puedes usar IA para:

* pedir una explicación;
* entender un error;
* comparar dos formas de resolver algo;
* pedir ejemplos parecidos;
* mejorar documentación;
* repasar conceptos;
* recibir pistas cuando estés bloqueado.

No debes usar IA para entregar código que no entiendes.

Normas obligatorias:

1. Debes entender todo el código que entregas.
2. Debes poder explicarlo oralmente o por escrito.
3. Debes indicar el uso de IA en `ejercicios.md` o en el `README.md` de la práctica correspondiente.
4. No se aceptará una entrega que no puedas modificar o explicar.
5. Es obligatorio mantener un historial de commits razonable.

Ejemplo aceptable:

```text
He usado IA para contrastar la validación de un formulario y para entender un error de sesión. Después he adaptado la solución y la he probado con varios casos.
```

Ejemplo no aceptable:

```text
Le he pedido a la IA que hiciera toda la práctica y he copiado el resultado sin revisarlo.
```

---

## 12. Defensa del trabajo

El profesor podrá pedirte en cualquier momento que expliques tu código, que modifiques una parte o que resuelvas una variante sencilla.

Una entrega no se considera válida si no puedes explicar razonablemente lo que has subido.

Por ejemplo, el profesor podrá pedirte que:

* expliques qué hace una variable concreta;
* cambies un mensaje mostrado por pantalla;
* añadas una comprobación adicional;
* modifiques un cálculo;
* corrijas un error;
* adaptes tu solución a un caso parecido.

---


