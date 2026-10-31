---
title: "Arnés agéntico basado en modelos de lenguaje y análisis semántico de tendencias para priorizar ideas de contenido en YouTube orientadas a la adquisición de miembros para SingulariDev"
author: "Miguel Ángel Brito Espejo"
guide: "Luis Fernando Aguas Bucheli"
date: "30 de octubre de 2026"
version: "Avance consolidado S10, versión 5 del 30 de octubre de 2026"
---

# Resumen

SingulariDev, unidad de Bistec LLC, busca atraer desde YouTube a emprendedores unipersonales angloparlantes interesados en agentes de inteligencia artificial. Su fundador investiga y prioriza ideas de video a mano, estima esa carga en más de 20 horas semanales y no conserva un registro que una señales, evidencia y decisiones. El proyecto desarrolla y valida un arnés agéntico con aprobación humana que separa cuatro responsabilidades: adaptadores de solo lectura que capturan historias de Hacker News y repositorios de GitHub con su procedencia; un motor determinista, sin modelo de lenguaje, que agrupa los textos con Qwen3-Embedding-0.6B en CPU y emite fichas de tendencia con crecimiento, afinidad con el perfil del canal, dos rankings y evidencia enlazada; un asistente que solo lee y redacta, con títulos y resúmenes citados; y una decisión del operador registrada con utilidad, motivo y tiempos por etapa. El prototipo, Earlyscript, es un fork de T3 Code, un estudio de agentes de código con licencia MIT, al que se añaden un espacio de Tendencias, hilos de video con guion versionado y validado, y un espacio de Resultados. Una matriz con criterios de ISO/IEC 25059:2023 justificó esta arquitectura frente a un agente generalista, con 4,45 frente a 2,55 sobre 5. El motor se evaluó sobre 50.462 ítems: en una prueba retrospectiva de cuatro cortes, la fórmula ponderada obtuvo una precisión de 0,95 entre las cinco primeras candidatas frente a 1,00 de una línea base por volumen, con una mediana de un día hasta el evento, así que avisar una o dos semanas antes no queda respaldado; el orden resistió cambios de pesos y fue sensible al umbral de agrupamiento. Sobre publicaciones de X, K-means quedó como opción provisional frente a BERTopic. Una corrida reciente sobre 28 días emitió 15 fichas en seis minutos y se reproduce por huella. La reducción de tiempo del 40 %, el respaldo factual del 90 % y la utilidad según revisores externos siguen sin medirse: el protocolo de seis pares está propuesto y los ejercicios empiezan en noviembre.

**Palabras clave:** arnés agéntico, modelos de lenguaje, detección de tendencias, priorización editorial, trazabilidad.

# Abstract

SingulariDev, a unit of Bistec LLC, aims to reach English-speaking solo entrepreneurs interested in artificial intelligence agents through YouTube. Its founder researches and prioritizes video ideas by hand, estimates that workload at more than 20 hours per week, and keeps no record linking signals, evidence, and decisions. The project develops and validates an agentic harness with human approval that separates four responsibilities: read-only adapters that capture Hacker News stories and GitHub repositories with their provenance; a deterministic engine, without a language model, that clusters texts with Qwen3-Embedding-0.6B on CPU, computes growth and affinity with the channel profile, and emits trend briefs with two rankings and linked evidence; an assistant that only reads and writes, producing cited titles and summaries; and an operator decision recorded with usefulness, reason, and time per stage. The prototype, Earlyscript, is a fork of T3 Code, an MIT-licensed coding-agent studio, extended with a Trends space, video threads with a versioned and validated script, and a Results space. A matrix based on ISO/IEC 25059:2023 justified this architecture over a generalist agent, scoring 4.45 versus 2.55 out of 5. The engine was evaluated in an earlier version of the prototype over 50,462 items: in a four-cutoff retrospective test, the weighted formula reached a precision of 0.95 among the top five candidates against 1.00 for a volume baseline, with a median of one day until the event, so the hypothesis of a one-to-two-week early warning is not supported; the ranking resisted weight changes and was sensitive to the clustering threshold. On X posts, K-means remained a provisional option over BERTopic. A recent run over 28 days produced 15 briefs in six minutes and is reproducible by hash. The 40 % time reduction, the 90 % factual support, and usefulness rated by external reviewers remain unmeasured: the six-pair protocol is proposed and the exercises start in November.

**Keywords:** agentic harness, language models, trend detection, editorial prioritization, traceability.

# Introducción

Este avance describe el proyecto en su estado al 31 de octubre de 2026 y sigue el formato del informe final. Lo que falta se marca **[PENDIENTE: …]** y se reúne en el capítulo 9. Se distingue **Hecho** (medido o leído en una fuente), **Estimación** (un cálculo), **Supuesto** (una condición de diseño) e **Hipótesis** (una afirmación pendiente de prueba). Lo que existe en una rama sin fusionar se declara así.

**Qué cambió desde el borrador de la Tarea 8.** Tres cosas. El corpus pasó de X y Reddit a Hacker News y GitHub, porque el lote pagado de X no permitía medir tendencias semanales y Reddit no tenía autorización (7.1). El motor de tendencias se construyó, se evaluó con una prueba retrospectiva y pruebas de robustez, y se portó a una plataforma nueva. Y el producto dejó de ser una aplicación de escritorio propia (Earlywindow) para construirse sobre T3 Code, porque esa base ya resuelve hilos, proveedores de modelos, historial y visor de diferencias con más calidad de la que el proyecto podía mantener (7.2). Los dos primeros cambios y el tercero deben comunicarse al tutor; su registro está en el Anexo 3.

## Identificación y descripción del problema o necesidad

El fundador de SingulariDev busca ideas de video, decide cuáles investigar, lee, compara, escribe un guion y decide si graba. Lo hace solo y estima que investigar y priorizar le toma más de 20 horas semanales (Brito Espejo, 2026). Es una estimación. Hecho declarado por el autor: existe un registro de dos semanas del proceso manual, con la búsqueda y la escritura separadas y el resultado de cada idea, reconstruido a partir del 1 de octubre; este avance no incorpora sus cifras porque no se verificaron todavía, y se integrará como reconstrucción, no como registro en el momento. Además, no consta qué señal llevó a cada idea, con qué criterio se filtró ni por qué se grabó, y YouTube Analytics no se conecta con la decisión que originó el video. La Figura 1 marca tres puntos donde probablemente se pierde el rastro.

**Figura 1**

*Proceso manual de investigación y selección de ideas*

![Nota. Reconstrucción documental a partir de la Tarea 1; los recuadros rojos marcan los posibles puntos de pérdida de trazabilidad. Pendiente de validar con el operador.](archive/output/tareas/evidencias-tarea-08/figura-1-proceso-manual.png)

Las causas son hipótesis: señales repartidas entre fuentes, criterios editoriales no escritos, una sola persona que investiga y produce, y fuentes que cambian cuotas y términos. La falta de miembros no es el problema que se ataca, porque depende también del video, la oferta y el precio. Al ser una necesidad de la organización y no la falla de un sistema, se analiza con un FODA (Tabla 1), aceptado por el Comité (*Reporte ejecutivo de evaluación de proyecto*, 2026).

**Tabla 1**

*FODA de SingulariDev (Brito Espejo, 2026, §2.3)*

| | Interno | Externo |
|---|---|---|
| **Favorable** | Canal propio con unos 7.200 suscriptores al 2 de agosto de 2026 y acceso a sus métricas. Experiencia del fundador en software, IA y contenido. | APIs y datos públicos con historial. Un segmento angloparlante nuevo de emprendedores unipersonales. Modelos de lenguaje con herramientas para sintetizar evidencia. |
| **Desfavorable** | Operación individual con más de 20 horas semanales estimadas. Audiencia histórica en español y comunidad inglesa sin historial. Criterios manuales sin registro. | Cambios de cuotas, precios y términos de las fuentes. Sesgo, saturación y variación rápida de los temas. Alucinación del modelo y dependencia del proveedor. |

La asistencia generativa redujo un 40 % el tiempo de escritura profesional (Noy y Zhang, 2023), pero preparar una idea también exige buscar y seleccionar, y en 640 emprendedores no tuvo un efecto promedio concluyente (Otis et al., 2026). Una conversación con un modelo tampoco registra fuentes, criterios ni decisiones. La necesidad es doble: menos tiempo y más trazabilidad, sin delegar la decisión. La propuesta fija seis requerimientos: decisión humana registrada con motivo y fecha; afirmaciones rastreables hasta su fuente; guiones en inglés; solo datos autorizados; inferencia de hasta 30 USD mensuales; y tiempo y calidad medibles frente al proceso manual. **[PENDIENTE: validar la Figura 1 con el operador y pasarla a BPMN; integrar y verificar el registro de dos semanas; captura fechada de YouTube Analytics.]**

## Descripción de la organización

Bistec LLC, sociedad de responsabilidad limitada de Wyoming, Estados Unidos, dedicada a software y productos digitales, auspicia el proyecto (Anexo 1). SingulariDev es su unidad de formación y comunidad en línea sobre IA aplicada, y Miguel Ángel Brito Espejo representa a ambas. No hay misión ni visión formales; el propósito, según la propuesta, es atraer desde YouTube a emprendedores unipersonales angloparlantes hacia una comunidad en Skool. Una persona cumple cuatro funciones (Figura 2); la necesidad ocurre en la de investigación y planificación editorial. El canal Miguelito Hacks tiene audiencia mayoritariamente hispanohablante; el piloto de tres videos en inglés no tiene evidencia de publicación y la comunidad en Skool no tiene historial. La validación se acota a contenido para programadores en inglés. El producto se desarrolla con un solo código para la tesis y su uso posterior, con Bistec LLC como titular; su modelo de negocio queda fuera del proyecto. **[PENDIENTE: sector formal registrado; misión y visión; estado de la comunidad.]**

**Figura 2**

*Organigrama funcional de SingulariDev*

![Nota. Reconstrucción funcional a partir de la propuesta; una persona cumple las cuatro funciones.](archive/output/tareas/evidencias-tarea-08/figura-2-organigrama-funcional.png)

# Análisis de posibles soluciones

## Identificación y selección de la mejor solución

