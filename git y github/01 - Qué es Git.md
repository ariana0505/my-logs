# 01. ¿Qué es Git?

Git es una herramienta de **control de versiones**: guarda el historial de los cambios que registras en un proyecto. Te permite consultar qué cambió, comparar versiones y recuperar contenido anterior.

## 1. ¿Qué problema resuelve?

Imagina que estás creando una página web y guardas copias para conservar tus avances:

```text
pagina.html
pagina-final.html
pagina-final-2.html
pagina-final-ahora-si.html
```

Con Git puedes conservar el nombre `pagina.html` y registrar tus avances en el historial. Así evitas depender de muchas copias con nombres difíciles de distinguir.

## 2. ¿Cómo guarda esos avances?

Un **commit** registra una versión del proyecto junto con información sobre su autor y un mensaje que explica el cambio. Puedes imaginarlo como una fotografía del estado de los archivos que Git está siguiendo.

Por ejemplo, el historial podría contener:

```text
Primer commit:  "Crear la página principal"
Segundo commit: "Agregar el menú"
Tercer commit:  "Corregir el color del menú"
```

Git no convierte automáticamente cada edición o guardado de un archivo en un commit. Tú eliges qué cambios preparar y cuándo registrarlos. Más adelante veremos cómo hacerlo con `git add` y `git commit`.

## 3. ¿Qué es un repositorio?

Un **repositorio** almacena el historial y la información que Git necesita para controlar las versiones del proyecto.

En un proyecto local habitual, la carpeta de trabajo contiene tus archivos y una carpeta oculta llamada `.git`, donde Git guarda esa información:

```text
mi-proyecto/
├── .git/
├── pagina.html
└── estilos.css
```

No necesitas modificar manualmente la carpeta `.git` para usar Git.

## 4. ¿Para qué te sirve?

- **Consultar cambios:** revisar qué se modificó entre versiones registradas.
- **Recuperar contenido:** volver a consultar o restaurar archivos de un commit anterior.
- **Probar ideas:** trabajar en ramas separadas y combinar los cambios cuando estén listos.
- **Colaborar:** compartir el historial e integrar los aportes de otras personas.

Recuperar una versión anterior depende de que ese contenido haya quedado registrado. Git no puede garantizar la recuperación de cualquier cambio que nunca guardaste en su historial.

## 5. ¿Necesita internet?

Puedes crear commits, consultar el historial y trabajar con ramas en tu computadora sin conexión. Necesitas acceso al servidor cuando intercambias cambios con un repositorio remoto alojado en internet.

Git es **distribuido**: una clonación normal permite tener una copia local del historial disponible del repositorio y trabajar con ella.

## Idea principal

**Git te permite registrar versiones de tu proyecto y entender cómo fue cambiando.** Guardar un archivo conserva tu edición; crear un commit registra una versión en el historial de Git.

## Documentación

- [Introducción: ¿qué es Git?](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)
- [Tutorial de Git](https://git-scm.com/docs/gittutorial)
- [Manual de Git](https://git-scm.com/docs/user-manual)
