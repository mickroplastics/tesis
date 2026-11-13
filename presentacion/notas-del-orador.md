# Notas del orador

Presentación final, ronda 8, 13 de noviembre de 2026. 23 diapositivas expuestas. Frases cortas, una por línea. Tiempo total hablado: 13:30, con la demo incluida.

## 1. Portada: «Earlyscript» y título aprobado

_Portada · 0:15_

Buenas noches.

Construí Earlyscript para que SingulariDev prepare guiones de video en inglés más rápido.

La meta era reducir el tiempo al menos un 40 %, con la persona siempre al mando.

## 2. SingulariDev explora el mercado en inglés

_Contexto · 0:30_

Bistec LLC tiene una comunidad que se llama SingulariDev.

Enseña, en español, a crear software y a hacerlo rentable con IA.

Hace videos en YouTube para atraer clientes a esa comunidad.

Ahora quiere explorar el mercado en inglés.

Y todo lo hace una sola persona: busca temas, escribe, graba y enseña.

## 3. Buscar y escribir a mano toma más de 14 horas por semana

_Problema · 0:35_

Primero medimos el trabajo a mano durante dos semanas.

Buscar temas y escribir tomó 14,2 horas en una semana y al menos 16,1 en la otra.

Y 7 de cada 17 sesiones de trabajo terminaron sin ningún guion.

Tampoco quedaba registro de por qué elegí cada tema.

## 4. Antes: pestañas y notas sueltas; cada salto de pantalla es tiempo muerto

_Problema: antes · 0:25_

Así trabajaba antes: muchas pestañas de noticias, una app de notas, post-its.

Cada salto de pantalla distrae.

Es tiempo muerto que podría usar en algo productivo.

## 5. Con Earlyscript, todo en una sola app

_Solución: después · 0:30_

Con Earlyscript todo está en una sola app.

Las tendencias ya vienen analizadas.

A la izquierda, el guion con sus citas.

A la derecha, la fuente abierta en el navegador integrado.

Puedo preguntarle al asistente y aprender del tema mientras escribo.

## 6. Tres metas: rapidez, respaldo y utilidad

_Objetivos y alcance · 0:35_

Nos pusimos tres metas.

Uno: reducir el tiempo de preparar un guion al menos un 40 %.

Dos: que 9 de cada 10 datos del guion estén respaldados por su fuente.

Tres: que dos revisores externos le den 4 de 5 en utilidad.

En esa escala, 1 es que no sirve, 3 que hay que rehacer mucho y 5 que está lista para decidir.

El sistema no publica, no genera videos y no predice ventas.

## 7. Del diagnóstico a la evaluación

_Objetivos específicos · 0:30_

Para llegar ahí nos pusimos cinco objetivos.

Uno: medir el proceso manual.

Dos: diseñar y justificar la solución.

Tres: construir un flujo reproducible de tendencias.

Cuatro: integrar el motor de tendencias con un agente de IA.

Cinco: evaluar el resultado frente al proceso manual.

No queremos automatizar la decisión. Queremos acelerar lo tedioso.

## 8. ¿Por qué no pedirle todo a un chatbot?

_Solución: alternativas · 0:40_

¿Por qué no usar solo ChatGPT?

Comparamos dos opciones: pedirle todo a un chatbot, o combinar un motor de tendencias, un asistente y la persona.

Calificamos cada una de 1 a 5 en ocho criterios de calidad de la norma ISO para IA.

Los que más pesan son tres: ver de dónde sale cada dato, obtener siempre el mismo resultado y que la persona tenga el control.

La combinación sacó 4,45. El chatbot, 2,55.

Es una estimación nuestra, hecha antes de construir.

## 9. Un motor propone, un asistente redacta y la persona decide

_Arquitectura · 0:35_

Así funciona, en tres piezas.

El motor de tendencias lee fuentes públicas: Hacker News, GitHub, Hugging Face, npm y blogs.

El usuario puede activar, desactivar o añadir fuentes.

El motor agrupa las publicaciones, mide qué se mueve y encuentra tendencias.

El asistente de IA redacta el guion con citas y conversa conmigo para buscar ángulos y aprender del tema.

Y yo decido, y anoto el motivo. Lo que se mide, se mejora.

## 10. El motor agrupa las noticias parecidas

_Arquitectura: motor por dentro · 0:25_

Ahora, el motor por dentro.

Primero, un modelo de embeddings, Qwen, convierte cada noticia en números, en la computadora.

En este mapa, cada punto es una noticia.

La distancia dice qué tan parecidas son: más cerca, más parecidas.

Cada color es un tema que el motor agrupó.

## 11. El motor detecta los temas que empiezan a crecer

_Arquitectura: motor por dentro · 0:35_

Segundo, el motor cuenta cuántas noticias tiene cada tema cada semana.

Un tema nuevo acaba de aparecer, como Copilot en JetBrains Air.

Un tema que vuelve a crecer había bajado y sube otra vez, como Kimi K3.1 Pro.

Esos dos son la oportunidad: temas que empiezan a ganar atención.

Un tema estable, como los agentes de programación, siempre está ahí.

La idea viene de BERTrend: juzgar un tema por cómo evoluciona.

## 12. Filtra por el perfil del canal y quedan las tendencias útiles

_Arquitectura: motor por dentro · 0:30_

Tercero, el motor mide cuánto le sirve cada tema al canal, de 0 a 1.

Usa el perfil del canal, que se escribe en texto al iniciar la app.