Las dos alternativas usan modelos de lenguaje y difieren en dónde se calcula la prioridad y cuánto control conserva el operador. En la **alternativa A, agente generalista**, un agente con herramientas consulta fuentes, interpreta señales y redacta; se construye rápido, pero su priorización queda implícita y puede cambiar entre ejecuciones. La **alternativa B, arnés híbrido y modular**, separa adaptadores, almacén de evidencia, análisis determinista y generación: la puntuación se recalcula desde datos y pesos registrados, y el operador acepta, edita o rechaza cada pieza. La Tabla 2 las compara con ocho características de ISO/IEC 25059:2023, el modelo de calidad para sistemas de IA que extiende ISO/IEC 25010 (International Organization for Standardization [ISO] e International Electrotechnical Commission [IEC], 2023). Es una estimación previa del autor, de 1 (sin mecanismo claro) a 5 (cobertura explícita y verificable).

**Tabla 2**

*Matriz de selección (Brito Espejo, 2026, §6.4)*

| Criterio ISO/IEC 25059 | Peso | A | B |
|---|---:|---:|---:|
| Transparencia y procedencia | 20 % | 2 | 5 |
| Corrección funcional y reproducibilidad | 20 % | 2 | 4 |
| Controlabilidad del usuario | 15 % | 3 | 5 |
| Robustez ante fallos | 15 % | 2 | 4 |
| Adaptabilidad funcional | 10 % | 4 | 4 |
| Intervenibilidad | 10 % | 3 | 5 |
| Riesgos sociales y éticos | 5 % | 2 | 4 |
| Mantenibilidad e integración | 5 % | 4 | 4 |
| **Total ponderado** | **100 %** | **2,55** | **4,45** |

Se eligió B. Earlyscript la materializa: el motor no usa modelo de lenguaje, el asistente solo lee y redacta, y la decisión se graba por un camino que el modelo no puede invocar (7.2). Se parece en superficie a la alternativa A, porque el operador conversa con un agente en un hilo; la diferencia es que la prioridad la calcula el motor con pesos registrados, el agente no puntúa ni reordena y cada guion es un archivo con versiones y citas verificables. No se construyó A para compararla sobre las mismas tareas; dentro de B se compararon las alternativas técnicas de la Tabla 3. **[PENDIENTE: tabla complementaria de viabilidad, costo, innovación, impacto y tiempo que pide la guía del tutor, si confirma que complementa la matriz aprobada.]**

**Tabla 3**

*Alternativas técnicas comparadas dentro de la solución*

| Comparación | Qué se fija | Resultado | Alcance |
|---|---|---|---|
| BERTopic frente a K-means | Mismos 79 textos de X, embeddings y UMAP por semilla | K-means 5 provisional; BERTopic sin la cobertura de agrupamiento mínima (7.3) | Evidencia sobre X, anterior al motor |
| Fórmula ponderada frente a orden por volumen `items_7d` | Mismas candidatas, cortes y etiqueta | La línea base gana o empata en los cuatro cortes (7.3) | Dos órdenes de las mismas señales, no dos sistemas |
| Qwen3-Embedding-0.6B local frente a text-embedding-3-large | Mismos textos y algoritmos | No ejecutada: exigía gasto y clave (Anexo 3) | No demuestra superioridad ni equivalencia |
| Motor en macOS frente al mismo motor portado en Linux | Mismo corpus, corte y perfil; 45.557 textos | 19 fichas frente a 18; coinciden 3 de 5 en el top 5 por volumen. Hipótesis: los vectores de Qwen difieren entre plataformas (coseno mediano 0,965) | Mismo método en dos plataformas |

## Impacto del proyecto en la sociedad

Los impactos son esperados, no observados. Económico: reducir el esfuerzo del único operador. Social: investigar con evidencia enlazada, con riesgo de amplificar anuncios de grandes proveedores (7.4). Tecnológico: integra técnicas existentes y no aporta un algoritmo nuevo; el fork devuelve a un proyecto de código abierto un caso de uso editorial. Legal: los textos de terceros están sujetos a los términos de cada fuente y a la protección de datos (Ley Orgánica de Protección de Datos Personales, 2021). Ambiental: no se midió energía. No se identificó un efecto político directo. **[PENDIENTE: lugar de operación y obligaciones legales por tratamiento; respuesta de Y Combinator sobre uso comercial.]**

# Objetivos

Los objetivos conservan las metas de la Tarea 1; el objetivo 3 incorpora la comparación de embeddings de la Tarea 3. Su estado está en el capítulo 8.

## Objetivo General

Desarrollar y validar, entre agosto y noviembre de 2026, un arnés agéntico con aprobación humana que reduzca al menos 40 % el tiempo mediano de preparación de guiones en inglés para SingulariDev. La meta no se ha alcanzado ni medido al corte.

## Objetivos Específicos

1. Caracterizar el proceso manual de investigación y selección de ideas mediante un diagrama del flujo actual, un registro de carga de al menos dos semanas y seis fichas manuales, para sustituir la estimación de 20 horas semanales por una línea base observada.
2. Diseñar la arquitectura, los permisos y los criterios de aceptación del arnés, y documentar la comparación previa de dos alternativas con criterios de ISO/IEC 25059:2023, para justificar la solución seleccionada.
3. Implementar un flujo reproducible que recolecte evidencia de fuentes autorizadas con su procedencia y compare BERTopic con K-means, y Qwen3-Embedding-0.6B con text-embedding-3-large, sobre los mismos textos, para elegir el agrupamiento con métricas registradas.
4. Integrar un agente de código con herramientas acotadas y una interfaz gráfica para generar al menos seis fichas en inglés con evidencia, registrar cada decisión humana con su motivo y demostrar una personalización reversible.
5. Evaluar el prototipo frente al proceso manual con seis pares de temas y dos revisores externos ciegos, para determinar si alcanza 40 % de reducción del tiempo mediano, 90 % de respaldo factual y utilidad media de 4 sobre 5, y publicar tres videos cuyos resultados se reporten sin atribución causal.

La utilidad usa las anclas de la Tarea 1: 1, no utilizable; 2, cambios mayores; 3, revisión sustancial; 4, cambios menores; 5, lista para decidir. La meta se calcula con los dos revisores externos y la valoración del autor se informa aparte. El tiempo de la meta es el tiempo activo desde el inicio de la búsqueda hasta la decisión; el prototipo lo mide por etapas (explorar, leer, escribir, decidir) con un reloj con pausa (7.2). El objetivo 4 nombraba a Pi coding agent; el prototipo usa los agentes de T3 Code, desviación registrada en el Anexo 3. **[PENDIENTE: calibrar la rúbrica con los revisores; respuesta del tutor sobre las desviaciones de los objetivos 3, 4 y 5.]**

# Alcance

## Alcance de la solución seleccionada

**Qué aborda.** Los cinco objetivos, con la retrospectiva y la robustez del motor como evidencia técnica añadida. **Fuentes.** Hacker News y GitHub, capturadas en vivo por día; el corpus congelado de evaluación cubre del 30 de agosto al 18 de octubre de 2026 y el corpus reciente del 3 al 30 de octubre. X queda como evidencia histórica (99 publicaciones); Reddit y YouTube no se usaron. **Plataforma.** Fork de T3 Code: servidor Node e interfaz web, empaquetable como aplicación de escritorio para macOS y Linux; base propia `editorial.sqlite`; agentes de código instalados en la máquina del operador (Claude Code, Codex). **Unidad de trabajo.** Ficha de tendencia de lectura y guion de video como archivo Markdown con versiones y citas. **Medición.** Reloj por etapas con pausa, decisión con utilidad y motivo, y espacio Resultados descriptivo.

**Qué no aborda.** Publicación autónoma; generación final de videos o imágenes; CRM, facturación, multiusuario o modelo de negocio; predicción de conversión, abandono o valor de vida del cliente; aprendizaje de pesos por retroalimentación; comentarios, transcripciones y otros idiomas; atribución causal de resultados comerciales; las funciones de T3 Code ajenas al estudio (terminal, solicitudes de cambio, proveedores de control de versiones en la nube, acceso remoto, relay), escondidas por banderas y no borradas.

**Supuestos.** La cercanía entre embeddings refleja temas útiles, sin evaluación humana en el corpus nuevo. Hacker News y GitHub siguen sin tarifa, y la gratuidad no acredita permiso para todo tratamiento. Los agentes de código instalados siguen disponibles con la suscripción del operador. Habrá dos revisores calibrados.

**Periodicidad.** La corrida es diaria por diseño: existe la captura idempotente por día y la corrida con corte; el programador nocturno no está iniciado.

## Limitaciones y restricciones del proyecto

**Limitaciones del entorno.** La comunidad en inglés no tiene historial, así que los resultados comerciales solo se reportan de forma descriptiva. X cobra cada lectura y su lote pagado no permite evaluar tendencias semanales. Reddit no tiene autorización documentada. Y Combinator restringe el uso comercial del contenido (Y Combinator, s. f.), así que Hacker News se limita a la evaluación local. GitHub solo ofrece estrellas actuales. Hecho: el 91,49 % de las historias de Hacker News no tiene cuerpo. Los vectores de Qwen no reproducen entre macOS y Linux (coseno mediano 0,965 para el mismo texto), así que los resultados medidos en una plataforma no se trasladan sin repetirlos. No hay un banco de pruebas para anticipar temas editoriales: BERTrend se validó con casos (Boutaleb et al., 2024) y BackTrend cubre señales científicas (Zhou et al., 2026). Sin dos revisores, la utilidad externa no es evaluable.

**Restricciones del proyecto.** Periodo del 10 de agosto al 15 de noviembre de 2026. Un integrante que desarrolla, opera y es evaluado, mitigado con revisores ciegos. Hasta 30 USD mensuales de inferencia, aparte de X. Aprobación humana antes de usar un guion (Tabassi, 2023). El producto corre en local; la interfaz editorial está en español porque el operador la usa en español, y los guiones se escriben en inglés. Sin credenciales, corpus ni opiniones de revisores en Git. Orden del autor: gana la opción con menos código y un compromiso incumplido se registra como desviación. Hecho: el corpus congelado ocupa 161.681.858 bytes; una corrida completa tarda 305 segundos con caché en una Mac Apple M4 y 374 segundos en un servidor Linux de 22 núcleos con seis procesos de embeddings.

# Planificación y costos del proyecto

Iteraciones semanales con un incremento verificable por entrega: entregable, decisiones fechadas y commit. Desde el 21 de octubre el trabajo técnico se organiza en unidades con prueba observable, delegadas a agentes de programación: un modelo implementa en una rama con batería de pruebas, un segundo modelo verifica en solo lectura y emite un veredicto, el primero corrige y el autor o su coordinador fusiona; cada decisión tomada en ausencia del autor queda registrada y es reversible. No se usó Scrum ni Kanban formal (Tabla 4).

**Tabla 4**

*Cronograma de 14 semanas, previsto en la Tarea 1 y real al 31 de octubre*

