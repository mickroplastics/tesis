# Cifras del proyecto

Estado al 10 de noviembre de 2026. Esta tabla es la única fuente de números para el informe, las diapositivas y la demo. Si una cifra cambia, se cambia aquí primero.

Cada cifra lleva su tipo:

- **Hecho:** medido o leído en la fuente citada.
- **Estimación:** autorreportado o reconstruido.
- **Meta:** umbral acordado, no un resultado.

Las rutas cuelgan de la raíz del repositorio. `planificacion/` y `decisiones/` abrevian `archive/contexto/intento-actual/planificacion/` y `…/decisiones/`.

## 1. Metas del proyecto

| Cifra | Valor | Tipo | Fuente |
|---|---|---|---|
| Reducción del tiempo mediano de elaboración | al menos 40 % | Meta | Propuesta, objetivo 5 |
| Afirmaciones verificables respaldadas | al menos 90 % | Meta | Propuesta, objetivo 5; Tarea 1, sección 6.4 |
| Utilidad media según dos revisores externos | al menos 4 de 5 | Meta | Propuesta, objetivo 5; Tarea 1 |
| Fichas en inglés | al menos 6 | Meta | Propuesta, objetivo 4 |
| Videos publicados como piloto | 3 | Meta | Propuesta, objetivo 5 |
| Tope de inferencia | 30 USD al mes | Meta | `AGENTS.md`, "Alcance y criterios" |
| Puntaje de las dos alternativas de IA comparadas con ISO/IEC 25059 | arnés híbrido y modular 4,45 de 5; agente generalista 2,55 de 5 | Estimación previa del autor | Propuesta aprobada; `AGENTS.md`, "Estado del proyecto" |

## 2. Problema y línea base manual

| Cifra | Valor | Tipo | Fuente |
|---|---|---|---|
| Tiempo semanal de investigar y priorizar, según el fundador | más de 20 horas | Estimación | Propuesta, sección 2.2 |
| Registro de carga, semana del 1 al 7 de octubre | 14,2 horas en 6 días con registro | Estimación (reconstruida) | `planificacion/2026-10-31-registro-carga-manual-oct-2026.md`, "Agregados" |
| Registro de carga, semana del 8 al 14 de octubre | 16,1 horas en 6 días con registro, cota inferior | Hecho (cronometrada) | Mismo documento |
| Bloques de trabajo registrados | 17, en 12 de 14 días | Hecho | Mismo documento |
| Bloques que terminaron sin ficha ni guion | 7 de 17 | Hecho | Mismo documento, "Resultado de los bloques" |
| Mediana por bloque completo | 95 minutos | Mixto | Mismo documento |
| Costo de referencia de la búsqueda y escritura manual | 355 a 805 USD por semana | Estimación: 14,2 a 16,1 horas del registro por 25 a 50 USD la hora, que es la tarifa de referencia del tutor | `archive/output/entrega-final/informe-final.md`, capítulo de planificación y costos |
| Uso mensual de Earlyscript: una suscripción básica a un modelo de IA | unos 20 USD al mes | Estimación del autor; distinto de los pagos por API, que sumaron menos de 1 USD en el estudio | `archive/output/entrega-final/informe-final.md`, capítulo de planificación y costos, Tabla 6 |
| Suscriptores del canal en español al 2 de agosto | unos 7.200 | Estimación, sin captura fechada | Propuesta, sección 2.1 |

El registro mide solo búsqueda y escritura. No incluye grabación, edición ni comunidad. Cubre seis días con registro por semana y dos semanas concretas. La primera semana se reconstruyó después; la segunda se cronometró. Por eso **no confirma ni refuta** la estimación de 20 horas: el propio registro lo advierte.

## 3. Los seis pares: manual frente a asistido

Ejecutados por Miguel el 9 y 10 de noviembre de 2026 en Earlyscript. Fuente de toda la sección: `planificacion/2026-11-09-motor-v3/pares/resultados-v3.json`. Decisión y límites en `decisiones/2026-11-09-motor-v3-resultado.md`.