Así quedan pocas tendencias: el 9 de noviembre fueron quince.

Con los mismos datos sale siempre el mismo orden.

Así se puede revisar por qué cada tema quedó arriba.

## 13. Cada decisión guarda su motivo: lo que se mide se mejora

_Ética y control humano · 0:30_

La persona decide siempre: acepta, edita o rechaza el guion.

El asistente no puede registrar una decisión.

Cada decisión guarda una nota de utilidad y un motivo.

Así podemos medir con el tiempo qué tan bien trabajan el motor y el asistente.

Lo que se mide, se mejora.

Solo usamos fuentes públicas, y los datos se guardan en la computadora.

## 14. Del primer arranque al guion decidido, en una sola app

_Demostración · 2:15_

Ahora les muestro la aplicación.

Empezamos con una instalación limpia y el primer arranque.

Configuro el canal con unas líneas.

Leo las tendencias y elijo una.

Abro un guion asistido.

Converso con la IA, con la tendencia cargada y el navegador al lado.

Le pido otra estructura y aprendo del tema.

Y decido. La nota es opcional y sirve para mejorar.

## 15. Iteramos de la terminal a una app de escritorio

_Planificación: evolución · 0:30_

Earlyscript empezó como un prototipo en la terminal, sobre el agente Pi.

Leía publicaciones de X con su API, y era caro: hasta 0,55 USD por apenas cien publicaciones de prueba.

La terminal daba mucha fricción: copiar, pegar, cambiar de ventana.

Así que iteramos hasta una app de escritorio sobre T3 Code, de código abierto.

## 16. Construido en 14 semanas, cuesta unos 20 USD al mes

_Planificación y costos · 0:25_

Todo esto tomó catorce semanas: diseño, construcción y evaluación.

Estimo que usarlo cuesta unos 20 dólares al mes: una suscripción básica a un modelo de IA.

Durante el estudio, los pagos por API no llegaron a un dólar.

## 17. El modo asistido redujo un 64 % el tiempo por guion

_Resultados · 0:40_

Ahora, los resultados.

Hicimos seis pares de temas sorteados: uno a mano y otro en modo asistido.

El modo asistido fue más rápido en los seis.

La mediana bajó de 29,3 a 10,4 minutos: un 64 % menos.

La meta era 40 %.

Con seis pares, ganarlos todos da significancia: Wilcoxon exacta, p 0,031.

## 18. El 94 % de las frases asistidas lleva su fuente

_Resultados · 0:30_

El segundo hallazgo es la trazabilidad.

En los guiones asistidos, 193 de 206 frases llevan una cita a su fuente: el 94 %.

En los manuales, 61 de 129: el 47 %.

Abajo vemos una frase del guion real con sus números de cita. Cada número abre la publicación citada.

Sirve para rastrear de dónde vino lo que digo, leer la noticia original o ver si sigue vigente.

## 19. Los revisores ciegos marcan el siguiente paso: darle al asistente una voz propia

_Resultados · 0:35_

Para medir la calidad hicimos una revisión ciega.

Dos revisores externos leyeron los doce guiones sin saber cuál era a mano y cuál asistido.

Calificaron la utilidad de cada guion de 1 a 5.

En utilidad, los guiones a mano recibieron 3,50 frente a 2,92 del asistido. La meta era 4.

Creemos que viene del estilo genérico del modelo que redacta.

Por eso el siguiente paso es claro: instrucciones de estilo con la voz del creador.

## 20. Lo que aprendí del desarrollo de software

_Cierre: aprendizaje · 0:30_

Yo venía de la producción audiovisual, no de la programación.

Con este proyecto aprendí el ciclo de vida completo del software.

Integración continua: cada cambio se prueba antes de entrar.

El producto pasa 1.181 pruebas automáticas.

Aprendí a orquestar agentes y subagentes en paralelo, y a repartir el trabajo entre ellos.

Y a trabajar con Git y GitHub.

## 21. Recomendaciones y trabajo futuro

_Cierre: trabajo futuro · 0:25_

Lo que sigue tiene tres partes.

Uno: instrucciones de estilo para que el asistente escriba con la voz del creador.

Dos: seguir mejorando la interfaz con datos de uso.

Tres: un nuevo estudio con más creadores y más guiones, porque este fue con una persona y seis pares de temas.

## 22. Siguiente paso: del guion al video

_Cierre: siguiente paso · 0:30_

¿Por qué quedarnos en el guion?

Los asistentes de IA ya pueden producir el video completo.

El video de producto de Earlyscript lo hizo un asistente de código, Claude Opus en T3 Code, la misma base de la que deriva Earlyscript.

Usó Remotion para escribir el video con código, ElevenLabs para mi voz clonada, una grabación automática de la app y ffmpeg para montarlo.

La tesis dejó fuera generar videos. Ese es el siguiente paso natural: del guion al video.

## 23. Un entorno de trabajo integrado para crear guiones

_Cierre · 0:35_

Para cerrar.

Earlyscript es un entorno de trabajo integrado para crear guiones.

Es más rápido: un 64 % menos de tiempo.

Cada guion llega con sus fuentes: sabes de dónde sale lo que vas a decir.

Conversas con el asistente y aprendes del tema.

Y estimo que usarlo cuesta unos 20 dólares al mes.

Cumplimos los objetivos 1 a 3, y el 4 y el 5 parcialmente.

Earlyscript no reemplaza al creador: le devuelve tiempo para crear. Gracias.