| Semanas de 2026 | Previsto | Real al 31 de octubre |
|---|---|---|
| 1 (10 a 16 ago.) | Observaciones del Comité e instrumentos | Hecho (Tarea 1) |
| 2 a 5 (17 ago. a 13 sep.) | Credenciales, fuentes, línea base manual; arquitectura | Arquitectura hecha (Tarea 3); línea base manual sin integrar |
| 6 a 8 (14 sep. a 4 oct.) | Recolección; agrupamiento; puntuación; revisores | Con retraso: X el 29 de sep.; ranking provisional; revisores sin identificar |
| 9 a 10 (5 a 18 oct.) | Agente, interfaz, fichas; videos 1 y 2 | Parcial: Tareas 6 y 7; videos sin verificar |
| 11 (19 a 25 oct.) | Prueba ciega; video 3 | Rediseño: motor de tendencias, retrospectiva, robustez, seguridad y calidad (Earlywindow) |
| 12 (26 oct. a 1 nov.) | Análisis y corrección | Verificación del motor; traslado del entorno a Linux; fork de T3 Code y diez unidades fusionadas; S10. Ejercicios sin iniciar |
| 13 a 14 (2 a 15 nov.) | Prototipo reproducible, informe y defensa | **[PENDIENTE: corte del 5 de nov. con un ejercicio completo con modelo real; sesiones de ejercicios; revisores; integración del registro de dos semanas; informe final; defensa probable el 13]** |

Ni el motor ni el fork estaban en el cronograma: el motor respondió a que el lote de X no permitía medir tendencias y a que el ranking de la Tarea 5 no medía relevancia; el fork, a que la aplicación propia repetía con menos calidad lo que T3 Code ya resuelve y a que el autor quiere un producto que use después. La evaluación humana, los revisores y los videos son la deuda principal. **[PENDIENTE: cierres de Brightspace de S11 y S12.]**

**Costos.** Un costo desconocido se informa como desconocido, no como cero. API de X: hasta 0,55 USD por 100 publicaciones más una prueba de 10 (Estimación, sin factura). Hacker News, GitHub y embeddings locales: sin tarifa por solicitud (Hecho; sin contar equipo ni energía). Modelo de lenguaje: por la suscripción del operador a los agentes instalados, sin precio por solicitud; los títulos y resúmenes usan el modelo barato del proveedor. Claude Max, ChatGPT Pro con Codex y Cursor son recursos de desarrollo. Horas del autor: rango del tutor de 25 a 50 USD por hora. **[PENDIENTE: horas registradas por semana; imputación del equipo por depreciación; análisis financiero con TCO; no se calcula retorno mientras no exista línea base de tiempo.]**

# Descripción de estudios realizados

La Tarea 2 revisó diez estudios de 2022 a 2026: tres sobre modelado temático y agrupamiento con embeddings (Grootendorst, 2022; Egger y Yu, 2022; Zhang et al., 2022), tres sobre agentes y generación con citas (Yao et al., 2023; Gao et al., 2023; Min et al., 2023), dos sobre productividad y decisión con IA generativa (Noy y Zhang, 2023; Csaszar et al., 2024) y dos sobre explicaciones y sesgo de popularidad en recomendación (Feng et al., 2026; Klimashevskaia et al., 2024). Ninguno mide utilidad editorial ni adquisición de miembros. El enfoque, el resultado y el límite de cada estudio están en la tabla de la Tarea 2.

Dos lecciones guiaron el diseño. Un agrupamiento más complejo no es mejor de antemano (Zhang et al., 2022): por eso se compararon BERTopic y K-means y el motor usa un apilado simple por coseno. Una cita no garantiza respaldo (Gao et al., 2023; Min et al., 2023): por eso la meta del 90 % cuenta afirmaciones respaldadas, el validador del guion cuenta mecánicamente afirmaciones con y sin cita, y el juicio de respaldo sigue siendo humano.

**Detección temporal.** BERTrend (Boutaleb et al., 2024) entrena un modelo por corte, fusiona temas y separa ruido, señal débil y señal fuerte; el motor toma la idea de señales que persisten día a día, sin fusión ni decaimiento. BackTrend (Zhou et al., 2026) evalúa señales científicas, con F1 de 10,1 % para su mejor sistema. Los ciclos de atención se acortan (Crane y Sornette, 2008; Lorenz-Spreen et al., 2019), lo que hace verosímil una ventana corta, coherente con la mediana de uno a dos días de 7.3 sin probarla. El sistema se documenta con una Model Card (Mitchell et al., 2019). Las obras anteriores a 2019 (Shapley, 1953; Hubert y Arabie, 1985; Rousseeuw, 1987; Crane y Sornette, 2008) se citan como fuentes originales de los métodos o hallazgos usados.

**Vacío.** Ningún estudio revisado evalúa el ciclo completo para un operador único (señales de varias fuentes, agrupamiento temporal, guion con respaldo verificable y decisión registrada) frente al proceso manual. La revisión fue exploratoria. **[PENDIENTE: ampliar la bibliografía sobre utilidad en recomendación de contenido y sesgos de modelos de lenguaje, como pidió el Comité.]**

# Desarrollo del proyecto

## Diseño de la solución

**Enfoque.** Desarrollo tecnológico aplicado con comparación intrausuario: cada iteración fija un protocolo, ejecuta, mide y registra la decisión. Están completos el análisis exploratorio, el modelado del motor y su evaluación técnica; la evaluación humana está pendiente y la implementación en entorno real está en curso: el operador usó la vista previa del prototipo con una corrida real y dictó cambios de nombre y de orden que ya están integrados.

**Principios.** Determinista y sin modelo: misma entrada, misma salida; cada corrida lleva huellas de configuración, corpus y resultado. El humano decide y el modelo solo lee: las herramientas del agente son de solo lectura y la decisión se graba por un camino que el modelo no puede invocar. La línea base va a la vista: cada ficha muestra su posición por volumen y por fórmula. Un día perdido no vacía la lista: la cobertura por fuente es un dato de la corrida. Local y a costo cero en el motor: embeddings en la máquina, fuentes públicas sin claves. Procedencia por diseño: toda tendencia enlaza a sus ítems, todo ítem a su fuente y fecha, toda corrida a su corte. Aditivo a la base: paquetes y carpetas propios, enganches de una línea en los archivos de T3 Code, banderas para esconder y un registro de cada archivo divergente. El producto útil prima sobre cada compromiso literal, gana la opción con menos código y el motor es reemplazable, mientras el contrato de la ficha y la instrumentación son rígidos.

**Cambio de corpus.** Hecho: la Tarea 3 acordó X y Reddit; el prototipo usa Hacker News y GitHub. Justificación propuesta para el tutor: X cobra cada consulta y el lote pagado reunió 99 publicaciones capturadas en 28 minutos y 37 segundos, insuficientes para evaluar la evolución semanal de tendencias; el acceso de Reddit sigue pendiente; Hacker News aporta historial para la retrospectiva; GitHub aporta metadatos actuales, sin historial de estrellas, y queda fuera de la retrospectiva. El costo es que la población de señales cambia, la evidencia sobre X queda como histórica y la retrospectiva mide actividad en Hacker News, no utilidad para la audiencia. Hay adaptadores de cinco fuentes más (Wikipedia Pageviews, Stack Exchange, arXiv, npm y Bluesky) en la versión anterior del prototipo; ninguno entra en el corpus evaluado. Hecho: el correo al tutor no se ha enviado (Anexo 3).

**Criterios de evaluación, fijados antes de ejecutar.** Sistema: las metas de la Tarea 1 (capítulo 3); el contraste de seis pares mide el tiempo por etapa, de modo que compara explorar a mano frente a la bandeja de Tendencias, escribir a mano frente a escribir con asistente sobre el mismo tema, y el proceso completo manual frente al asistido; el tiempo activo de semanas anteriores se informa con el registro de dos semanas. Retrospectiva: precisión en 5 y en 10 frente a la línea base `items_7d` y mediana de días hasta el evento. Robustez, con los umbrales del curso: una perturbación del 5 % que mueve la salida más del 40 % indica inestabilidad, y un cambio mayor del 20 % en una métrica clave exige actuar. Agrupamiento sobre X: cobertura de al menos 80 %, silueta coseno válida en cinco semillas (Rousseeuw, 1987), estabilidad ARI (Hubert y Arabie, 1985) y claridad ciega de al menos 3,5 sobre 5. Ninguna métrica técnica mide calidad editorial.

**Decisiones de experiencia de uso.** Hecho: el autor validó en pantalla dos maquetas con datos reales, "Una mañana con Earlyscript" y "Modo manual", y fijó diez decisiones: al arrancar, si hay corrida nueva, abrir en Tendencias con el conteo de nuevas; título de una línea y resumen de tres párrafos por tendencia, redactados una vez por corrida por el asistente, marcados como tales y sin cambiar el orden; orden por defecto nuevas primero y luego por crecimiento, con selector por volumen y por afinidad; la bandeja de tendencias reutiliza el modelo de bandeja de hilos de T3 Code (no leída, seguir observando, descartar con motivo, en producción con enlace al hilo); hasta 10 nuevas visibles; reloj visible con pausa que se detiene en la decisión; tercer espacio Resultados descriptivo, sin calcular ahorro; métricas del video a mano en el hilo cerrado; modo manual sin chat ni motor con tres etapas (Explorar con navegador integrado y captura rápida, Escribir con editor Markdown y versiones, Decidir con la misma grabación); y "Ficha de tendencia" en lugar de "Expediente".

## Desarrollo de la solución

**Arquitectura.** Earlyscript es un fork de T3 Code (T3 Tools, 2026), un estudio de escritorio para agentes de código con licencia MIT, que aporta hilos de conversación con historial, proveedores de modelos por los agentes instalados en la máquina, un servicio de generación de texto, un navegador integrado, un editor de archivos y un visor de diferencias. Sobre esa base, el prototipo añade tres espacios en la barra lateral, Hilos, Tendencias y Resultados, y una base propia `editorial.sqlite` junto a la de T3 Code. El flujo tiene cuatro capas:

1. **Evidencia.** Adaptadores de solo lectura capturan, por día UTC, historias de Hacker News por la API de Algolia y repositorios de GitHub creados ese día con 20 estrellas o más, con pausas, reintentos y bloqueo por cuota. Cada día queda `complete`, `partial` o `unavailable`, en un corpus por archivos JSONL con manifiesto SHA-256; GitHub es siempre `partial` porque devuelve 100 repositorios por consulta ordenados por estrellas actuales.
2. **Cálculo.** Un motor determinista, sin modelo de lenguaje, aplica un corte antes de abrir archivos; toma título más 1.000 caracteres de cuerpo; excluye el texto con menos del 90 % de letras ASCII (una aproximación al inglés) y los duplicados por URL; embebe con `onnx-community/Qwen3-Embedding-0.6B-ONNX` (revisión `c25a394`, q8, CPU, 1.024 dimensiones) en procesos hijo con caché por modelo, plataforma y texto; apila cada ítem, en orden de publicación, a la señal activa en los últimos 30 días de mayor coseno si supera 0,70, o abre una señal; calcula series diarias de ítems, autores y fuentes; asigna etapa con g = ln((ítems de 7 días + 1) / (ítems de los 7 previos + 1)), `growing` si g ≥ 0,69 con al menos tres ítems recientes, `fading` si g ≤ −0,69, `steady` en otro caso; calcula afinidad como coseno máximo con los temas incluidos del perfil del canal (umbral 0,60) y bajo 0,60 con los excluidos; y ordena las señales elegibles de dos formas, por ítems de siete días y por 0,5 × crecimiento + 0,2 × ln(1 + autores de 7 días) + 0,3 × afinidad, emitiendo hasta 20 fichas con hasta diez evidencias, cobertura por fuente y huecos de datos. Un día sin datos queda marcado y no vacía la lista. El apilado guarda los centroides en un arreglo contiguo y poda con la cota de Cauchy-Schwarz: 9,7 veces más rápido con señales idénticas bit a bit a la versión directa.
3. **Síntesis.** El servicio de generación de texto de T3 Code, que lanza el CLI local de Claude Code o Codex con el modelo barato del proveedor, redacta una vez por corrida un título y un resumen de tres párrafos por tendencia (qué pasó, por qué importa al canal, qué ángulo de video se ve) citando identificadores de evidencia; el resultado se guarda con el hash del prompt y de la entrada, y se marca "desactualizado" si cambian. En el hilo de video, el operador escribe el guion en un archivo Markdown con el agente que elija; un validador cuenta afirmaciones, citas y afirmaciones sin cita por versión, y está disponible como herramienta MCP `script_check`.
4. **Decisión.** El operador crea un hilo de video desde una tendencia, la sigue observando o la descarta con motivo; en el hilo, acepta, edita, rechaza o difiere el guion con utilidad de 1 a 5, motivo obligatorio, versión decidida y tiempos por etapa de un reloj con pausa registrada. Una política del servidor impide que un agente actúe en un hilo manual. Cada decisión queda ligada a la corrida, la versión del guion y la configuración que produjo su ficha.

La Figura 3 muestra la ficha de tendencia con título y resumen redactados; la Figura 4, la bandeja y la misma ficha antes de redactar, con su evidencia. La aplicación se empaqueta para macOS (455 MiB, sin firmar) y Linux.

**Figura 3**

*Ficha de tendencia con título y resumen redactados por el asistente*

![Nota. Captura del 31 de octubre de 2026, tema claro, sobre la corrida del 19 de octubre. El título y los tres párrafos los redactó claude-haiku-5-5 con citas a identificadores de evidencia; los términos del motor, las dos posiciones del ranking, la afinidad con el perfil, la cobertura por fuente y la curva de 28 días son del motor y no cambian.](archive/output/tareas/evidencias-tarea-10/figura-earlyscript-ficha-tendencia.png)

**Figura 4**

*Bandeja del espacio Tendencias y ficha antes de la redacción del asistente, con evidencia enlazada y el bloque "Por qué está aquí"*

![Nota. Captura del 31 de octubre de 2026. A la izquierda, la bandeja: cada fila muestra la etiqueta del motor, la fuente, la primera evidencia, publicaciones y autores de siete días, la posición por puntaje y la curva. A la derecha, la misma tendencia de la Figura 3 sin título redactado: evidencia con fecha y autor, y las razones del motor para incluirla.](archive/output/tareas/evidencias-tarea-10/figura-earlyscript-bandeja-tendencias.png)

**Estado de la implementación.** La Tabla 5 resume lo que está en la rama principal del prototipo al 31 de octubre de 2026 (commit `f75eebfae2`) y lo que falta. Cada unidad tiene un veredicto de un segundo modelo en solo lectura antes de fusionar; las que tocan datos recibieron "no apto" en su primera pasada y se corrigieron. La divergencia respecto de T3 Code está registrada archivo por archivo: 383 archivos cambiados, 31.448 líneas añadidas y 488 quitadas respecto del commit de origen, la mayoría en paquetes y carpetas propios.

**Tabla 5**

*Componentes del prototipo y su estado al 31 de octubre de 2026*

| Componente | Qué hace | Estado |
|---|---|---|
| Capa de marca y banderas | Nombre, directorio, puertos y esquema de URL propios para convivir con T3 Code; telemetría, analítica de terceros y comprobación de actualizaciones apagadas, con cero salidas de red medidas; terminal, solicitudes de cambio, forjas en la nube, acceso remoto, relay y T3 Connect escondidos y bloqueados en el servidor | Fusionado y verificado |
| Motor de tendencias (`trend-engine`) y contratos | Corpus, corte, embeddings, apilado, series, etapa, afinidad, dos rankings, fichas, `run.json` con huellas; `engine check` reproduce una corrida; fuentes en vivo con captura idempotente | Fusionado y verificado; huella reproducida tres veces |
| Validador del guion (`editorial-script`) | Estructura, citas, afirmaciones con y sin cita, mapa de afirmaciones; CLI | Fusionado y verificado |
| Base editorial y servicios | `editorial.sqlite` con migraciones 001 a 005: estados de bandeja, decisiones, versiones del guion, capturas, resultados, corridas importadas, presentaciones; reloj de trabajo; importador idempotente | Fusionado y verificado |
| Espacio Tendencias | Barra lateral con tres espacios, bandeja con estado (no leída, en observación, descartada, en producción) y sus tres salidas, ficha con evidencia, extracto, cobertura y curva, títulos y resúmenes del asistente; lector de corridas en el formato del motor y en el de la versión anterior | Fusionado y verificado |
| Servidor del hilo de video | Creación desde una tendencia, política que bloquea agentes en hilos manuales, versiones del guion con hash, `script_check` por MCP | Fusionado y verificado |
| Espacio Resultados | Agregados por modo y etapa con mediana, rango intercuartílico y n; utilidad; citas; bandeja; decisiones; estado vacío honesto | Fusionado y verificado; solo ha mostrado datos de prueba |
| Pantalla del hilo de video | Reloj con pausa en la cabecera, guion en el editor con versiones, panel de decisión, bloque de resultado a mano | Fusionado y verificado; probado con un hilo real del agente, no con un ejercicio del operador |
| Modo manual y corrida nocturna | Explorar, Escribir, Decidir sin agente; programador diario | Sin iniciar |

**Versiones y tecnologías.** Hecho: T3 Code en el commit `aa11ef6783` del 30 de octubre de 2026; Node 26.12.1; pnpm 12.14.0; TypeScript y Electron de T3 Code; `@huggingface/transformers` 4.3.1 y `onnxruntime-node` 1.30.0; SQLite por `node:sqlite`; Debian 13 para el servidor y macOS 27 en Apple M4 para el empaquetado. Electron y TypeScript porque los agentes corren en Node; embeddings en CPU para no mantener otro lenguaje; apilado frente a BERTopic porque cada asignación se explica con un coseno; T3 Code porque ya resuelve hilos, proveedores e historial y porque su licencia permite el fork. No se entrena ningún modelo: se calibran umbrales, pesos y perfil. Los asistentes de programación (Claude Code con Opus 5.5 y Fable 5.1; Codex con GPT-6 Astra y GPT-6.1 Sol) fueron recursos de desarrollo, no parte del sistema. **[PENDIENTE: cita APA del uso de IA generativa según la política de la UDLA.]**

**Pruebas.** Hecho: la batería rápida del prototipo (`es:typecheck`, `es:test`) cubre los paquetes propios y los módulos de T3 Code que tocan; la batería completa de T3 Code corre antes de cada fusión y pasó el 31 de octubre en un servidor Linux de 22 núcleos (630 s) y en una Mac mini (706 s). Sobre la rama principal pasaron el typecheck de 39 paquetes y 122 pruebas editoriales en 15 archivos. El apilado acelerado se probó contra la versión directa en 401 casos con hashes idénticos. Verifican contratos y flujos, no calidad editorial.

**Reproducibilidad y entrega técnica.** El repositorio tiene un README con propósito académico, problema y solución, requisitos, ejecución paso a paso (instalar, capturar fuentes, correr el motor, verificar una corrida, validar un guion, arrancar el estudio, empaquetar), pipeline, organización de carpetas, pruebas y evidencia, fuentes y condiciones de uso, y limitaciones; un registro de divergencia respecto de T3 Code; y una guía del entorno Linux. Los datos viven fuera del repositorio, en `~/earlyscript-data/` (corpus, corridas, modelos, caché de embeddings, perfiles). Un clon en un segundo servidor instaló y compiló desde cero y la corrida reciente pasó `engine check`. Hecho: el código se publica en https://github.com/mickroplastics/earlyscript, y los informes y evidencias de esta tesis en https://github.com/mickroplastics/tesis; la versión anterior del prototipo, Earlywindow, con su README para evaluadores, retrospectiva, robustez y paquete congelado verificable, queda en un repositorio privado con acceso de lectura a solicitud del tutor y del tribunal. El Anexo 4 mapea cada elemento de la consigna a su evidencia. **[PENDIENTE: video de la demo de tres minutos; acceso efectivo del tutor y del tribunal a Earlywindow.]**

## Resultados y Discusión.

Los resultados técnicos del motor se midieron en Earlywindow, la versión anterior del prototipo, con el mismo método y la misma configuración (`include_min` 0,60); la corrida reciente se hizo en Earlyscript. La evaluación humana no se ha hecho.

**Corrida de evaluación.** Hecho: corpus congelado del 30 de agosto al 18 de octubre de 2026, 49.784 historias de Hacker News en 50 días completos y 678 repositorios de GitHub en 50 días parciales; 45.557 textos tras excluir 121 por idioma y 4.784 duplicados; 13.701 señales, 86 `growing`, 11.922 `steady`, 1.693 `fading`; 18 fichas en 305 segundos; huella lógica registrada. El 89,25 % de las señales tiene un solo ítem, la mayor reúne 2.830 ítems bajo una etiqueta genérica y 169 de 172 evidencias tienen extracto vacío. **Interpretación.** El motor aísla señales en crecimiento en cinco minutos, pero la mayoría de los grupos son aislados, algunos mezclan temas y gran parte de la evidencia es un título. Una ficha acredita de dónde viene una señal, no que el artículo respalde el guion.