| Sesión | Manual (min) | Asistido (min) | Utilidad de Miguel, manual | Utilidad de Miguel, asistido |
|---|---:|---:|---:|---:|
| 1 | 30,00 (censurado; 49,6 observado) | 14,72 | 5 | 5 |
| 2 | 29,63 | 5,19 | 4 | 5 |
| 3 | 28,89 | 8,94 | 4 | 5 |
| 4 | 29,73 | 12,75 | 3 | 5 |
| 5 | 26,20 | 8,73 | 3 | 5 |
| 6 | 25,77 | 11,88 | 4 | 5 |

| Cifra | Valor | Tipo |
|---|---|---|
| Ejercicios | 12, en 6 pares | Hecho |
| Límite por ejercicio | 30 minutos | Hecho |
| Mediana del manual | 29,26 min, con un ejercicio censurado | Hecho |
| Mediana del asistido | 10,41 min | Hecho |
| Reducción de la mediana | 64,4 % | Hecho |
| Pares a favor del asistido | 6 de 6 | Hecho |
| Wilcoxon de rangos con signo, exacta | W+ 21, p bilateral 0,031 | Hecho |
| Utilidad media según Miguel | 3,83 manual; 5,00 asistido | Hecho, autovaloración no ciega |
| Decisiones | manual: 6 "editar"; asistido: 6 "aceptar" | Hecho |
| Afirmaciones con cita según el validador | manual 61 de 129 (47 %); asistido 193 de 206 (94 %) | Hecho |
| Temas que Miguel conocía total o parcialmente | 10 de 12 | Autodeclarado |

Tres cuidados al usar estas cifras:

1. El manual también se hizo dentro de Earlyscript. La reducción compara dos modos de la misma herramienta, no el asistido contra el proceso de octubre.
2. El validador cuenta si hay cita. No comprueba que la fuente respalde la afirmación.
3. Con seis pares, 6 de 6 es el único resultado que alcanza p menor que 0,05.
4. Es una comparación dentro de una misma persona. El operador es también el autor y el desarrollador del sistema.
5. Hubo incidencias que el informe debe declarar. En la sesión 1, Miguel vio la tarjeta y la evidencia del manual antes de empezar, y el asistido se reinició después de unos 4 minutos con un hilo que se borró. Dos hilos abiertos por error quedaron marcados como ensayo y no cuentan. Un motivo del asistido se dio fuera de la app. El detalle está en `decisiones/2026-11-09-motor-v3-resultado.md`, "Desviaciones e incidencias", y en `planificacion/2026-11-09-motor-v3/estado.md`.

## 4. Revisores externos

