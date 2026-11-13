# Pitch de Earlyscript: guion de 5 minutos

Video que acompaña la entrega final y expone la tesis. Se graba con las diapositivas de la defensa en pantalla (`presentacion-defensa.pdf`) y la voz de Miguel; cámara opcional en una esquina. Unas 510 palabras: a ritmo tranquilo y con pausas entre diapositivas, entre 4 y 5 minutos.

Sigue la arquitectura narrativa de la clase de la semana 11 (`clases/semana-11/presentacion-s11-pmia.md`, diapositivas 16 a 19): problema, contexto, solución, resultados, aprendizajes e impacto. Gancho en los primeros 60 segundos y cierre con impacto. Cifras respaldadas en `base/03-cifras.md` y en el informe. No decir: "cuatro de cada cinco temas son útiles" ni que los modelos ya no inventan.

---

## 1. Gancho y problema · 0:00 a 1:00 · [Diapositivas 1 y 3]

¿De qué vale la pena hablar hoy? Esa pregunta abre cada video de SingulariDev, la comunidad que dirijo y que enseña inteligencia artificial aplicada.

Responderla tenía un costo. Durante dos semanas de octubre medí mi propio trabajo: buscar ideas, elegir una y escribir el guion me llevó 14,2 horas en una semana y 16,1 en la otra. Y no quedaba rastro: no podía explicar por qué elegí un tema ni de dónde salió cada dato.

Ese es el problema que resuelve esta tesis: menos horas para decidir y escribir, y una decisión que se pueda explicar.

## 2. Contexto · 1:00 a 1:30 · [Diapositiva 2]

SingulariDev la lleva una sola persona. Cada hora de investigación es una hora que no se dedica a enseñar. Y en inteligencia artificial los temas cambian cada semana: llegar tarde a una tendencia es perderla.

## 3. Solución y método · 1:30 a 2:45 · [Diapositivas 5, 6 y 7]

Construimos Earlyscript, una aplicación de escritorio con tres partes.

Primero, un motor de tendencias. Cada día lee cinco fuentes técnicas públicas, como Hacker News y GitHub, agrupa las publicaciones que hablan de lo mismo y mide qué temas se mueven y cuáles encajan con el canal. No usa un modelo de lenguaje para ordenar: siempre da el mismo resultado con los mismos datos.

Segundo, un asistente de IA que escribe el guion conmigo, con una cita a su fuente en cada dato.

Tercero, la decisión humana. Acepto, edito o rechazo cada guion, con una nota y un motivo, y la app guarda fuentes, versiones y tiempos.

No elegimos esta arquitectura a ciegas. La comparamos con un agente generalista: la nuestra obtuvo 4,45 sobre 5 y la otra 2,55. También comparamos dos formas de agrupar y dos modelos de representación del texto, y elegimos las opciones más simples que corren en la propia computadora, sin costo.

## 4. Resultados · 2:45 a 4:00 · [Diapositivas 10 y 11]

Lo evaluamos con seis pares de guiones: en cada par, un tema escrito a mano y otro con la herramienta.

El hallazgo principal: escribir un guion pasó de 29 minutos a 10, un 64 % menos. El modo asistido fue más rápido en los seis pares, y la diferencia es estadísticamente significativa.

El segundo hallazgo es la trazabilidad: en los guiones asistidos, el 94 % de las frases lleva su fuente; en los manuales, el 47 %. Y cada decisión queda registrada con su motivo.

Todo funcionó con menos de un dólar en pagos por uso, y el código tiene 1.181 pruebas automáticas.

## 5. Aprendizajes · 4:00 a 4:30 · [Diapositiva 13]

Qué aprendimos. Dos revisores externos leyeron los guiones sin saber su origen, y eso nos mostró el siguiente paso: darle al asistente una voz más propia, más cercana a la del creador. Ya tenemos el camino, con instrucciones de estilo para el modelo que redacta.

## 6. Impacto y cierre · 4:30 a 5:00 · [Diapositiva 13, o la portada]

Para SingulariDev, el impacto es directo: casi dos tercios menos de tiempo en cada guion, para dedicarlo a enseñar. Para quien aprende con nosotros, contenido más oportuno y con cada dato rastreable hasta su fuente.

Y como aporte profesional: un producto funcional, construido y evaluado por una sola persona en 14 semanas, con asistentes de IA para programar y con el código abierto.

Earlyscript no reemplaza al creador: le devuelve tiempo para crear. Gracias.

---

## Para grabar

- **No leas de corrido.** Ensaya tres veces, como pide la clase, y luego habla mirando las diapositivas; el texto es una guía.
- **Cómo:** pantalla con las diapositivas y tu voz (QuickTime o la grabación de Teams).
- **Ritmo:** si pasas de 5:15, recorta el último párrafo de "Solución y método" (las comparaciones de agrupamiento) o la frase del costo.
- **Archivo:** si pasa de 20 MB, súbelo como enlace sin listar y ponlo en el informe y en la diapositiva 12.