**Corrida reciente.** Hecho: corte del 31 de octubre de 2026, 28.311 historias de Hacker News en 28 días completos y 282 repositorios de GitHub en 28 días parciales, capturados en vivo; 26.037 textos embebidos; 8.776 señales, 99 `growing`; 251 pasan el perfil y 15 son elegibles; 374 segundos en Linux; `engine check` correcto. Las cinco primeras por volumen tratan de mercados y apuestas en tecnología, la salida a bolsa de un proveedor de modelos, el empleo, agentes para productos SaaS y la burbuja de IA; por fórmula, el empleo sube al primer puesto. La afinidad con el canal va de 0,60 a 0,76. La redacción de tres fichas con `claude-haiku-5-5` tardó de 12 a 22 segundos por ficha y la revisión no encontró atribuciones inventadas.

**Prueba retrospectiva.** El motor se ejecutó a ciegas, solo con Hacker News y sin ajuste, en cortes del 13, 20 y 27 de septiembre y 4 de octubre. Las historias de los 14 días siguientes se asignaron a cada candidata por coseno mayor que 0,70 contra su centroide congelado; una candidata es positiva el primer día en que acumula cinco historias de dos autores, y la anticipación cuenta los días hasta ese evento (Tabla 6).

**Tabla 6**

*Precisión retrospectiva de la fórmula frente al orden por volumen, configuración de evaluación (`include_min` 0,60)*

| Corte | Positivas sobre candidatas | P@5 fórmula / volumen | P@10 fórmula / volumen | Mediana de días hasta el evento |
|---|---:|---:|---:|---:|
| 13 de sep. | 19 de 20 | 0,80 / 1,00 | 0,90 / 0,90 | 1 |
| 20 de sep. | 11 de 12 | 1,00 / 1,00 | 1,00 / 1,00 | 1 |
| 27 de sep. | 20 de 20 | 1,00 / 1,00 | 1,00 / 1,00 | 1 |
| 4 de oct. | 14 de 15 | 1,00 / 1,00 | 0,90 / 1,00 | 1 |
| Agregado | 64 de 67 | 0,95 / 1,00 | 0,95 / 0,975 | 1 |

Notas. Precisión agregada como media de los cortes; P@k usa `min(k, candidatas)`. Con la configuración anterior (`include_min` 0,50, 80 candidatas) el agregado fue 0,80 frente a 0,90 en P@5 y la mediana, 2 días. Las filas son señales con ventanas solapadas, no observaciones independientes; no hay intervalo de confianza. Resultado medido en macOS.

**Interpretación.** La fórmula no supera a la línea base en ningún corte: pierde en el primero y empata en los otros tres. La etiqueta casi se satura: 64 de 67 candidatas cruzan el umbral, 22 el mismo día del corte, y solo 2 tardan siete días o más. La mediana mide actividad mínima en Hacker News, no interés de la audiencia. **La hipótesis de avisar una o dos semanas antes no queda respaldada.** Como el umbral 0,60 se eligió mirando el corte del 19 de octubre, esa retrospectiva no es independiente. Hipótesis: el umbral alto filtra hacia temas que ya tienen volumen. Este motor no anticipa con estos datos; eso no prueba que ninguno pueda. Por eso la ficha muestra las dos posiciones y el orden por defecto en la interfaz es por crecimiento, no por fórmula.

**Robustez.** Cinco familias de perturbación con semilla fija y sin proveedor real (Tabla 7).

**Tabla 7**

*Pruebas de robustez del motor, configuración de evaluación*

| Familia y perturbación | Efecto | Lectura con los umbrales del curso |
|---|---|---|
| Pesos: ±5, ±10 y ±20 % por peso; 90 escenarios | Tau de Kendall mínima 0,905; con ±5 % se movió como máximo el 20 % de las candidatas; ningún escenario supera el umbral de actuación | Estable |
| Umbral de apilado: 0,65 y 0,75 frente a 0,70 | Con 0,65, de 18 a 5 fichas, porque solo 77 señales superan la afinidad mínima; con 0,75, 20 | Sensible: ±0,05 es ±7,14 % relativo. Hipótesis central |
| Ítems quitados: 5 % con semilla fija | El top 10 sustituye entre 2 y 5 de 10 según la semilla | En el límite del 40 %; el identificador depende del primer ítem |
| Proveedor: 429, 500, respuestas vacías y truncadas | Las ocho combinaciones terminan en fallo con motivo, sin ficha parcial; el reintento manual termina bien | Esperado con proveedor simulado |
| Deriva: 13 de sep. frente a 4 de oct. | 62,09 % de 5.104 señales activas a 30 días y 11,78 % con actividad nueva; Jaccard de etiquetas 0,456 | El vocabulario cambia en tres semanas; recalcular a diario |
| Día perdido en los 14 previos al corte | En la versión anterior dejaba cero fichas; el motor actual marca el día como desconocido y conserva la lista | Corregido; no probado con una fuente caída en vivo |

Notas. Una verificación independiente recalculó el umbral y los ítems quitados desde sus bases y coinciden. Un Jaccard bajo mide cambio de membresía, no pérdida de utilidad. La prueba de pesos no vuelve a agrupar. Añadido: el mismo motor en Linux emite 19 fichas frente a 18 en macOS y coincide en 3 de 5 del top 5 por volumen; la plataforma de los vectores es una fuente más de variación.

**Interpretación.** La puntuación es robusta a sus pesos; el apilado es sensible a su umbral, a la muestra y a la plataforma, y la salida depende de la combinación de umbral de apilado y umbral de afinidad. Las fichas sirven como material de trabajo; ni la lista ni la posición en el top 10 son una medida estable de qué temas importan.

**Verificación independiente.** Hecho: un modelo distinto del que programó verificó cada unidad en solo lectura. En la versión anterior, tres pasadas sobre la integración encontraron doce hallazgos (entre ellos motivos privados en el paquete compartible y un enlace entre ficha y perfil sin validar), corregidos antes de declararla apta. En el prototipo actual, cada unidad de la Tabla 5 tiene veredicto; el importador de corridas y el lector del formato nativo recibieron "no apto" en su primera pasada por defectos de datos (manifiesto sin protección, corrida corrupta invisible, base importada que no se reindexa) y se corrigieron antes de fusionar.

**Evidencia sobre X (Tareas 5 a 7).** Sus cifras no describen al motor. La API de X devolvió 100 publicaciones; quedaron 99 textos de 94 autores en 28 minutos y 37 segundos, partidos 59, 20 y 20. Con Qwen3-Embedding-0.6B (Qwen, s. f.), UMAP ajustado con 59 textos (McInnes et al., 2018) y cinco semillas, se compararon K-means 10, K-means 5 y BERTopic con HDBSCAN (Grootendorst, 2022) sobre los mismos 79 textos. K-means 5 se eligió antes de abrir la prueba por menor fragmentación (2,6 grupos de un texto frente a 4,4) y no por superioridad: su silueta de validación fue −0,0165 ± 0,0229 frente a −0,0182 ± 0,0243, con dos semillas a favor y tres en contra; ARI de 0,88 y 0,86 en validación y prueba; BERTopic no alcanzó la cobertura mínima (0 % y 2 %). En el ensayo de la Tarea 6, el autor como único operador hizo dos fichas manuales (296,0 segundos con utilidad autovalorada 2, y otra incompleta al límite de 300 con 3) y dos asistidas (170,1 y 130,3 segundos, con 4 y 5); un tiempo censurado impide calcular ahorro. SHAP sobre un sustituto con fidelidad del 62 % (Lundberg y Lee, 2017), LIME (Ribeiro et al., 2016) y valores de Shapley exactos (Shapley, 1953) mostraron que la recencia decidía el orden y que el mismo grupo ganaba en las 171 combinaciones de pesos; por eso el motor reemplazó la recencia por crecimiento entre ventanas. El prototipo de esa etapa tiene copia pública en https://github.com/miwgel/singularidev-editorial-prototype.

**Discusión frente a los criterios de éxito.** La Tabla 8 da el estado de cada criterio.

**Tabla 8**

*Estado de cada criterio de éxito al 31 de octubre de 2026*

| Criterio | Meta | Evidencia | Estado |
|---|---|---|---|
| Tiempo mediano, métrica principal | 40 % menos tiempo activo desde la búsqueda | Reloj por etapas, hilo de video y decisión fusionados; modo manual sin iniciar; registro de dos semanas declarado, sin integrar; ejercicios sin iniciar | No evaluado |
| Respaldo factual | 90 %, dos juicios | El validador cuenta afirmaciones con cita por versión; el inventario humano y los dos juicios siguen pendientes | No evaluado |
| Utilidad | 4 sobre 5, dos revisores externos | Sin revisores; la decisión registra la del operador con anclas | No evaluable |
| Claridad de grupos | 3,5 sobre 5, ciega | No se traslada el resultado sobre X | No evaluable |
| Tres videos | Resultados descriptivos en siete días | Sin evidencia de publicación | Pendiente |
| Anticipación de una a dos semanas | Señal débil que se vuelve fuerte | Mediana de un día; la fórmula no supera a la línea base | No respaldada |
| Presupuesto | 30 USD mensuales, aparte de X | Suscripción del operador sin precio por solicitud; el motor no gasta inferencia; sin gasto real medido | No verificable |

**Lo demostrado.** El arnés recolecta con procedencia, detecta señales de forma determinista y reproducible en dos plataformas, las presenta con títulos legibles, evidencia enlazada y dos posiciones de ranking, y registra decisiones, versiones y tiempos por etapa; su puntuación es explicable y robusta a los pesos. **Lo débil.** Avisar antes no quedó demostrado: el motor no ordena mejor que contar ítems de la última semana, el apilado depende de su umbral y de la plataforma, la evidencia suele ser un titular y no hay métricas humanas. Las Figuras 5 y 6 muestran lo que existe para la medición, con dos advertencias: los datos de la Figura 5 son un fixture de prueba y el hilo de la Figura 6 es una prueba del agente, no un ejercicio del operador.

**Figura 5**

*Espacio Resultados con datos de prueba sembrados*

![Nota. Captura del 31 de octubre de 2026. Las seis decisiones, los tiempos y las utilidades son un fixture de prueba de la unidad, no ejercicios reales; se incluye para mostrar la forma del reporte, que no calcula ahorro y declara que la comparación de la tesis es por pares y con revisores externos.](archive/output/tareas/evidencias-tarea-10/figura-earlyscript-resultados-datos-de-prueba.png)