| Cifra | Valor | Tipo | Fuente |
|---|---|---|---|
| Revisores | 2: una persona con experiencia en contenido y un ingeniero de ML con experiencia en productos de software | Hecho | `decisiones/2026-11-09-motor-v3-resultado.md` |
| Fichas de calibración | 2, fuera de la evaluación | Hecho | `planificacion/2026-11-09-motor-v3/pares/calibracion/` |
| Diferencias de más de un punto en la calibración | 2, las dos en la misma ficha | Hecho | Libro `planificacion/2026-11-09-motor-v3/libro/ledger-v3.jsonl`, asiento `rubrica_congelada` |
| Guiones en revisión ciega | 12 | Hecho | `planificacion/2026-11-09-motor-v3/pares/ciega/` |
| Pares de afirmación y cita seleccionados para revisar | 3 por guion en 11 guiones, 33 en total, con semilla 20261109. Un guion manual no tiene citas. Los dos revisores las revisaron todas y la revisión está cerrada, con consenso | Hecho | `planificacion/2026-11-09-motor-v3/pares/muestra-citas-v3.json` |
| Utilidad externa media de los guiones asistidos | 2,92 de 5 (revisor A 2,83; revisor B 3,00) | Hecho | `planificacion/2026-11-09-motor-v3/pares/revision-externa-v3.json` |
| Utilidad externa media de los guiones manuales | 3,50 de 5 (revisor A 3,50; revisor B 3,50) | Hecho | Mismo archivo |
| Pares en que cada modo recibió mejor utilidad externa | manual 5, asistido 1 (sesión 1). Diferencia media de 0,58 puntos a favor del manual. Con seis pares no es concluyente: permutación exacta de signos, dos colas, p 0,125 | Hecho | Mismo archivo |
| Utilidad externa por par, asistido frente a manual (promedio de los dos revisores) | sesión 1: 2,0 y 1,5; sesión 2: 3,0 y 4,0; sesión 3: 3,0 y 4,0; sesión 4: 3,0 y 3,5; sesión 5: 3,5 y 4,0; sesión 6: 3,0 y 4,0 | Hecho | Mismo archivo |
| Meta de utilidad de 4 | No se alcanzó en ninguno de los dos modos | Hecho | Mismo archivo |
| Criterios, media asistido frente a manual | relevancia 4,00 y 3,92; respaldo 2,83 y 3,58; diferenciación 2,83 y 3,83; factibilidad 3,17 y 3,75; claridad 3,83 y 3,92 | Hecho | Mismo archivo |
| Acuerdo entre revisores en la utilidad | nota idéntica en 9 de 12 guiones; a un punto o menos en 12 de 12; alfa ordinal de Krippendorff 0,80 | Hecho | Mismo archivo |
| Citas de la muestra respaldadas, guiones asistidos (18) | 12 según los dos revisores (67 %); 14 según al menos uno (78 %) | Hecho | Mismo archivo |
| Citas de la muestra respaldadas, guiones manuales (15) | 14 según los dos revisores (93 %); 15 según al menos uno (100 %) | Hecho | Mismo archivo |
| Citas contradichas por su fuente | Ninguna tras el consenso. Antes, un revisor marcó una cita de un guion asistido como contradicha y el otro como parcial | Hecho | Mismo archivo |
| Acuerdo entre revisores en las citas | 29 de 33 por separado. Las cuatro en desacuerdo se resolvieron por consenso: las cuatro quedaron como respaldadas | Hecho | Mismo archivo |
| Citas respaldadas tras el consenso | asistido 15 de 18 (83 %); manual 15 de 15 (100 %). Las tres restantes del asistido son parciales | Hecho | Mismo archivo |
| Meta de respaldo del 90 % | No se alcanzó en el asistido (83 % de la muestra tras el consenso). Las citas de los guiones manuales sí la superan en la muestra (100 %), pero esos guiones citan menos de la mitad de sus afirmaciones | Hecho | Mismo archivo |
| Respaldo estimado sobre todas las afirmaciones (proporción citada por proporción respaldada en la muestra) | asistido 78 %; manual 47 %, con los veredictos tras el consenso | Estimación | Mismo archivo; cobertura del validador en la sección 3 |
| Aciertos al adivinar el origen | 13 de 24 (revisor A 7 de 12; revisor B 6 de 12). No se distingue del azar: binomial, dos colas, p 0,84. Los revisores dijeron "asistido" en 21 de 24 | Hecho | Mismo archivo |

Los dos revisores son amigos del autor. Se declara como posible sesgo.

**Cómo leer estas cifras.** El asistido tardó un 64 % menos (sección 3), pero los revisores externos valoraron mejor los guiones manuales. El operador valoró al revés: 5,00 el asistido y 3,83 el manual. La meta de utilidad de 4 no se alcanzó en ningún modo. La meta de respaldo del 90 % no se alcanzó en el asistido. El cegamiento funcionó: los revisores no distinguieron el origen. Lo que el informe puede decir es que el flujo asistido redujo el tiempo y que esa reducción vino con menor utilidad según dos revisores externos. No puede decir que el asistido produce guiones igual de útiles ni mejor respaldados.

**Límites de la revisión de citas.** La muestra se sacó de los pares de afirmación y cita que arma el validador. Incluye frases que no son afirmaciones verificables, como transiciones. El guion manual de la sesión 1 no tiene citas y no entra en la muestra. Los guiones manuales citan menos de la mitad de sus afirmaciones (47 %) y los asistidos casi todas (94 %); por eso la estimación sobre todas las afirmaciones favorece al asistido aunque sus citas se respalden menos.

**Desviación que el informe debe declarar.** La Tarea 1, sección 6.4, prometía identificar todas las afirmaciones verificables, comprobar su respaldo con dos revisores y resolver los desacuerdos por consenso. Lo ejecutado es una muestra de tres citas por guion. Una muestra da una estimación del respaldo. El consenso sobre las cuatro citas en desacuerdo se hizo por mensaje, a través del autor, y no en una reunión entre los dos revisores.

