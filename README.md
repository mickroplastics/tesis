# Earlyscript: entrega final del proyecto de titulación

Este repositorio reúne los entregables públicos del proyecto de titulación **"Arnés agéntico basado en modelos de lenguaje y análisis semántico de tendencias para priorizar ideas de contenido en YouTube orientadas a la adquisición de miembros para SingulariDev"**.

- **Autor:** Miguel Ángel Brito Espejo.
- **Tutor:** Luis Fernando Aguas Bucheli, PhD(c).
- **Programa:** Maestría en Inteligencia Artificial Aplicada, Facultad de Ingeniería y Ciencias Aplicadas, Universidad de Las Américas, 2026.
- **Auspiciante:** Bistec LLC. Unidad de aplicación: SingulariDev.

Construimos Earlyscript, una aplicación de escritorio que cada mañana propone los temas que se mueven en comunidades técnicas públicas y acompaña la escritura del guion de un video, con la decisión final en manos del operador. En seis pares de ejercicios, el modo asistido redujo el tiempo mediano de escribir un guion de 29,26 a 10,41 minutos (64,4 % menos) y dejó registro de cada decisión. El informe cuenta el problema, la solución, la evaluación y lo que sigue.

## Código

El código de Earlyscript está en [github.com/mickroplastics/earlyscript](https://github.com/mickroplastics/earlyscript). Allí están las instrucciones para instalarlo y reproducir una corrida del motor. Dos etiquetas marcan las versiones citadas:

- [`entrega-final`](https://github.com/mickroplastics/earlyscript/tree/entrega-final): la versión entregada, con la interfaz mejorada después de la evaluación.
- [`motor-v3-pares`](https://github.com/mickroplastics/earlyscript/tree/motor-v3-pares): la versión evaluada en los seis pares; los resultados del informe corresponden a ella.

## Cómo navegar

| Carpeta | Contenido |
|---|---|
| [`informe/`](informe/) | [Informe final](informe/informe-final.md) en Markdown, con sus figuras. |
| [`presentacion/`](presentacion/) | Diapositivas de la defensa en [PDF](presentacion/presentacion.pdf), [notas del orador](presentacion/notas-del-orador.md), [guion](presentacion/guion.md) y una [hoja con todas las diapositivas](presentacion/hoja.png). En [`presentacion/html/`](presentacion/html/), la versión HTML con los videos de cada diapositiva. |
| [`pitch/`](pitch/) | [Guion del pitch presentado en clase](pitch/guion-pitch.md) y [guion del pitch en video](pitch/guion-video.md). |
| [`videos.md`](videos.md) | Enlaces a los videos en YouTube: pitch, demostración, exposición de la tesis y un video producido con Earlyscript. |
| [`cifras/`](cifras/) | [Tabla única de cifras](cifras/03-cifras.md) que usan el informe, las diapositivas y la demostración, con el tipo de cada cifra (hecho, estimación o meta). |
| [`notebook/`](notebook/) | [Cuaderno de demostración del motor](notebook/demo-motor-earlyscript.ipynb), ejecutable en Google Colab sin instalar nada. |
| [`capturas/`](capturas/) | Doce capturas de la aplicación entregada: Resultados, ficha de tendencia, hilo de video, primer arranque y Ajustes. |
| [`tareas/`](tareas/) | Entregas parciales del curso, de la 1 a la 10, en Markdown. |

## Cómo abrir la presentación HTML

1. Clona o descarga el repositorio. La presentación necesita la carpeta `clips/` a su lado, por eso no se ve desde la página de GitHub.
2. Abre `presentacion/html/presentacion.html` en Chrome o Edge. No necesita conexión.
3. Avanza con las flechas o la barra espaciadora. `F` activa la pantalla completa y `S` abre la vista del orador con las notas. Para saltar a una diapositiva, escribe su número y pulsa `Enter`.
4. Para ver todas las diapositivas una debajo de otra, abre `presentacion.html?apiladas`.

En la diapositiva 14, la demostración se abre en YouTube. Los demás clips son mudos y se repiten en bucle.

## Qué no está aquí

- **Nombres de usuario de terceros.** En las capturas, diapositivas y clips, los nombres de usuario de Hacker News, GitHub y Hugging Face aparecen difuminados o pixelados.
- **Datos personales y de terceros.** La carta de auspicio, los correos, las actas, las opiniones textuales de los revisores externos y la clave del cegamiento no se publican. En el cuaderno, los nombres de usuario de los autores de GitHub y Hugging Face se reemplazaron por seudónimos estables (`autor_0001`, `autor_0002`…). Los titulares y los enlaces públicos se conservan.
- **Base documental del proyecto.** El informe cita rutas como `planificacion/…` o `decisiones/…`. Pertenecen a la base documental privada del proyecto, que no se publica.
- **Figuras de las tareas.** Las tareas se publican como texto; sus figuras y sus PDF no se incluyen, por eso sus enlaces de imagen no se ven.
- **Corridas, corpus y modelos.** Viven fuera de Git. El repositorio de Earlyscript explica cómo generarlos.

## Licencia

Los textos de este repositorio no tienen una licencia declarada. El código de Earlyscript tiene la suya en su propio repositorio.