**Figura 6**

*Hilo de video con guion versionado y decisión registrada*

![Nota. Captura del 31 de octubre de 2026 en la rama del hilo de video, fusionada y verificada ese mismo día. A la derecha: ficha enlazada, guion con versión y conteo de afirmaciones con cita, decisión "Editar, utilidad 4 de 5" con motivo y tiempos por etapa, y bloque de resultado del video a mano. El hilo y el guion son una prueba del agente, no un ejercicio del operador.](archive/output/tareas/evidencias-tarea-10/figura-earlyscript-hilo-de-video-rama-sin-fusionar.png)

## Implicaciones éticas

El sistema apoya una decisión de riesgo limitado, qué video preparar, pero procesa textos de terceros, los envía a un proveedor de modelos de lenguaje y produce puntuaciones que pueden inducir más confianza de la debida. La referencia es el NIST AI RMF (Tabassi, 2023) y los principios de transparencia, rendición de cuentas, equidad y privacidad (Corrêa et al., 2023). La Tabla 9 responde a la observación 4 del Comité: probabilidad e impacto son juicios cualitativos con los controles aplicados; el responsable de todas las filas es el autor (Supuesto hasta que fije proveedor y retención). "Aplicada" consta en el código fusionado; "propuesta" no existe.

**Tabla 9**

*Matriz de riesgos con probabilidad, impacto y mitigación*

| Riesgo y evidencia | P / I | Mitigación y estado |
|---|---|---|
| R01. Instrucciones incrustadas en textos de terceros (3 de 30 llegan sin marca al extracto) y complacencia del modelo (Nguyen et al., 2026) | Media / alto | Aplicada: el agente del título solo recibe evidencia acotada; los textos se tratan como datos; el guion exige aceptación humana. Propuesta: un recorrido real con la variante inyectada |
| R02. Texto en otro idioma pasa el filtro ASCII (español en 9 de 10 semillas) | Alta / medio | Aplicada: exclusiones por motivo en `run.json` y limitación declarada. Propuesta: rechazo con motivo "language" y recuento |
| R03. La selección depende de la combinación de umbrales (de 18 a 5 fichas) y de la plataforma de los vectores | Alta / alto | Aplicada: configuración fijada por hash, umbrales declarados como hipótesis, caché por plataforma; todo cambio crea otra configuración |
| R04. El top 10 cambia al quitar el 5 % de los ítems | Media / alto | Aplicada: cobertura por fuente y día, dos posiciones visibles y aprobación humana; la posición no se presenta como estable |
| R05. Una fuente caída deja la lista vacía sin explicar la causa | Media / medio | Aplicada: un día sin datos queda marcado y no vacía la lista; aviso de cobertura parcial en la ficha (Figura 3). Propuesta: prueba con una fuente caída en vivo |
| R06. Cambios de API o cuotas | Alta / medio | Aplicada: corpus congelado verificable, reintentos y bloqueo por cuota, respuestas grabadas en las pruebas |
| R07. Términos de las fuentes no cubren todos los usos (Y Combinator) | Alta / alto | Aplicada: corpus local sin redistribución. Propuesta: aclaración de Y Combinator y retención en días |
| R08. Cambia el comportamiento del modelo conversacional | Media / alto | Aplicada: hash del prompt y de la entrada de cada título, estado "desactualizado"; T3 Code registra agente y modelo por hilo. Propuesta: fijar agente y modelo antes del primer ejercicio |
| R09. Las exportaciones divulgan datos privados | Baja / alto | Aplicada en la versión anterior: lista blanca de columnas con sonda sin fugas. Propuesta: consentimiento de los revisores y paquete ciego en el prototipo actual |
| R10. Costo real de inferencia desconocido | Baja / medio | Aplicada: motor sin inferencia; títulos con el modelo barato; costo reportado como desconocido |
| R11. Anclaje en la nota de utilidad | Baja / medio | Aplicada: utilidad obligatoria de 1 a 5 con anclas, sin valor preseleccionado |
| R12. Un solo operador, que además desarrolló el sistema | Alta / alto | Propuesta, con instrumento construido: protocolo fijado antes de medir, espacio Resultados descriptivo y revisores ciegos |
| R13. El crecimiento aporta más de la mitad del puntaje en 10 de 18 fichas; falsa precisión | Alta / medio | Aplicada: desglose visible y orden por defecto por crecimiento, con la fórmula como columna |

**Permisos y términos.** Hacker News: la API de Algolia da acceso técnico, pero Y Combinator restringe copiar, extraer, crear obras derivadas y explotar comercialmente el contenido sin autorización expresa (Y Combinator, s. f.); el corpus se guarda en local para evaluación, y el uso comercial y la redistribución quedan bloqueados hasta una aclaración escrita. GitHub: los términos de su API rigen el acceso (GitHub, 2026). Que un dato sea público no acredita permiso ilimitado ni anonimato. X limita la redistribución y exige borrar lo borrado (X Corp., s. f.); el lote histórico no se redistribuye. Reddit y YouTube no se usaron (Google, 2026).

**Privacidad.** Los embeddings son locales. El servicio de títulos envía al proveedor del agente instalado los términos, los conteos y la evidencia con identificadores de cada ficha; el hilo de video envía lo que el operador escriba y adjunte. La telemetría, la analítica de terceros y la comprobación de actualizaciones de T3 Code están apagadas por bandera, con cero salidas de red medidas. El prototipo no copia credenciales: lee las sesiones de los agentes instalados en su sitio. Borrar la copia local no prueba el borrado remoto. El corpus contiene nombres públicos y no es anónimo. **[PENDIENTE: política escrita de conservación y borrado por fuente; registro de los controles de entrenamiento de los proveedores; consentimiento de los revisores.]**

**Model Card.** Sección integrante del informe con los seis elementos que pide el curso, según Mitchell et al. (2019), en la Tabla 10. Describe el motor en su versión evaluada y en su porte; la Model Card del producto completo se escribirá cuando el hilo de video y el modo manual estén fusionados.

**Tabla 10**

*Model Card del motor de tendencias*

| Elemento | Contenido |
|---|---|
| Versión | Método `engine.v0.02` (`include_min` 0,60) evaluado en Earlywindow `47c7d4d`, corrida 2263f7, 18 fichas; portado como `trend-engine` 0.1.0 con configuración `earlyscript.engine.v1`, corrida 5e57bf del 31 de octubre, 15 fichas. Prompt de títulos v3 con `claude-haiku-5-5`. |
| Propósito y usuario | Apoyar a un solo operador en la priorización de ideas de video en inglés para SingulariDev. El operador decide cada tendencia y cada guion con motivo y utilidad. No entrena pesos de modelos. |
| Componentes | Motor determinista; Qwen3-Embedding-0.6B ONNX q8 en CPU, cuya tarjeta no declara licencia; T3 Code (MIT) con los agentes instalados en la máquina; validador del guion. |
| Datos | Corpus congelado: 49.784 ítems de Hacker News y 678 de GitHub del 30 de agosto al 18 de octubre de 2026, 45.557 con embedding. Corpus reciente: 28.311 y 282 del 3 al 30 de octubre, 26.037 con embedding. El 91,49 % de Hacker News es solo título y todos los días de GitHub son parciales. Datos de inferencia y evaluación, en local y sin redistribución. |
| Métricas | Retrospectiva: P@5 0,95 frente a 1,00 de `items_7d`, P@10 0,95 frente a 0,975, mediana de un día, 2 de 64 positivas con siete días o más; no supera a la línea base en ningún corte. Robustez: tau mínima 0,905 ante pesos; de 18 a 5 fichas con umbral 0,65; top 10 sustituido entre 0,20 y 0,50 al quitar el 5 %. Tiempo, respaldo y utilidad humanos sin medir. |
| Explicabilidad | Desglose aditivo del puntaje y coseno de cada ítem con su centroide; el crecimiento aporta del 33,8 % al 64,7 % del puntaje. El modelo conversacional no tiene explicación validada. |
| Riesgos y limitaciones | Sin anticipación demostrada. Un operador que también desarrolló el sistema. El filtro ASCII deja pasar el español. Selección sensible a los umbrales, a la muestra y a la plataforma. Evidencia casi siempre sin extracto. Instrucciones incrustadas sin marca. Detalle en la Tabla 9. |
| Uso recomendado y no previsto | Apoyo de lectura y redacción para un operador que revisa cada cita y decide. No usar para publicar sin aprobación, predecir tendencias o demanda, verificar hechos, trabajar en otros idiomas, fuentes o periodos sin evaluación, ni atribuir clics, registros o pagos. |

# Conclusiones y Recomendaciones

Las conclusiones son preliminares: se basan en dos corridas del motor, una retrospectiva de cuatro cortes solapados, pruebas automáticas y verificaciones de un segundo modelo, y, para la etapa sobre X, 99 textos y un ensayo de un operador. No se generalizan fuera de ese caso.

1. **Objetivo 1, en curso.** La línea base manual no se acreditó en este avance: hay un diagrama preliminar, dos fichas manuales sobre X y un registro de dos semanas que el autor declara tener, sin integrar ni verificar. Las 20 horas semanales siguen siendo una estimación.
2. **Objetivo 2, completo con validación externa pendiente.** La matriz (4,45 frente a 2,55), los principios del motor y la arquitectura implementada reproducen la alternativa B. Falta comunicar al tutor el cambio de corpus y el cambio de plataforma.
3. **Objetivo 3, parcial con desviación registrada.** El flujo es reproducible: un paquete congelado reconstruye la misma huella en la versión anterior y `engine check` reproduce la corrida reciente; cambiar de plataforma cambia los vectores y parte de las señales. La comparación de agrupadores existe solo sobre X, la de embeddings no se ejecutó y la claridad de grupos no es evaluable en el corpus nuevo. La fórmula no superó a la línea base por volumen y la anticipación no quedó respaldada.
4. **Objetivo 4, parcial.** La integración con los agentes de código existe; los títulos y resúmenes se redactaron con un modelo real; el hilo de video registra versiones del guion, decisión y tiempos; el modo manual no está iniciado. Faltan las seis fichas evaluadas por el operador. La personalización reversible del perfil existe en la versión anterior y no se portó aún.
5. **Objetivo 5, pendiente.** El protocolo está propuesto, sin adopción acreditada, y no hay ejercicios, revisores ni videos. Decisión del autor: si antes del 5 de noviembre un ejercicio completo con modelo real funciona en el prototipo actual, los seis pares se hacen sobre él; si no, se hacen sobre la versión anterior y el prototipo actual pasa a trabajo futuro.