## 5. Motor de tendencias v3

Fuente de las cifras: `planificacion/2026-11-09-motor-v3/informes/resultados-desarrollo.md`. Kappa y acuerdo: `planificacion/2026-11-09-motor-v3/README.md`. Límites: `decisiones/2026-11-09-motor-v3-resultado.md`. Todas son mediciones retrospectivas sobre octubre de 2026, con jueces LLM.

"Soporte" es el número de cortes válidos comunes a los dos métodos comparados. Cambia de fila a fila y hay que citarlo.

| Cifra | Valor | Tipo |
|---|---|---|
| Periodo de desarrollo | 21 cortes, del 4 al 24 de octubre | Hecho |
| Acuerdo de los jueces LLM con Miguel en encaje temático | 58 de 60 tarjetas; kappa 0,870; acuerdo 0,967 | Hecho |
| Utilidad juzgada de la variante elegida (U@10) | 3,435 de 5, en 20 cortes válidos | Hecho, estimada por jueces LLM |
| Frente a la lista por palabras clave | +0,24, intervalo [−0,21; 0,67], soporte 20 | Hecho; no demuestra ventaja |
| Frente a `engine.v1`, el motor anterior | 3,435 frente a 3,07, soporte 20 | Hecho; diferencia descriptiva, sin intervalo |
| Frente a `engine.v2` | −0,21, soporte 20 | Hecho; v2 puntuó más alto |
| Frente a una regla trivial de regresión a la media | 3,496 frente a 2,509 en 14 cortes; +0,99, intervalo [0,50; 1,49] | Hecho. No usar 3,435 en esta comparación: es de otro soporte |
| Efecto de la tarjeta completa frente a la plana, con la misma lista | +0,30, medido sobre la variante V1; +0,15 sobre palabras clave | Hecho. No se midió sobre la variante elegida |
| Despegues captados | 8 de 50 en los 21 cortes; 4 a tiempo y 4 tarde | Hecho |
| Nota del consejo al contrato | 9,2; 9,5; 9,5; 9,5 | Hecho; califica el diseño, no el motor |

Límites que acompañan a estas cifras:

1. Los jueces se calibraron en encaje temático, de sí o no. Eso no valida su nota de utilidad de 1 a 5.
2. Es el tercer uso declarado de los datos de octubre.
3. Tres cosas cambiaron después de ver datos: la regla para combinar a los jueces, la limpieza de fechas y el perfil v2. Están declaradas en el libro.
4. No se puede decir que el motor anticipa tendencias ni que detecta señales débiles de forma demostrada.

### Comparaciones del 10 de noviembre, aparte del motor congelado

Las dos tienen la regla de decisión fijada antes de calcular. No cambian el motor de la entrega.

| Cifra | Valor | Tipo | Fuente |
|---|---|---|---|
| BERTopic frente a K-means sobre el corpus actual (2.614 publicaciones, vectores de Qwen, cinco semillas, cuatro grupos cada uno) | Empate según la regla. BERTopic gana en Davies-Bouldin (3,21 frente a 3,97) y en NPMI (0,184 frente a 0,075) y pierde en silueta (0,058 frente a 0,098). Se prefiere K-means por simplicidad | Hecho | `archive/contexto/intento-actual/planificacion/2026-11-10-comparaciones-finales/bertopic-kmeans.md` |
| Grupos que deja BERTopic con sus valores por defecto | 4, de los cuales 2 son cajones de 1.911 y 641 textos | Hecho | Mismo archivo |
| Agrupamiento propio del motor sobre la misma muestra | 445 temas | Hecho | Mismo archivo |
| Relevancia: AUC de text-embedding-3-large frente a Qwen3-Embedding-0.6B (11.381 titulares etiquetados por un juez LLM, cinco pliegues) | 0,969 frente a 0,938. Diferencia +0,031, intervalo [+0,027; +0,034] | Hecho | `archive/contexto/intento-actual/planificacion/2026-11-10-comparaciones-finales/embeddings.md` |
| Agrupamiento con uno u otro modelo de embeddings | Sin ganador claro | Hecho | Mismo archivo |
| Decisión sobre embeddings | La entrega mantiene Qwen, que corre en local y sin costo. Según la regla, text-embedding-3-large queda recomendado como opción para la relevancia; adoptarlo exige reentrenar, recalibrar y repetir la evaluación del motor | Hecho, decisión de Miguel del 10 de noviembre | Mismo archivo |
| Costo de la prueba con la API | 0,072 USD | Estimación: tokens medidos y tarifa de lista | Mismo archivo |
| Costo mensual de usar text-embedding-3-large | unos 0,21 USD | Estimación | Mismo archivo |

