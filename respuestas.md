# Respuestas — Taller Git Práctica 2

---

## Pregunta 1
**¿Qué sucede cuando hacemos un `git add`?**

### Respuesta
El fichero pasa del _working directory_ al _staging area_ (índice). Git toma una instantánea del estado actual del fichero y lo prepara para incluirlo en el próximo commit. No se guarda ningún historial todavía; simplemente se marca ese cambio como "listo para confirmar".

---

## Pregunta 2
**¿Qué sucede cuando hacemos un `git commit`? ¿Dónde está ese commit?**

### Respuesta
Git guarda permanentemente todos los cambios del staging area como un nuevo objeto en el repositorio **local** (dentro de `.git/objects`). El commit recibe un identificador único (hash SHA-1) y queda registrado en la rama local activa. Todavía no existe en ningún servidor remoto.

---

## Pregunta 3
**¿Por qué al hacer `git commit` todavía no está disponible ese commit en el repositorio remoto?**

### Respuesta
Porque `git commit` solo escribe en el repositorio local. El repositorio remoto (GitHub) es un servidor independiente. Git es un sistema de control de versiones distribuido: cada copia es autónoma y los cambios solo se sincronizan cuando se lo pedimos explícitamente mediante `git push`.

---

## Pregunta 4
**¿Qué hay que hacer para que veamos este commit en nuestro repositorio remoto de GitHub?**

### Respuesta
Ejecutar `git push`. Este comando envía los commits locales de la rama actual al repositorio remoto configurado (normalmente llamado `origin`). A partir de ese momento, el commit es visible en GitHub.

---

## Pregunta 5
**¿Qué diferencia hay entre hacer un fork o crear una nueva rama?**

### Respuesta
- **Fork**: crea una copia completa e independiente de un repositorio en otra cuenta de GitHub. Es útil para contribuir a proyectos ajenos sin tener permisos de escritura en el original.
- **Rama**: es una línea de desarrollo paralela dentro del mismo repositorio. Permite trabajar en nuevas funcionalidades sin afectar a la rama principal del mismo proyecto.

En resumen: el fork separa proyectos entre cuentas; la rama separa líneas de trabajo dentro del mismo proyecto.

---

## Pregunta 6
**¿Qué comando se utiliza para crear una nueva rama sin cambiarte a ella?**

### Respuesta
```bash
git branch nombre-de-la-rama
```
Para crear la rama y cambiarse a ella a la vez se usa `git checkout -b nombre-de-la-rama` o `git switch -c nombre-de-la-rama`.

---

## Pregunta 7
**¿Cuál es la diferencia entre los comandos `git switch` y `git checkout` al trabajar con ramas?**

### Respuesta
- `git checkout` es un comando multipropósito: cambia de rama, restaura ficheros del working directory, crea ramas con `-b`, etc. Su amplitud de funciones puede causar confusión.
- `git switch` (introducido en Git 2.23) está dedicado exclusivamente a cambiar de rama, lo que lo hace más claro e intuitivo. Para crear y cambiar a una rama nueva se usa `git switch -c nombre`.

Ambos realizan lo mismo al cambiar entre ramas, pero `git switch` es la opción moderna y recomendada.

---

## Pregunta 8
**¿Qué es una rama por defecto (como `main` o `master`) y por qué es importante?**

### Respuesta
Es la rama principal que se crea automáticamente al inicializar el repositorio. Representa el estado estable y productivo del proyecto. Es importante porque:
- Es el punto de referencia para el resto de ramas.
- Suele ser la versión que se despliega en producción.
- Las demás ramas se crean a partir de ella y se fusionan de vuelta cuando los cambios están listos.

---

## Pregunta 9
**¿Qué comando te permite ver la lista de todas las ramas locales de tu repositorio?**

### Respuesta
```bash
git branch
```
La rama activa aparece marcada con `*`. Para ver también las ramas remotas:
```bash
git branch -a
```

---

## Pregunta 10
**En el contexto de Git, explica con tus propias palabras qué es una rama (branch) y cuál es su beneficio principal al trabajar en un proyecto de software.**

### Respuesta
Una rama es un puntero ligero a un commit concreto que permite desarrollar de forma independiente sin afectar al resto del proyecto. Es como una "línea de tiempo alternativa" del código donde puedo hacer cambios, probar cosas y cometer errores sin romper lo que ya funciona.

Su beneficio principal es el **aislamiento**: varios desarrolladores pueden trabajar en paralelo en diferentes funcionalidades o correcciones, y fusionar los cambios a la rama principal solo cuando están listos y probados, sin interrumpir el trabajo de los demás.

---

## Pregunta 11
**¿Qué ha pasado con el contenido de la carpeta `practica-taller-git`? ¿Por qué no la podemos ver en nuestro repositorio remoto de GitHub?**

### Respuesta
La carpeta `practica-taller-git` fue creada con `git init`, lo que genera únicamente un repositorio **local**. A diferencia del repositorio `git-practica-2` (obtenido mediante `git clone`, que ya trae configurado el remoto `origin` automáticamente), `practica-taller-git` no tenía ningún repositorio remoto vinculado.

Para que sus commits sean visibles en GitHub fue necesario:
1. Crear manualmente un repositorio vacío en GitHub con el mismo nombre.
2. Vincular el remoto con `git remote add origin https://github.com/JaquelineCamarillo/practica-taller-git.git`.
3. Subir las ramas con `git push -u origin master` y `git push -u origin develop`.

Hasta que no se realizaron esos pasos, los commits solo existían en la máquina local y GitHub no tenía conocimiento de ellos.