**Síntesis.** El arnés cumple la parte de trazabilidad de la necesidad: conserva fuentes, versiones y decisiones que el proceso manual pierde, dentro de una herramienta que el operador quiere usar a diario. El tiempo queda por medir y la promesa de anticipación no se sostiene con el motor actual.

**Reflexión crítica y retroalimentación integrada.** Por la observación de la Tarea 1, el Anexo 2 incluye el bloque de firmas. Por S4, las versiones están fijadas en el lockfile y la verificación exige las mismas. Por S5, se añadió un modo manual con el mismo reloj y el protocolo de seis pares. S6 valoró el descarte honesto de BERTopic; la retrospectiva informa igual el resultado desfavorable de la fórmula, y por él la interfaz muestra las dos posiciones y ordena por crecimiento. Las observaciones del Comité se responden en las Tablas 7 y 9 y en el Anexo 5. El error principal fue de calendario: construir el motor antes de medir el tiempo humano dejó la métrica principal para las dos últimas semanas, y el cambio de plataforma lo agrava si no se cumple el corte del 5 de noviembre. La corrección es el corte fijado, congelar el producto que se use para los ejercicios y separar mejoras de evaluación. A cambio, el fork redujo el código propio que hay que mantener: las unidades son paquetes y carpetas aditivos con enganches de una línea, en lugar de una aplicación de escritorio completa.

**Recomendaciones.** Al operador: usar las fichas como apoyo de lectura, no como predicción, y abrir el artículo antes de aceptar una afirmación basada en un titular o en un resumen del asistente. Al desarrollo: fusionar solo con verificación, no presentar lo que está en rama como hecho, y probar señales con más contexto que el título. A la gobernanza: pedir a Y Combinator la aclaración de uso y aprobar la política de conservación antes de ampliar el corpus. **[PENDIENTE: conclusión por objetivo con cada meta alcanzada, no alcanzada o no evaluable, tras los ejercicios, el registro y el piloto.]**

# Trabajo futuro

**Lo que falta de esta tesis**, como plan y no como resultado:

- **Semana 13 (2 al 8 de noviembre).** Modo manual y corrida nocturna; corte del 5 de noviembre con un ejercicio completo con modelo real; adopción del protocolo y congelado del producto elegido; sesiones de ejercicios; integración del registro de dos semanas; reclutamiento y calibración de revisores; correo al tutor; demo de tres minutos y pitch. Entrega S11: informe ajustado y presentación.
- **Semana 14 (9 al 15 de noviembre).** Análisis descriptivo de tiempos y utilidad en el espacio Resultados, auditoría de afirmaciones, informe final y ensayo de defensa. Entrega S12 y defensa probable el 13.

Con un solo ejecutor, los seis pares y los revisores caben en dos semanas solo si el producto queda congelado el 5 de noviembre. Si faltan pares, se informan los ejercicios hechos y el mínimo incumplido, sin relajar reglas después de ver resultados. Los pendientes que dependen de terceros están en la Tabla 11.

**Tabla 11**

*Pendientes que dependen de terceros o de la evaluación, al 31 de octubre de 2026*

| Pendiente | De quién depende |
|---|---|
| Validar la Figura 1 con el operador y pasarla a BPMN; captura fechada de YouTube Analytics | Autor |
| Integrar y verificar el registro de dos semanas, declarado como reconstrucción | Autor |
| Sector formal, misión y visión, estado de la comunidad; lugar de operación y obligaciones legales | Autor y auspiciante |
| Tabla complementaria de viabilidad, costo, innovación, impacto y tiempo, si el tutor la pide | Tutor |
| Respuesta de Y Combinator; política de conservación y borrado; controles de entrenamiento de los proveedores; consentimiento de los revisores | Terceros y autor |
| Calibrar la rúbrica de utilidad con los revisores; respuesta del tutor sobre las desviaciones y el cambio de plataforma | Tutor y revisores |
| Horas registradas por semana, imputación del equipo, análisis financiero con TCO | Autor, tras la línea base |
| Ampliar la bibliografía sobre utilidad en recomendación y sesgos de modelos de lenguaje; cita APA del uso de IA generativa | Autor |
| Acceso del tutor y del tribunal a Earlywindow; video de la demo; pitch | Autor y tutor |
| Bloque de firmas y grado académico del tutor en la portada | Tutor |
| Ejercicios, tiempos, utilidades, revisores y auditoría factual; conclusión por objetivo | Evaluación |

**Proyectos posteriores.** Portar las fuentes con adaptador de la versión anterior (Wikipedia Pageviews, Stack Exchange, arXiv, Bluesky y npm); identidad estable de tendencias entre corridas y fusión de señales; "Preguntar a la ficha" con un agente de solo lectura; perfil editable con reversión; conectores de métricas en Ajustes; fusión regular del upstream de T3 Code; firma y notarización para distribuir; X bajo demanda; acceso comercial autorizado; ranking adaptativo, otros idiomas, CRM y medición causal de la adquisición.

# Referencias bibliográficas

Boutaleb, A., Picault, J., & Grosjean, G. (2024). BERTrend: Neural topic modeling for emerging trends detection. En J. Tetreault, T. H. Nguyen, H. Lamba, & A. Hughes (Eds.), *Proceedings of the Workshop on the Future of Event Detection (FuturED)* (pp. 1–17). Association for Computational Linguistics. https://doi.org/10.18653/v1/2024.futured-1.1

Brito Espejo, M. Á. (2026). *Arnés agéntico basado en modelos de lenguaje y análisis semántico de tendencias para priorizar ideas de contenido en YouTube orientadas a la adquisición de miembros para SingulariDev* [Propuesta de proyecto de titulación no publicada]. Universidad de Las Américas.

Corrêa, N. K., Galvão, C., Santos, J. W., Del Pino, C., Pinto, E. P., Barbosa, C., Massmann, D., Mambrini, R., Galvão, L., Terem, E., & de Oliveira, N. (2023). Worldwide AI ethics: A review of 200 guidelines and recommendations for AI governance. *Patterns, 4*(10), Article 100857. https://doi.org/10.1016/j.patter.2023.100857

Crane, R., & Sornette, D. (2008). Robust dynamic classes revealed by measuring the response function of a social system. *Proceedings of the National Academy of Sciences, 105*(41), 15649–15653. https://doi.org/10.1073/pnas.0803685105

Csaszar, F. A., Ketkar, H., & Kim, H. (2024). Artificial intelligence and strategic decision-making: Evidence from entrepreneurs and investors. *Strategy Science, 9*(4), 322–345. https://doi.org/10.1287/stsc.2024.0190

Egger, R., & Yu, J. (2022). A topic modeling comparison between LDA, NMF, Top2Vec, and BERTopic to demystify Twitter posts. *Frontiers in Sociology, 7*, Article 886498. https://doi.org/10.3389/fsoc.2022.886498

Feng, Y., Feuerriegel, S., & Shrestha, Y. R. (2026). Contextualizing recommendation explanations with LLMs: A user study. *Proceedings of the International AAAI Conference on Web and Social Media, 20*(1), 788–803. https://doi.org/10.1609/icwsm.v20i1.42667

Gao, T., Yen, H., Yu, J., & Chen, D. (2023). Enabling large language models to generate text with citations. En H. Bouamor, J. Pino, & K. Bali (Eds.), *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing* (pp. 6465–6488). Association for Computational Linguistics. https://doi.org/10.18653/v1/2023.emnlp-main.398

GitHub. (2026, 27 de abril). *GitHub terms of service*. https://docs.github.com/en/site-policy/github-terms/github-terms-of-service

Google. (2026, 15 de octubre). *YouTube API Services: Developer policies*. https://developers.google.com/youtube/terms/developer-policies

Grootendorst, M. (2022). *BERTopic: Neural topic modeling with a class-based TF-IDF procedure* (arXiv:2203.05794) [Prepublicación]. arXiv. https://doi.org/10.48550/arXiv.2203.05794

Hubert, L., & Arabie, P. (1985). Comparing partitions. *Journal of Classification, 2*(1), 193–218. https://doi.org/10.1007/BF01908075

International Organization for Standardization & International Electrotechnical Commission. (2023). *Software engineering: Systems and software Quality Requirements and Evaluation (SQuaRE): Quality model for AI systems* (ISO/IEC 25059:2023). https://www.iso.org/standard/80655.html

Klimashevskaia, A., Jannach, D., Elahi, M., & Trattner, C. (2024). A survey on popularity bias in recommender systems. *User Modeling and User-Adapted Interaction, 34*(5), 1777–1834. https://doi.org/10.1007/s11257-024-09406-0

Ley Orgánica de Protección de Datos Personales. (2021, 26 de mayo). *Registro Oficial, Quinto Suplemento 459*. https://www.registroficial.gob.ec/quinto-suplemento-al-registro-oficial-no-459/

Lorenz-Spreen, P., Mønsted, B. M., Hövel, P., & Lehmann, S. (2019). Accelerating dynamics of collective attention. *Nature Communications, 10*, Article 1759. https://doi.org/10.1038/s41467-019-09311-w

Lundberg, S. M., & Lee, S.-I. (2017). A unified approach to interpreting model predictions. En I. Guyon, U. von Luxburg, S. Bengio, H. Wallach, R. Fergus, S. V. N. Vishwanathan, & R. Garnett (Eds.), *Advances in neural information processing systems* (Vol. 30, pp. 4765–4774). Curran Associates. https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html

McInnes, L., Healy, J., & Melville, J. (2018). *UMAP: Uniform manifold approximation and projection for dimension reduction* (arXiv:1802.03426) [Prepublicación]. arXiv. https://doi.org/10.48550/arXiv.1802.03426

Min, S., Krishna, K., Lyu, X., Lewis, M., Yih, W.-t., Koh, P. W., Iyyer, M., Zettlemoyer, L., & Hajishirzi, H. (2023). FActScore: Fine-grained atomic evaluation of factual precision in long form text generation. En H. Bouamor, J. Pino, & K. Bali (Eds.), *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing* (pp. 12076–12100). Association for Computational Linguistics. https://doi.org/10.18653/v1/2023.emnlp-main.741