Límite: las etiquetas de relevancia son de un juez LLM, no de Miguel.

## 6. Intentos anteriores de mejorar el motor

| Cifra | Valor | Tipo | Fuente |
|---|---|---|---|
| Protocolo P2, candidato frente a referencia | 0,046 frente a 0,015; diferencia +0,031; resultado "no supera" | Hecho | `planificacion/2026-11-08-protocolo-p2/README.md`; decisión en `decisiones/2026-11-08-protocolo-p2-resultado.md` |
| Protocolo P2, diferencia mínima detectable | 0,140 | Hecho | Mismo documento |
| Protocolo P3, techo de la lista emitida | 0,21 frente a 0,40 exigido; cerró sin evaluar variantes | Hecho | `decisiones/2026-11-08-protocolo-p3-resultado.md` |
| Backtest de la versión anterior (Earlywindow v0.02) | P@5 0,95 frente a 1 de la línea base por volumen; anticipación mediana de 1 día | Hecho | `product.md`, sección 6; `archive/output/tareas/10-avance-consolidado.md` |

## 7. Datos del corte del 9 de noviembre

| Cifra | Valor | Tipo | Fuente |
|---|---|---|---|
| Corrida usada en los pares | `run_20261109_20261109T081813_457c97` | Hecho | `decisiones/2026-11-09-motor-v3-resultado.md` |
| Tarjetas mostradas | 15: 10 "En movimiento" y 5 "De fondo" | Hecho | Mismo documento |
| Fuentes agrupadas | 5: Hacker News, GitHub, Hugging Face, npm y RSS | Hecho | `config/engine.v3-sel.json` en Earlyscript, rama `es/motor-v3` |
| Publicaciones de los 35 días previos con vector | 36.808 | Hecho, contado al preparar el cuaderno | `archive/output/entrega-final/demo-motor-earlyscript.ipynb`, anexo |
| Muestra del cuaderno de Colab | 2.614 publicaciones, 445 temas | Hecho | Mismo cuaderno |
| Sonda de relevancia: titulares de entrenamiento | 11.381 | Hecho | `config/relevance.v2.json` en Earlyscript |
| Acuerdo del juez que etiquetó esos titulares con Miguel | 0,838; kappa 0,656 | Hecho | README de `packages/trend-engine` en Earlyscript |

## 8. Antecedentes del prototipo anterior, sobre X

Sirven como comparación de alternativas de IA. No describen Earlyscript.

| Cifra | Valor | Tipo | Fuente |
|---|---|---|---|
| Textos de X usados | 99; particiones 59, 20 y 20 | Hecho | `decisiones/tarea-05-resultados-preliminares.md` |
| Agrupamientos comparados | K-means 10, K-means 5 y BERTopic; cinco semillas | Hecho | `decisiones/tarea-06-ajustes-y-validacion.md` |
| Ensayo humano previo: asistidas | 170,1 y 130,3 segundos; utilidad 4 y 5 | Hecho | `AGENTS.md`, "Actualización de Tarea 6" |
| Ensayo humano previo: manuales | 296,0 segundos y una censurada a 300; utilidad 2 y 3 | Hecho | Mismo lugar |
| Fidelidad del sustituto usado con SHAP | 62 % | Hecho | `decisiones/tarea-07-interpretabilidad-y-etica.md` |

## 9. Cifras que faltan

1. Captura fechada de los suscriptores del canal.
2. Horas del autor en el proyecto y costo de las suscripciones de desarrollo: no están registrados. El capítulo de planificación y costos los informa como desconocidos.