Mitchell, M., Wu, S., Zaldivar, A., Barnes, P., Vasserman, L., Hutchinson, B., Spitzer, E., Raji, I. D., & Gebru, T. (2019). Model cards for model reporting. En *Proceedings of the Conference on Fairness, Accountability, and Transparency (FAT\* '19)* (pp. 220–229). Association for Computing Machinery. https://doi.org/10.1145/3287560.3287596

Nguyen, H., Kamruzzaman, M., Chhabra, A., & Kim, G. L. (2026). *Token-level diagnosis of sycophancy in LLMs with attribution-guided steering* [Prepublicación]. arXiv. https://doi.org/10.48550/arXiv.2607.28906

Noy, S., & Zhang, W. (2023). Experimental evidence on the productivity effects of generative artificial intelligence. *Science, 381*(6654), 187–192. https://doi.org/10.1126/science.adh2586

onnx-community. (s. f.). *Qwen3-Embedding-0.6B-ONNX* (Revisión c25a394dd583836952667c12f008335071b3f43d) [Modelo de embeddings]. Hugging Face. https://huggingface.co/onnx-community/Qwen3-Embedding-0.6B-ONNX/tree/c25a394dd583836952667c12f008335071b3f43d

Otis, N. G., Clarke, R., Delecourt, S., Holtz, D., & Koning, R. (2026). The uneven impact of generative artificial intelligence on entrepreneurial performance: Evidence from a field experiment in Kenya. *Management Science*. Publicación anticipada en línea. https://doi.org/10.1287/mnsc.2024.06909

Qwen. (s. f.). *Qwen3-Embedding-0.6B* [Modelo de embeddings]. Hugging Face. https://huggingface.co/Qwen/Qwen3-Embedding-0.6B

*Reporte ejecutivo de evaluación de proyecto* [Informe no publicado]. (2026). Universidad de Las Américas.

Ribeiro, M. T., Singh, S., & Guestrin, C. (2016). "Why should I trust you?": Explaining the predictions of any classifier. En *Proceedings of the 22nd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining* (pp. 1135–1144). Association for Computing Machinery. https://doi.org/10.1145/2939672.2939778

Rousseeuw, P. J. (1987). Silhouettes: A graphical aid to the interpretation and validation of cluster analysis. *Journal of Computational and Applied Mathematics, 20*, 53–65. https://doi.org/10.1016/0377-0427(87)90125-7

Shapley, L. S. (1953). A value for n-person games. En H. W. Kuhn & A. W. Tucker (Eds.), *Contributions to the theory of games* (Vol. 2, pp. 307–318). Princeton University Press. https://doi.org/10.1515/9781400881970-018

T3 Tools. (2026). *T3 Code* (Commit aa11ef6783) [Software]. GitHub. https://github.com/pingdotgg/t3code

Tabassi, E. (2023). *Artificial Intelligence Risk Management Framework (AI RMF 1.0)* (NIST AI 100-1). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.AI.100-1

X Corp. (s. f.). *X developer policy*. Recuperado el 26 de octubre de 2026, de https://docs.x.com/developer-terms/policy

Y Combinator. (s. f.). *Terms of use*. https://www.ycombinator.com/legal

Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2023). ReAct: Synergizing reasoning and acting in language models. En *The Eleventh International Conference on Learning Representations*. https://openreview.net/forum?id=WE_vluYUL-X

Zhang, Z., Fang, M., Chen, L., & Namazi-Rad, M.-R. (2022). Is neural topic modelling better than clustering? An empirical study on clustering with contextual embeddings for topics. En M. Carpuat, M.-C. de Marneffe, & I. V. Meza Ruiz (Eds.), *Proceedings of the 2022 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies* (pp. 3886–3893). Association for Computational Linguistics. https://doi.org/10.18653/v1/2022.naacl-main.285

Zhou, X., Zhao, Y., Jiang, O., Hu, T., Xu, C., Patwardhan, M., & Cohan, A. (2026). *BackTrend: Evaluating scientific weak-signal prediction via backward reconstruction* [Prepublicación]. arXiv. https://doi.org/10.48550/arXiv.2609.24921


# Anexos

**Anexo 1. Carta de auspicio de Bistec LLC.** Carta del 2 de agosto de 2026 en la que Bistec LLC apoya el proyecto y se compromete a dar acceso a la información y facilitar pruebas, sin relación laboral. Se adjunta el PDF existente. Esta revisión no verificó la firma ni el sello.

**Anexo 2. Firmas de responsabilidad.**

| | Autor | Tutor |
|---|---|---|
| Nombre | Miguel Ángel Brito Espejo | Luis Fernando Aguas Bucheli |
| Firma | | |
| Fecha | | |

**[PENDIENTE: confirmar con el tutor si el bloque aplica al avance y su grado académico, PhD(c) o PhD, para la portada.]**

**Anexo 3. Registro de desviaciones.** Compromisos que la versión de evaluación no cumple tal cual; ninguno bloquea el producto y todos deben comunicarse al tutor, con un correo cuyo borrador existe y no se ha enviado. Las que más afectan a la evaluación: el corpus de Hacker News y GitHub en lugar de X y Reddit (7.1); la comparación de embeddings no ejecutada (Tabla 3); los agrupadores comparados solo sobre X y la anticipación no respaldada (7.3); el producto final como fork de T3 Code y no como aplicación propia sobre Pi; la ficha de ocho apartados generada por el agente sustituida por un guion escrito por el operador con asistente y validador; el modelo de lenguaje como agente instalado en la máquina y no como proveedor fijado por configuración; la interfaz editorial en español; el reloj por etapas en lugar de un cronómetro desde la búsqueda. El registro completo, con 37 filas de la versión anterior, sustituto, efecto por objetivo y estado, está en la base documental del proyecto.

**Anexo 4. Entrega técnica del prototipo.** Correspondencia entre lo que pide la consigna y dónde está.

| Elemento de la consigna | Dónde está |
|---|---|
| Implementación final y código limpio, modular y estructurado | https://github.com/mickroplastics/earlyscript, rama `main`: paquetes `editorial-contracts`, `trend-engine`, `editorial-script`; carpetas `apps/server/src/editorial`, `apps/web/src/editorial`, `apps/*/src/earlyscript`; enganches de una línea registrados en `docs/upstream-divergence.md` |
| Modelo final validado | No se entrena un modelo: se calibran umbrales, pesos y perfil, fijados por hash en `packages/trend-engine/config/engine.v1.json` y validados con la retrospectiva y la robustez de 7.3 |
| Mejoras del curso | Tabla 5 (unidades), capítulo 8 (reflexión) y Anexo 3 (desviaciones) |
| Evidencia de pruebas finales | `pnpm es:test` y batería completa de T3 Code; informes de verificación por unidad en la base documental; huellas de corrida reproducidas |
| README: problema y solución, requisitos, ejecución paso a paso, pipeline | `README.md` del repositorio |
| Control de versiones y demo | Historial Git con una rama por unidad y veredicto antes de fusionar; capturas en https://github.com/mickroplastics/tesis (`evidencias-tarea-10/`); video de la demo pendiente |
| Organización de carpetas (datos, scripts, resultados) | Código en el repositorio; datos en `~/earlyscript-data/` (`corpus/`, `runs/`, `models/`, `embeddings/`, `profiles/`), fuera de Git |
| Resultados finales, métricas comparativas, robustez | 7.3, Tablas 6 a 8 y Model Card (Tabla 10) |
| Anexos técnicos previos | Tareas 1 a 8 en https://github.com/mickroplastics/tesis; Earlywindow (README para evaluadores, retrospectiva, robustez, paquete congelado) en repositorio privado con acceso a solicitud |

**Anexo 5. Observaciones del Comité y su estado al 31 de octubre.**

1. Diagramar el proceso manual: diagrama preliminar (Figura 1); BPMN pendiente.
2. Medir la carga con registros reales: registro de dos semanas declarado por el autor, reconstruido; sin integrar ni verificar.
3. Anclas de utilidad y validación de la rúbrica: anclas definidas; validación con revisores pendiente.
4. Riesgos con mitigaciones: hecho, matriz de 13 riesgos (Tabla 9).
5. Algoritmo además de BERTopic: hecho sobre X.
6. Sensibilidad de pesos: hecho sobre X (171 combinaciones) y sobre el motor (90 escenarios).
7. Datos, permisos, cuotas y términos: hecho para Hacker News, GitHub, X, Reddit y YouTube; aclaración de Y Combinator pendiente.
8. Robustez ante fallos y variación de tendencias: hecho para pesos, umbral, pérdida de ítems, proveedor, deriva y día perdido; añadida la sensibilidad a la plataforma.
9. Procedencia, herramientas, parámetros y decisiones: hecho, con huellas por corrida, decisiones ligadas a su corrida, reproducción desde un clon limpio y registro de divergencia archivo por archivo.
10. Bibliografía sobre utilidad y sesgos: pendiente.

**Anexo 6. Protocolo de evaluación humana.** Propuesto el 22 de octubre de 2026; su adopción, la selección de pares y la ejecución no están acreditadas. El instrumento es el hilo de video (asistido o manual) con reloj por etapas y el espacio Resultados.

- **Registro.** El registro de dos semanas del autor, reconstruido, se integra declarado como tal; un día sin registro es faltante, no cero.
- **Pares y asignación.** Seis pares comparables fijados antes de conocer resultados; condición y orden por semilla registrada, tres sesiones con manual primero y tres con asistida.
- **Tareas.** Guion en inglés con la estructura del validador y 30 minutos como límite; en manual, sin modelo generativo. Antes del primer ejercicio se fijará qué textos leen ambas condiciones y cualquier asimetría se declarará antes de medir.
- **Tiempo.** El reloj del hilo registra explorar, leer, escribir y decidir, con pausas; el contraste principal es el proceso completo por par. Un ejercicio al límite o abandonado se informa como censurado.
- **Calidad y análisis.** Utilidad por el operador y por dos revisores ciegos; auditoría de cada cita y de las afirmaciones sin cita, inventariadas aparte, con la misma lista para el segundo juicio. Medianas por condición y diferencias por par, descriptivas, sin prueba de significación ni atribución causal.

**[PENDIENTE: ejercicios ejecutados, tiempos, utilidades, revisores confirmados y resultados de la auditoría factual.]**

**Anexo 7. Fuentes técnicas.** Base documental del proyecto en el repositorio privado de la tesis: especificación y unidades del motor (`planificacion/2026-10-21-earlywindow-spec/`), informes de las olas 7 y 8 (`2026-10-22-ola7/`, `2026-10-26-ola8/`, con las verificaciones independientes, el protocolo, el registro de desviaciones y la versión extensa anterior de este avance), y diseño y plan de construcción del prototipo actual (`2026-10-30-earlyscript-motor/`). Datos fuera de Git: corridas, retrospectivas, verificaciones y capturas en `~/earlywindow-data/` y `~/earlyscript-data/`.
