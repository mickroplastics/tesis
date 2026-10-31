---
title: "Arnés agéntico basado en modelos de lenguaje y análisis semántico de tendencias para priorizar ideas de contenido en YouTube orientadas a la adquisición de miembros para SingulariDev"
author: "Miguel Ángel Brito Espejo"
guide: "Luis Fernando Aguas Bucheli"
date: "30 de octubre de 2026"
version: "Avance consolidado S10, versión 4 del 30 de octubre de 2026"
---

# Resumen

SingulariDev, unidad de Bistec LLC, busca atraer desde YouTube a emprendedores unipersonales angloparlantes interesados en agentes de inteligencia artificial. Su fundador investiga y prioriza ideas de video a mano, estima esa carga en más de 20 horas semanales y no conserva un registro que una señales, evidencia y decisiones. El proyecto desarrolla y valida un arnés agéntico que detecta señales, las ordena con una fórmula explícita y acompaña la redacción de guiones en inglés con un modelo de lenguaje, con decisión humana registrada. Una matriz con criterios de ISO/IEC 25059:2023 favoreció un arnés híbrido y modular, con 4,45 frente a 2,55 sobre 5. Las Tareas 5 a 7, sobre 99 publicaciones de X, dejaron K-means como opción provisional frente a BERTopic. Entre el 21 y el 26 de octubre se construyó Earlywindow, una aplicación de escritorio con un motor determinista de tendencias sobre 50.462 ítems de Hacker News y GitHub, agrupados con Qwen3-Embedding-0.6B en CPU. Su prueba retrospectiva dio una precisión de 0,95 entre las cinco primeras candidatas frente a 1,00 de una línea base por volumen, con una mediana de un día hasta el evento: avisar una o dos semanas antes no queda respaldado. El 30 de octubre el autor decidió que el producto final es Earlyscript, un fork privado de T3 Code, un estudio de agentes de código con licencia MIT, que conserva sus hilos, proveedores de modelos e historial y añade el motor portado de Earlywindow, un espacio de Tendencias con fichas redactadas por el asistente, hilos de video con guion versionado y un espacio de Resultados. Al 31 de octubre, diez unidades están fusionadas y verificadas por un segundo modelo, y una corrida fresca sobre 28 días emitió 15 fichas en 6 minutos. Earlywindow queda como motor y antecedente evaluado. La reducción de tiempo del 40 %, el respaldo factual del 90 % y la utilidad según revisores externos siguen sin medirse; los ejercicios humanos correrán sobre Earlyscript si un ejercicio completo con modelo real funciona antes del 5 de noviembre.

**Palabras clave:** arnés agéntico, modelos de lenguaje, detección de tendencias, priorización editorial, trazabilidad.

# Abstract

SingulariDev, a unit of Bistec LLC, aims to reach English-speaking solo entrepreneurs interested in artificial intelligence agents through YouTube. Its founder researches and prioritizes video ideas by hand, estimates that workload at more than 20 hours per week, and keeps no record linking signals, evidence, and decisions. The project develops and validates an agentic harness that detects signals, ranks them with an explicit formula, and supports the drafting of English video scripts with a language model, with a recorded human decision. A matrix based on ISO/IEC 25059:2023 favored a hybrid modular harness, scoring 4.45 versus 2.55 out of 5. Tasks 5 to 7, on 99 X posts, kept K-means as a provisional option over BERTopic. Between October 21 and 26, Earlywindow was built: a desktop application with a deterministic trend engine over 50,462 Hacker News and GitHub items, clustered with Qwen3-Embedding-0.6B on CPU. Its four-cutoff retrospective test reached a precision of 0.95 among the top five candidates against 1.00 for a volume baseline, with a median of one day until the event, so the hypothesis of a one-to-two-week early warning is not supported. On October 30 the author decided that the final product is Earlyscript, a private fork of T3 Code, an MIT-licensed coding-agent studio, which keeps its threads, model providers, and history and adds the trend engine ported from Earlywindow, a Trends space with assistant-written briefs, video threads with a versioned script, and a Results space. As of October 31, ten units are merged and verified by a second model; a fresh run over 28 days of Hacker News produced 15 briefs in 6 minutes. Earlywindow remains as the engine and as the evaluated antecedent. The 40 % time reduction, the 90 % factual support, and usefulness rated by external reviewers remain unmeasured; the human exercises will run on Earlyscript if a complete exercise with a real model works before November 5.

**Keywords:** agentic harness, language models, trend detection, editorial prioritization, traceability.

# Introducción

**Cómo leer este avance.** Es la versión consolidada de la semana 10, versión 4, cerrada el 30 de octubre de 2026 con corte de datos del 31 de octubre a las 02:40 UTC. Parte del borrador de la Tarea 8 y de la versión condensada del 26 de octubre. Describe tres etapas del arnés: la etapa sobre X (Tareas 5 a 7), Earlywindow (21 a 26 de octubre, con sus resultados técnicos en 7.3) y Earlyscript (30 y 31 de octubre), que es el producto final por decisión del autor del 30 de octubre. Las fuentes técnicas están en el Anexo 4. **Hecho** es medido o leído en una fuente; **Estimación**, un cálculo; **Supuesto**, una condición de diseño; **Hipótesis**, una afirmación pendiente de prueba. Lo que falta se marca **[PENDIENTE: …]** y se ordena por semana en el capítulo 9. Lo que está en una rama sin fusionar se declara así y no se presenta como hecho.

## Identificación y descripción del problema o necesidad

El fundador de SingulariDev busca ideas de video, decide cuáles investigar, lee, compara, escribe una ficha y decide si graba. Lo hace solo y estima que investigar y priorizar le toma más de 20 horas semanales (Brito Espejo, 2026). Es una estimación. Hecho declarado por el autor el 30 de octubre de 2026: existe un registro de dos semanas del proceso manual, con la búsqueda y la escritura separadas y con el resultado de cada idea, reconstruido a partir del 1 de octubre; este avance no incorpora sus cifras porque no se verificaron todavía, y se integra en S11 como reconstrucción, no como registro en el momento. Además, no consta qué señal llevó a cada idea, con qué criterio se filtró ni por qué se grabó, y YouTube Analytics no se conecta con la decisión que originó el video. La Figura 1 marca tres puntos donde probablemente se pierde el rastro.

**Figura 1**

*Proceso manual de investigación y selección de ideas*

![Nota. Reconstrucción documental a partir de la Tarea 1; los recuadros rojos marcan los posibles puntos de pérdida de trazabilidad. Pendiente de validar con el operador.](archive/output/tareas/evidencias-tarea-08/figura-1-proceso-manual.png)

Las causas son hipótesis de la Tarea 1: señales repartidas entre fuentes, criterios editoriales no escritos, una sola persona que investiga y produce, y fuentes que cambian cuotas y términos. La falta de miembros no es el problema que se ataca, porque depende también del video, la oferta y el precio. Al ser una necesidad de la organización y no la falla de un sistema, se analiza con un FODA (Tabla 1), aceptado por el Comité (*Reporte ejecutivo de evaluación de proyecto*, 2026).

**Tabla 1**

*FODA de SingulariDev (Brito Espejo, 2026, §2.3)*

| | Interno | Externo |
|---|---|---|
| **Favorable** | Canal propio con unos 7.200 suscriptores al 2 de agosto de 2026 y acceso a sus métricas. Experiencia del fundador en software, IA y contenido. | APIs y datos públicos con historial. Un segmento angloparlante nuevo de emprendedores unipersonales. Modelos de lenguaje con herramientas para sintetizar evidencia. |
| **Desfavorable** | Operación individual con más de 20 horas semanales estimadas. Audiencia histórica en español y comunidad inglesa sin historial. Criterios manuales sin registro. | Cambios de cuotas, precios y términos de las fuentes. Sesgo, saturación y variación rápida de los temas. Alucinación del modelo y dependencia del proveedor. |

La asistencia generativa redujo un 40 % el tiempo de escritura profesional (Noy y Zhang, 2023), pero preparar una idea también exige buscar y seleccionar, y en 640 emprendedores no tuvo un efecto promedio concluyente (Otis et al., 2026). Una conversación con un modelo tampoco registra fuentes, criterios ni decisiones. La necesidad es doble: menos tiempo y más trazabilidad, sin delegar la decisión. La propuesta fija seis requerimientos: decisión humana registrada con motivo y fecha; afirmaciones rastreables hasta su fuente; fichas en inglés; solo datos autorizados; inferencia de hasta 30 USD mensuales; y tiempo y calidad medibles frente al proceso manual. **[PENDIENTE: validar la Figura 1 con el operador y pasarla a BPMN; integrar y verificar el registro de dos semanas del autor, declarado como reconstrucción; captura fechada de YouTube Analytics.]**

## Descripción de la organización

Bistec LLC, sociedad de responsabilidad limitada de Wyoming, Estados Unidos, dedicada a software y productos digitales, auspicia el proyecto (Anexo 1). SingulariDev es su unidad de formación y comunidad en línea sobre IA aplicada, y Miguel Ángel Brito Espejo representa a ambas. No hay misión ni visión formales; el propósito, según la propuesta, es atraer desde YouTube a emprendedores unipersonales angloparlantes hacia una comunidad en Skool. Una persona cumple cuatro funciones (Figura 2); la necesidad ocurre en la de investigación y planificación editorial.

**Figura 2**

*Organigrama funcional de SingulariDev*

![Nota. Reconstrucción funcional de la Tarea 8 a partir de la propuesta; una persona cumple las cuatro funciones.](archive/output/tareas/evidencias-tarea-08/figura-2-organigrama-funcional.png)

El canal Miguelito Hacks tiene audiencia mayoritariamente hispanohablante; el piloto de tres videos en inglés no tiene evidencia de publicación y la comunidad en Skool no tiene historial. El 20 de octubre el autor acotó la validación a contenido para programadores en inglés y decidió desarrollar el producto con un solo código para la tesis y su uso posterior, con Bistec LLC como titular; su modelo de negocio queda fuera del proyecto. El 30 de octubre decidió que ese producto es Earlyscript (7.2). **[PENDIENTE: sector formal registrado; misión y visión; estado de la comunidad.]**

# Análisis de posibles soluciones

## Identificación y selección de la mejor solución

Las dos alternativas usan modelos de lenguaje y difieren en dónde se calcula la prioridad y cuánto control conserva el operador. En la **alternativa A, agente generalista**, un agente con herramientas consulta fuentes, interpreta señales y redacta; se construye rápido, pero su priorización queda implícita y puede cambiar entre ejecuciones. La **alternativa B, arnés híbrido y modular**, separa adaptadores, almacén de evidencia, análisis determinista y generación: la puntuación se recalcula desde datos y pesos registrados, y el operador acepta, edita o rechaza cada ficha. La Tabla 2 las compara con ocho características de ISO/IEC 25059:2023, el modelo de calidad para sistemas de IA que extiende ISO/IEC 25010 (International Organization for Standardization [ISO] e International Electrotechnical Commission [IEC], 2023). Es una estimación previa del autor, de 1 (sin mecanismo claro) a 5 (cobertura explícita y verificable).

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

Se eligió B: conserva fuentes, exige aprobación y permite revertir, aunque el modelo y las APIs pueden fallar. Earlywindow la materializó con un motor determinista sin modelo de lenguaje y un agente acotado al expediente que elige el operador; Earlyscript conserva esa separación: el motor no usa modelo, el asistente solo lee y redacta, y la decisión se graba por un camino que el modelo no puede invocar (7.2). Earlyscript se parece en superficie a la alternativa A, porque el operador conversa con un agente en un hilo; la diferencia es que la prioridad la calcula el motor con pesos registrados, el agente no puntúa ni reordena y cada guion es un archivo con versiones y citas verificables. No se construyó A para compararla sobre las mismas tareas; dentro de B se compararon las alternativas técnicas de la Tabla 3. **[PENDIENTE: tabla complementaria de viabilidad, costo, innovación, impacto y tiempo que pide la guía del tutor, si confirma que complementa la matriz aprobada.]**

**Tabla 3**

*Alternativas técnicas comparadas dentro de la solución*

| Comparación | Qué se fija | Resultado al 26 de octubre | Alcance |
|---|---|---|---|
| BERTopic frente a K-means | Mismos 79 textos de X, embeddings y UMAP por semilla (Tarea 6) | K-means 5 provisional; BERTopic sin la cobertura de agrupamiento mínima | Evidencia histórica sobre X |
| Fórmula ponderada frente a orden por volumen `items_7d` | Mismas candidatas, cortes y etiqueta | Con v0.01 y con v0.02 la línea base gana o empata (7.3) | Dos órdenes de las mismas señales, no dos sistemas |
| Qwen3-Embedding-0.6B local frente a text-embedding-3-large | Mismos textos y algoritmos | No ejecutada: exigía gasto y clave (Anexo 3) | No demuestra superioridad ni equivalencia |
| Motor de Earlywindow frente a motor portado a Earlyscript | Mismo corpus, corte y perfil; 45.557 textos | 19 expedientes frente a 18; coinciden 3 de 5 en el top 5 por volumen y 1 de 5 en el ponderado. Hipótesis: vectores de Linux frente a macOS (coseno mediano 0,965) | Mismo método en dos plataformas, no dos métodos |

## Impacto del proyecto en la sociedad

Los impactos son esperados, no observados. Económico: reducir el esfuerzo del único operador. Social: investigar con evidencia enlazada, con riesgo de amplificar anuncios de grandes proveedores (Tarea 7; Anexo 4, c10). Tecnológico: integra técnicas existentes y no aporta un algoritmo nuevo. Legal: los textos de terceros están sujetos a los términos de cada fuente y a la protección de datos (Ley Orgánica de Protección de Datos Personales, 2021). Ambiental: no se midió energía. Los riesgos éticos se tratan en 7.4. No se identificó un efecto político directo. **[PENDIENTE: lugar de operación y obligaciones legales por tratamiento; respuesta de Y Combinator sobre uso comercial.]**

# Objetivos

Los objetivos conservan las metas de la Tarea 1; el objetivo 3 incorpora la comparación de embeddings de la Tarea 3. Su estado está en el capítulo 8.

## Objetivo General

Desarrollar y validar, entre agosto y noviembre de 2026, un arnés agéntico con aprobación humana que reduzca al menos 40 % el tiempo mediano de preparación de fichas en inglés para SingulariDev.

El alcance original de la meta se mantiene en el método: detección temporal de señales, agrupamiento semántico y modelos de lenguaje al servicio de la adquisición de miembros. La meta no se ha alcanzado ni medido al corte.

## Objetivos Específicos

1. Caracterizar el proceso manual de investigación y selección de ideas mediante un diagrama del flujo actual, un registro de carga de al menos dos semanas y seis fichas manuales, para sustituir la estimación de 20 horas semanales por una línea base observada.
2. Diseñar la arquitectura, los permisos y los criterios de aceptación del arnés, y documentar la comparación previa de dos alternativas con criterios de ISO/IEC 25059:2023, para justificar la solución seleccionada.
3. Implementar un flujo reproducible que recolecte evidencia de fuentes autorizadas con su procedencia y compare BERTopic con K-means, y Qwen3-Embedding-0.6B con text-embedding-3-large, sobre los mismos textos, para elegir el agrupamiento con métricas registradas.
4. Integrar un agente de código con herramientas acotadas y una interfaz gráfica para generar al menos seis fichas en inglés con evidencia, registrar cada decisión humana con su motivo y demostrar una personalización reversible. La Tarea 1 nombraba a Pi coding agent; Earlywindow lo usó y Earlyscript usa los agentes de T3 Code (Claude Code y Codex), desviación registrada en el Anexo 3.
5. Evaluar el prototipo frente al proceso manual con seis pares de temas y dos revisores externos ciegos, para determinar si alcanza 40 % de reducción del tiempo mediano, 90 % de respaldo factual y utilidad media de 4 sobre 5, y publicar tres videos cuyos resultados se reporten sin atribución causal.

La utilidad usa las anclas de la Tarea 1: 1, no utilizable; 2, cambios mayores; 3, revisión sustancial; 4, cambios menores; 5, lista para decidir. La meta se calcula con los dos revisores externos y la valoración del autor se informa aparte. El tiempo de la meta es el tiempo activo desde el inicio de la búsqueda hasta la decisión; Earlywindow medía solo el tramo desde el expediente abierto hasta la decisión, y Earlyscript mide por etapas, explorar, leer, escribir y decidir, con un reloj con pausa en el hilo de video (7.2 y Anexo 3). **[PENDIENTE: calibrar la rúbrica con los revisores; respuesta del tutor sobre las desviaciones de los objetivos 3, 4 y 5.]**

# Alcance

## Alcance de la solución seleccionada

El alcance cambió cuatro veces (Tabla 4). El cambio de corpus del 20 y 21 de octubre y el cambio de producto del 30 están pendientes de comunicar al tutor (7.1).

**Tabla 4**

*Evolución del alcance*

| Elemento | Acordado en la Tarea 3 | Tareas 5 a 7 | Earlywindow (21 a 26 oct.) | Earlyscript (30 y 31 oct.) |
|---|---|---|---|---|
| Fuentes | X principal; Reddit con permiso; YouTube de respaldo | 99 publicaciones de X | Hacker News y GitHub, 50 días, corpus congelado | Las mismas dos fuentes, con captura en vivo idempotente; corrida fresca de 28 días |
| Embeddings | Qwen3 local y text-embedding-3-large | Qwen3-Embedding-0.6B en Python | Qwen3-Embedding-0.6B ONNX q8 en Transformers.js, macOS | El mismo modelo en Linux, con caché por plataforma |
| Agrupamiento | BERTopic y K-means | K-means 10, K-means 5 y BERTopic | Apilado incremental por coseno, umbral 0,70 | El mismo apilado, 9,7 veces más rápido con resultado idéntico bit a bit |
| Plataforma | Interfaz gráfica sobre Pi | Servidor Node con Pi por RPC | Escritorio macOS en Electron, Pi 1.3.0 como librería, SQLite | Fork de T3 Code: servidor Node, interfaz web y Electron para empaquetar; base `editorial.sqlite` propia |
| Modelo de lenguaje | Proveedor intercambiable | gpt-5.5 y GPT-6.1 Sol | `openai/gpt-6.1-sol` con la cuenta de ChatGPT del operador | Agentes instalados en la máquina (Claude Code, Codex); títulos y resúmenes con el modelo barato del proveedor |
| Unidad de trabajo | Ficha de contenido | Ficha en inglés de ocho apartados | Expediente y ficha generada por el agente | Ficha de tendencia de lectura y guion de video como archivo Markdown con versiones y citas |
| Medición | Cronómetro externo | Ensayo de la Tarea 6 | Tiempo, decisión, motivo y utilidad en la aplicación | Reloj por etapas con pausa, decisión con utilidad y motivo, espacio Resultados |

**Qué aborda.** Los cinco objetivos, con la retrospectiva y la robustez del motor como evidencia técnica añadida. **Qué no aborda.** Publicación autónoma; generación final de videos o imágenes; CRM, facturación, multiusuario o modelo de negocio; predicción de conversión, abandono o valor de vida del cliente; aprendizaje de pesos por retroalimentación; comentarios, transcripciones y otros idiomas; atribución causal de resultados comerciales; las funciones de T3 Code ajenas al estudio (terminal, solicitudes de cambio, proveedores de control de versiones en la nube, acceso remoto, relay), escondidas por banderas y no borradas.

**Supuestos.** La cercanía entre embeddings refleja temas útiles, sin evaluación humana en el corpus nuevo. Hacker News y GitHub siguen sin tarifa, y la gratuidad no acredita permiso para todo tratamiento. Los agentes de código instalados en la máquina del operador siguen disponibles con su suscripción. Habrá dos revisores calibrados.

**Periodicidad.** La corrida es diaria por diseño. Hecho: en Earlyscript existe `engine collect` idempotente y `engine run`; el programador nocturno está en construcción, sin fusionar. Earlywindow tenía `npm run daily` y un instalador de launchd nunca instalado.

## Limitaciones y restricciones del proyecto

**Limitaciones del entorno.** La comunidad en inglés no tiene historial, así que los resultados comerciales solo se reportan de forma descriptiva. X cobra cada lectura y su lote pagado no permite evaluar tendencias semanales (7.1). Reddit no tiene autorización documentada. Y Combinator restringe el uso comercial del contenido (Y Combinator, s. f.; 7.4), así que Hacker News se limita a la evaluación local. GitHub solo ofrece estrellas actuales. Hecho: el 91,49 % de las historias de Hacker News no tiene cuerpo. No hay un banco de pruebas para anticipar temas editoriales: BERTrend se validó con casos (Boutaleb et al., 2024) y BackTrend cubre señales científicas (Zhou et al., 2026). Sin dos revisores, la utilidad externa no es evaluable.

**Restricciones del proyecto.** Periodo del 10 de agosto al 15 de noviembre de 2026. Un integrante que desarrolla, opera y es evaluado, mitigado con revisores ciegos. Hasta 30 USD mensuales de inferencia, aparte de X. Aprobación humana antes de usar una ficha (Tabassi, 2023). El producto corre en local; Earlyscript se desarrolla en Linux y se empaqueta para macOS, y su interfaz editorial está en español porque el operador la usa en español, mientras los guiones se escriben en inglés. Tope de 40 solicitudes y 40 herramientas por ejercicio, ampliable de 20 en 20 con decisión registrada. Sin credenciales, corpus ni opiniones de revisores en Git. Orden del autor del 21 de octubre: gana la opción con menos código y un compromiso incumplido se registra como desviación. Hecho: el corpus congelado ocupa 161.681.858 bytes; en Earlywindow la primera corrida tardó 1.888 segundos y la canónica, con caché, 305, en una Mac Apple M4 compartida; en Earlyscript, en un servidor Linux de 22 núcleos, la corrida fresca del 31 de octubre tardó 374 segundos con 6 procesos de embeddings. Los vectores de Linux no reproducen los de macOS (coseno mediano 0,965 para el mismo texto), así que la retrospectiva de 7.3 es un resultado de macOS.

# Planificación y costos del proyecto

Iteraciones semanales con un incremento verificable por entrega: entregable, decisiones fechadas y commit. Desde el 21 de octubre el trabajo técnico se organizó en unidades con prueba observable (U0 a U9 en Earlywindow, U1 a U11 en Earlyscript) y en tareas delegadas a agentes de programación, coordinadas primero con Orca y desde el 30 de octubre desde T3 Code; un modelo trabaja, otro verifica y el primero corrige, y cada decisión tomada en ausencia del autor queda registrada y es reversible. No se usó Scrum ni Kanban formal (Tabla 5).

**Tabla 5**

*Cronograma de 14 semanas, previsto en la Tarea 1 y real al 31 de octubre*

| Semanas de 2026 | Previsto | Real al 31 de octubre |
|---|---|---|
| 1 (10 a 16 ago.) | Observaciones del Comité e instrumentos | Hecho (Tarea 1) |
| 2 a 5 (17 ago. a 13 sep.) | Credenciales, fuentes, línea base manual; arquitectura | Arquitectura hecha (Tarea 3); línea base manual sin iniciar |
| 6 a 8 (14 sep. a 4 oct.) | Recolección; agrupamiento; puntuación; revisores | Con retraso: X el 29 de sep.; ranking provisional; revisores sin identificar |
| 9 a 10 (5 a 18 oct.) | Pi, interfaz, fichas; videos 1 y 2 | Parcial: Tareas 6 y 7; videos sin verificar |
| 11 (19 a 25 oct.) | Prueba ciega; video 3 | Rediseño: S8, spec y Earlywindow U0 a U9; retrospectiva, robustez, seguridad y calidad |
| 12 (26 oct. a 1 nov.) | Análisis y corrección | Verificación de Earlywindow y v0.02 (26); traslado del entorno a un servidor Linux (29); decisión de producto, fork de T3 Code y diez unidades de Earlyscript fusionadas (30 y 31); S10 el 30. Ejercicios sin iniciar |
| 13 a 14 (2 a 15 nov.) | Prototipo reproducible, informe y defensa | **[PENDIENTE: corte del 4 o 5 de nov. para decidir si los ejercicios corren sobre Earlyscript; sesiones de ejercicios; revisores; integración del registro de dos semanas; informe final; defensa probable el 13]** |

Ni el motor de tendencias ni el fork estaban en el cronograma: el motor respondió a que el lote de X no permitía medir tendencias y a que el ranking de la Tarea 5 no medía relevancia (Tarea 7); el fork, a que Earlywindow repetía con menos calidad lo que T3 Code ya resuelve (hilos, proveedores, historial, visor de diferencias) y a que el autor quiere un producto que use después. El trabajo del 30 y 31 de octubre se hizo con agentes de programación coordinados desde T3 Code, con un modelo que implementa, otro que verifica y el primero que corrige; cada unidad tiene rama, informe y veredicto. La evaluación humana, los revisores y los videos son la deuda principal. **[PENDIENTE: cierres de Brightspace de S11 y S12.]**

**Costos.** Un costo desconocido se informa como desconocido, no como cero. API de X: hasta 0,55 USD por 100 publicaciones más una prueba de 10 (Estimación, sin factura). Hacker News, GitHub y embeddings locales: sin tarifa por solicitud (Hecho; sin contar equipo ni energía). Modelo de lenguaje: `cost_usd` nulo con `cost_source = subscription_unknown`, porque la suscripción no tiene precio por solicitud. Servicio de las Tareas 5 y 6: tarifa desconocida. Claude Max, ChatGPT Pro con Codex y Cursor son recursos de desarrollo. Horas del autor: rango del tutor de 25 a 50 USD por hora. **[PENDIENTE: horas registradas por semana; imputación del equipo por depreciación; análisis financiero con TCO; no se calcula retorno mientras no exista línea base de tiempo.]**

# Descripción de estudios realizados

La Tarea 2 revisó diez estudios de 2022 a 2026: tres sobre modelado temático y agrupamiento con embeddings (Grootendorst, 2022; Egger y Yu, 2022; Zhang et al., 2022), tres sobre agentes y generación con citas (Yao et al., 2023; Gao et al., 2023; Min et al., 2023), dos sobre productividad y decisión con IA generativa (Noy y Zhang, 2023; Csaszar et al., 2024) y dos sobre explicaciones y sesgo de popularidad en recomendación (Feng et al., 2026; Klimashevskaia et al., 2024). Ninguno mide utilidad editorial ni adquisición de miembros. El enfoque, el resultado y el límite de cada estudio están en la tabla de `archive/output/tareas/02-estado-del-arte-y-metodologia.md`.

Dos lecciones guiaron el diseño. Un agrupamiento más complejo no es mejor de antemano (Zhang et al., 2022): por eso se compararon BERTopic y K-means y Earlywindow usa un apilado simple. Una cita no garantiza respaldo (Gao et al., 2023; Min et al., 2023): por eso la meta del 90 % cuenta afirmaciones respaldadas. `claims.csv` exporta una fila por cita de la última ficha, y para el 90 % hay que inventariar además las afirmaciones verificables sin cita, porque una afirmación omitida no aparece como no respaldada.

**Detección temporal.** BERTrend (Boutaleb et al., 2024) entrena un modelo por corte, fusiona temas y separa ruido, señal débil y señal fuerte; Earlywindow toma la idea de señales que persisten día a día, sin fusión ni decaimiento. BackTrend (Zhou et al., 2026) evalúa señales científicas, con F1 de 10,1 % para su mejor sistema. Los ciclos de atención se acortan (Crane y Sornette, 2008; Lorenz-Spreen et al., 2019), lo que hace verosímil una ventana corta, coherente con la mediana de dos días de 7.3 sin probarla. El sistema se documenta con una Model Card (Mitchell et al., 2019). Las obras anteriores a 2019 (Shapley, 1953; Hubert y Arabie, 1985; Rousseeuw, 1987; Crane y Sornette, 2008) se citan como fuentes originales de los métodos o hallazgos usados.

**Vacío.** Ningún estudio revisado evalúa el ciclo completo para un operador único (señales de varias fuentes, agrupamiento temporal, ficha con respaldo verificable y decisión registrada) frente al proceso manual. La revisión fue exploratoria. **[PENDIENTE: ampliar la bibliografía sobre utilidad en recomendación de contenido y sesgos de modelos de lenguaje, como pidió el Comité.]**

# Desarrollo del proyecto

El arnés se construyó en tres etapas: tres iteraciones sobre 99 publicaciones de X (Tareas 5 a 7, del 29 de septiembre al 13 de octubre de 2026), Earlywindow sobre Hacker News y GitHub (21 a 26 de octubre) y Earlyscript (30 y 31 de octubre), que porta el motor de Earlywindow a un fork de T3 Code. La etapa sobre X se resume al final de 7.3; Earlywindow aporta el método del motor y los resultados técnicos; Earlyscript es el producto que se evaluará.

## Diseño de la solución

**Enfoque.** Desarrollo tecnológico aplicado con comparación intrausuario (Tarea 1, §6.1): cada iteración fija un protocolo, ejecuta, mide y registra la decisión. Al 31 de octubre están completos el análisis exploratorio, el modelado del motor y su evaluación técnica; la evaluación humana está pendiente y la implementación en entorno real está en curso: el operador usó la vista previa de Earlyscript con la corrida real en la madrugada del 31 y dictó cambios de nombre y de orden que ya están en `main`.

**Principios.** Evidencia: adaptadores de solo lectura con fuente, fecha, URL, texto y cobertura diaria. Cálculo: agrupamiento, series y puntuación deterministas y recalculables. Síntesis: el modelo propone ángulos y redacta, sin puntuar. Decisión: solo el operador aprueba; el agente no puede aprobar, publicar ni escribir en una base. Las órdenes del autor del 21 de octubre fijan que el producto útil prima sobre cada compromiso literal, que gana la opción con menos código y que el motor es reemplazable, mientras el contrato del expediente y la instrumentación son rígidos. El 30 de octubre añadió tres principios para Earlyscript: construir sobre los primitivos de T3 Code (hilos, chat libre, cierre de hilo) sin replantearlos; código aditivo, con enganches de una línea en los archivos de upstream, banderas para esconder funciones y un registro de cada archivo divergente; y un motor rediseñado desde principios escritos, no un enchufe del motor viejo.

**Cambio de corpus.** Hecho: la Tarea 3 acordó X y Reddit; Earlywindow y Earlyscript usan Hacker News y GitHub. Justificación propuesta para el tutor: X cobra cada consulta y el lote pagado reunió 99 publicaciones capturadas en 28 minutos y 37 segundos, insuficientes para evaluar la evolución semanal de tendencias; el acceso de Reddit sigue pendiente; Hacker News aporta historial para la retrospectiva; GitHub aporta metadatos actuales, sin historial de estrellas, y queda fuera de la retrospectiva. El costo es que la población de señales cambia, la Tarea 6 queda como evidencia sobre X y la retrospectiva mide actividad en Hacker News, no utilidad para la audiencia. El uso comercial de Hacker News depende de una aclaración escrita de Y Combinator.

Las otras cinco fuentes decididas el 20 de octubre se pospusieron el 21. Hecho: el 26 se construyeron sus adaptadores (Wikipedia Pageviews, Stack Exchange, arXiv, npm y Bluesky), que están en `main` en un registro único (`src/engine/sources/index.ts`) cuyas fuentes por defecto siguen siendo `hn` y `github`. Ninguno entra en el corpus evaluado ni se portó a Earlyscript. Hecho: el correo al tutor con el cambio de corpus no se ha enviado; su borrador es el informe E28 de la ola 8 y debe ampliarse con el cambio de producto del 30 de octubre (Anexo 3).

**Criterios de evaluación, fijados antes de ejecutar.** Sistema: las metas de la Tarea 1 (capítulo 3); el contraste de seis pares mide en Earlyscript el tiempo por etapa, de modo que compara explorar a mano frente a la bandeja de Tendencias, escribir a mano frente a escribir con asistente sobre el mismo tema, y el proceso completo manual frente al asistido; el tiempo activo desde la búsqueda se informa con el registro de dos semanas. Retrospectiva, definida en el spec del 21 de octubre: precisión en 5 y en 10 frente a la línea base `items_7d` y mediana de días hasta el evento (`lead_days`). Robustez, con los umbrales del curso: una perturbación del 5 % que mueve la salida más del 40 % indica inestabilidad, y un cambio mayor del 20 % en una métrica clave exige actuar. Agrupamiento sobre X: cobertura de agrupamiento de al menos 80 %, silueta coseno válida en cinco semillas (Rousseeuw, 1987), estabilidad ARI (Hubert y Arabie, 1985) y claridad ciega de al menos 3,5 sobre 5. Ninguna métrica técnica mide calidad editorial.

## Desarrollo de la solución

**Earlyscript, el producto final.** Hecho: el 30 de octubre de 2026 el autor clonó T3 Code (T3 Tools, 2026), un estudio de escritorio para agentes de código con licencia MIT, en el commit `aa11ef6783` de ese día, y creó el fork privado Earlyscript en un servidor Forgejo propio, con el upstream de GitHub en solo lectura. T3 Code aporta lo que Earlywindow repetía con menos calidad: hilos de conversación con historial, proveedores de modelos por los agentes instalados en la máquina, un servicio de generación de texto, un navegador integrado, un editor de archivos y un visor de diferencias. Sobre esa base, Earlyscript añade tres espacios en la barra lateral, Hilos, Tendencias y Resultados, al estilo de los espacios de Arc, y una base propia `editorial.sqlite` junto a la de T3. La Figura 3 muestra la ficha de tendencia con título y resumen redactados por el asistente; la Figura 4, la bandeja de Tendencias y la ficha antes de redactar, con su evidencia; la Figura 5, la aplicación nativa en macOS con marca propia.

**Figura 3**

*Ficha de tendencia en Earlyscript, con título y resumen redactados por el asistente sobre la corrida del 19 de octubre*

![Nota. Captura del 31 de octubre de 2026 en `main` 3e4c6c0741, tema claro. El título y los tres párrafos los redactó claude-haiku-5-5 con citas a identificadores de evidencia; los términos del motor, las dos posiciones del ranking, la afinidad con el perfil, la cobertura por fuente y la curva de 28 días son del motor y no cambian.](archive/output/tareas/evidencias-tarea-10/figura-earlyscript-ficha-tendencia.png)

**Figura 4**

*Bandeja del espacio Tendencias y ficha antes de la redacción del asistente, con evidencia enlazada y el bloque "Por qué está aquí"*

![Nota. Captura del 31 de octubre de 2026 en `main`. A la izquierda, la bandeja: cada fila muestra la etiqueta del motor, la fuente, la primera evidencia, publicaciones y autores de siete días, la posición por puntaje y la curva. A la derecha, la misma tendencia de la Figura 3 sin título redactado: evidencia con fecha y autor, y las razones del motor para incluirla.](archive/output/tareas/evidencias-tarea-10/figura-earlyscript-bandeja-tendencias.png)

**Figura 5**

*Earlyscript empaquetado para macOS, con marca propia*

![Nota. Captura del 31 de octubre de 2026 en una Mac mini, aplicación sin firmar compilada desde `main` ed5c3a2903 (455 MiB). Muestra un hilo cerrado de T3 Code con el agente Astra; las funciones editoriales se ven en las Figuras 3 y 4.](archive/output/tareas/evidencias-tarea-10/figura-earlyscript-macos.png)

**Decisiones de experiencia de uso.** Hecho: el 30 de octubre por la tarde el autor validó en pantalla dos maquetas con datos reales de la corrida 2263f7, "Una mañana con Earlyscript" y "Modo manual", y fijó diez decisiones (Tabla 6). Las maquetas sustituyeron la sesión de diseño prevista.

**Tabla 6**

*Decisiones de experiencia de uso validadas por el autor el 30 de octubre de 2026 y su estado en `main` 3e4c6c0741*

| Decisión | Estado |
|---|---|
| Al arrancar, si hay corrida nueva, abrir en Tendencias con el conteo de nuevas; si no, donde se dejó | Aterrizaje en `main` |
| Título de una línea y resumen de tres párrafos por tendencia (qué pasó, por qué importa al canal, qué ángulo de video), una vez por corrida, por el servicio de generación de texto de T3 con el modelo barato del proveedor; marcado "redactado por el asistente"; no cambia el orden ni el puntaje | En `main`; prueba real con claude-haiku-5-5: 3 fichas en 12 a 22 s |
| Orden por defecto: nuevas primero, luego por crecimiento semanal; selector por volumen y por afinidad | En `main` |
| La bandeja de tendencias reutiliza el modelo de bandeja de hilos de T3: no leída, seguir observando (se esconde y vuelve si crece), descartar con motivo (plegada), en producción (con enlace al hilo) | Estados y escritura en `main`; botones y diálogos en rama `es/inbox-actions`, sin fusionar |
| Hasta 10 nuevas visibles; el resto plegado | En `main` |
| Reloj visible arriba a la derecha del hilo de video, con pausa registrada; se detiene en la decisión | Servidor en `main`; pantalla en rama `es/video-thread`, sin fusionar |
| Tercer espacio, Resultados: tiempo por etapa asistido frente a manual, utilidad, citas, bandeja y métricas de video, descriptivo y sin calcular ahorro | En `main`, con estado vacío honesto |
| Métricas del video a mano, en un bloque "Resultado" del hilo cerrado | Servidor en `main`; formulario en `es/video-thread` |
| Modo manual: hilo sin chat ni motor, con tres etapas, Explorar (navegador integrado y captura rápida), Escribir (editor Markdown con versiones) y Decidir (misma grabación que en asistido) | Bloqueo de agentes en hilos manuales en `main`; pantalla sin iniciar |
| Nombre en la interfaz: "Ficha de tendencia" en lugar de "Expediente" | En `main` |

**Componentes de Earlyscript.** La Tabla 7 resume lo fusionado en `main` 3e4c6c0741 al 31 de octubre a las 02:40 UTC. Cada unidad pasó por un ciclo fijo: un modelo implementa en una rama con batería de pruebas completa, un segundo modelo verifica en solo lectura y emite "apto", "apto con correcciones" o "no apto", el primero corrige y el coordinador fusiona. La divergencia respecto de upstream está registrada archivo por archivo en `docs/upstream-divergence.md`, con catorce secciones; en total, 383 archivos cambiados, 31.448 líneas añadidas y 488 quitadas respecto del commit de origen, la mayoría en paquetes y carpetas propios.

**Tabla 7**

*Unidades de Earlyscript fusionadas en `main` 3e4c6c0741 y unidades en rama*

| Unidad | Qué hace | Verificación |
|---|---|---|
| Capa de marca | Nombre, icono, esquema de URL `earlyscript://`, directorio `~/.earlyscript`, puertos y lanzador propios, para convivir con un T3 Code instalado | Sol: no apto, corregido, apto |
| Banderas de funciones | Telemetría, analítica de terceros y comprobación de actualizaciones apagadas; medición en vivo con cero salidas de red; lote A esconde terminal, solicitudes de cambio, proveedores de control de versiones, acceso remoto, relay y T3 Connect, bloqueando en el servidor y no solo en la interfaz | Sol: no apto, corregido, apto |
| Batería en Linux | Scripts `es:*` que reparten las pruebas como el CI de upstream; batería completa en 630 s en un servidor de 22 núcleos | Sol: apto con correcciones |
| Motor de tendencias, paso 1 | Paquetes `editorial-contracts` y `trend-engine`, sin dependencia de T3: corpus `corpus/1` por día y fuente con manifiesto SHA-256, corte antes de abrir archivos, Qwen3-Embedding-0.6B ONNX q8 en procesos hijo con caché por plataforma, apilado por coseno 0,70, dos rankings, cobertura por fuente y `run.json` con huella lógica; `engine check` reproduce una corrida | Sol: no apto, corregido, apto con correcciones bajas; huella reproducida tres veces |
| Motor, rendimiento | Centroides en un arreglo contiguo y poda por la cota de Cauchy-Schwarz: apilado de 593 a 61 s, señales idénticas bit a bit a la versión directa (401 casos) | Sol: apto con correcciones |
| Fuentes en vivo | Adaptadores de Hacker News (Algolia) y GitHub con `engine collect` idempotente, pausas, reintentos y bloqueo por cuota; captura real de 1.210 historias en 3,4 s | Sol: apto con correcciones |
| Validador del guion | Paquete `editorial-script`: estructura de encabezados, citas y mapa de afirmaciones del guion Markdown, con CLI `check` | Sol: apto con correcciones |
| Base editorial | `editorial.sqlite` con migraciones 001 a 005: estados de bandeja, decisiones, versiones del guion, capturas, resultados, corridas importadas y presentaciones; servicios de comando, lectura, reloj de trabajo e hilo editorial; importador idempotente de corridas | Sol: apto con correcciones; importador no apto, corregido, apto |
| Espacio Tendencias | Barra lateral con pestañas Hilos, Tendencias y Resultados; lista; ficha de tendencia con evidencia enlazada, cobertura y curva; rutas propias y aterrizaje | Astra: no apto, corregido, apto |
| Título y resumen | Operación `generateTrendPresentation` en el servicio de generación de texto, hash con versión del prompt, estado "desactualizado" si cambia la entrada, botón para redactar toda la corrida | Sol y Astra: apto con correcciones, corregido |
| Servidor del hilo de video | `createVideo` desde una tendencia, política que impide que un agente actúe en un hilo manual, versiones del guion con hash y herramienta MCP `script_check` | Astra: no apto, corregido, apto |
| Espacio Resultados | Agregados por modo y etapa con mediana, rango intercuartílico y n; utilidad; citas; bandeja; tabla de decisiones; sin la palabra "ahorro" | Sol: apto con correcciones, corregido |
| Marca nativa macOS | Iconos, cadenas, permisos y ZIP propios; aplicación de 455 MiB sin firmar que arranca en 3 s | Sol: apto con correcciones, corregido |
| **En rama, sin fusionar** | Lector del formato nativo del motor (Sol: no apto, en corrección); bandeja con las tres salidas activas; pantalla del hilo de video con reloj, guion y decisión; modo manual; corrida nocturna con programador | No presentar como hechas |

**Lo que Earlyscript conserva de Earlywindow y lo que no.** Conserva el corte temporal, el corpus por hash y por día, la cobertura por fuente, Qwen local, el apilado por cercanía, el expediente con evidencia, los dos rankings y las huellas de reproducibilidad; el motor porta `engine.v0.02` con la procedencia en la cabecera de cada archivo. No conserva la aplicación Electron propia, el agente Pi con fases, `app.sqlite`, el instalador de launchd ni la ventana y sus vistas: eso lo da T3 Code o se rehace sobre él. La ficha de contenido de ocho apartados generada por el agente se sustituye por un guion que escribe el operador en un archivo Markdown, con o sin asistente, y que el validador comprueba.

**Arquitectura en dos capas (Earlywindow, conservada en el motor).** Un **motor de tendencias** determinista, sin modelo de lenguaje, responde qué se mueve y desde cuándo sobre un corpus congelado. Un **agente investigador** responde por qué importa, solo sobre el expediente que abre el operador. El **expediente** `dossier/1` es el contrato entre ambos, con esquema JSON rígido: versión y huellas de la corrida, perfil, señal y etapa, curva diaria de hasta 28 días (`curve_days`, distinta de los 30 días de `active_days`), desglose de la puntuación, cobertura por fuente, de una a diez evidencias con enlace y fecha (`thin` si son menos de cinco) y huecos de datos. Un cambio incompatible exige `dossier/2`. La Tabla 8 resume los componentes de Earlywindow.

**Tabla 8**

*Componentes de Earlywindow en `main` 47c7d4d*

| Componente | Función | Implementación |
|---|---|---|
| Recolector | Historias diarias de HN y repositorios nuevos de GitHub con 20 estrellas o más; cada día queda `complete`, `partial`, `unavailable` o `rate_limited` | `scripts/collect.ts`; registro `SOURCES` de siete fuentes |
| Corpus y caché | JSONL por fuente y día con manifiesto SHA-256; vectores por huella de configuración y texto | `~/earlywindow-data/` |
| Motor 0.01 | Limpieza, embeddings, apilado, series, etapa, perfil, puntuación y hasta 20 expedientes | `src/engine/run.ts`; `engine.v0.01` histórica y `engine.v0.02` para la evaluación |
| Aplicación | IPC tipado, única escritura en `app.sqlite`; interfaz en `sandbox` sin Node ni secretos | `src/main/`, `src/renderer/` |
| Agente | Una sesión de Pi por expediente en un `utilityProcess`, con fases y tope en el host | `src/worker/`; `researcher.v1` por defecto y `researcher.v2` opcional; tope mensual con clave de API |
| Exportación y congelado | Copia privada, paquete compartible, hoja de afirmaciones y paquete reconstruible | `scripts/export.ts`, `freeze.ts`; `--share` con lista blanca de columnas, `--blind` y `package:mac` |
| Retrospectiva y robustez | Cuatro cortes con línea base y cinco familias de perturbación | `scripts/backtest.ts`, `scripts/robustness/` |

Las capturas fechadas de Earlyscript están en las Figuras 3 a 5 y en `evidencias-tarea-10/`; la figura de componentes de Earlywindow se reemplaza por la Tabla 8, porque la aplicación de escritorio de Earlywindow no es el producto final.

**Método del motor 0.01** (`config/engine.v0.01.json`). (1) Texto: título más 1.000 caracteres del cuerpo, sin HTML. (2) Idioma: se excluye el texto con menos del 90 % de letras ASCII, una aproximación y no una identificación del inglés. (3) Duplicados: de dos historias con la misma URL queda la más antigua. (4) Embedding: `onnx-community/Qwen3-Embedding-0.6B-ONNX`, revisión `c25a394` (onnx-community, s. f.), conversión ONNX del modelo de Qwen (s. f.), q8, CPU, lote 1, pooling `last_token`, 1.024 dimensiones. (5) Apilado: en orden de publicación, cada ítem se une a la señal activa (con un ítem en los últimos 30 días) de mayor coseno si supera estrictamente 0,70, o abre una señal; sin fusión. (6) Serie diaria de ítems, autores y fuentes. (7) Etapa, con g = ln((ítems de 7 días + 1) / (ítems de los 7 previos + 1)): `growing` si g ≥ 0,69 con al menos tres ítems recientes; `fading` (decreciente) si g ≤ −0,69; `steady` en otro caso; `unclassified` si falta un día en los 14 previos. (8) Perfil: coseno máximo con los temas incluidos de al menos `include_min` (0,50) y con los excluidos bajo 0,60. (9) Puntuación con referencia cero: 0,5 × crecimiento + 0,2 × ln(1 + autores de 7 días) + 0,3 × afinidad, con cada contribución en el expediente. (10) Hasta 20 expedientes `growing` que pasan el perfil. Los umbrales se declaran como hipótesis en cada `run.json`.

**Configuración v0.02.** Hecho: el 26 de octubre el autor adoptó `engine.v0.02` para la evaluación. Solo sube `include_min` a 0,60, a partir del análisis c10, en el que un juicio de modelo, no una verdad de referencia, clasificó como ajenos al canal 8 de los 20 expedientes de v0.01 y 3 de los 18 de v0.02. La corrida `run_20261019_20261027T003754_2263f7` (commit d8f3079) terminó `ok` con las mismas 13.701 señales y emitió 18 expedientes: 11 conservados, 7 nuevos y 9 retirados, como predijo c10; `enrich` obtuvo texto en 143 de 170 URL. v0.01 se conserva porque la citan la retrospectiva y la corrida canónica. C16 repitió retrospectiva y robustez con v0.02.

**Agente sobre Pi.** Librería de Pi coding agent 1.3.0 en un `utilityProcess`, sin extensiones ni contexto del usuario (Zechner, 2026), en un ciclo ReAct (Yao et al., 2023) de dos fases: `propose` entrega dos o tres ángulos con evidencia o una abstención, y `draft` una ficha en inglés con ocho apartados (Audience, Need, Value proposition, Angle, Title, Narrative structure, Evidence y Limitations). El host rechaza identificadores ausentes del expediente y fichas sin ángulo aceptado. `read_item` devuelve hasta 4.000 caracteres del ítem y 4.000 del artículo, descargado después del corte. El tope se aplica en el host; al agotarse, **Continue** registra una decisión de ampliación del tope con motivo y suma 20 y 20. Los textos recuperados se tratan como datos, no como instrucciones.

**Prompts.** Cada corrida registra la huella del prompt. `researcher.v1` (`main`) no llamó a `read_item` en seis recorridos reales y se apoyó en titulares; ese caso justificó `researcher.v2` (C13, en `main`), que pide leer ítems y artículos y distingue titular de texto leído. Se activa con `EARLYWINDOW_PROMPT=researcher.v2`; v1 sigue por defecto. En Earlyscript esta decisión cambia de naturaleza: el agente no redacta la ficha con un prompt fijo, sino que el operador escribe el guion en un hilo de T3 Code con el agente que elija; el prompt que se fija antes del primer ejercicio es el de títulos y resúmenes (v3) y la versión del agente y del modelo quedan registradas por T3 en cada hilo.

**Instrumentación, la parte rígida.** En modo asistido, el reloj monotónico empieza cuando el worker del agente está listo y se construye el ejercicio; no incluye todo el tiempo desde el clic en **Open** ni la búsqueda previa, y el origen debe declararse también en modo manual. La decisión terminal guarda acción (`accept`, `edit`, `reject` o `defer`), motivo obligatorio, utilidad de 1 a 5, actor, versiones, corrida del motor, `elapsed_ms` y `blurred_ms` (tiempo sin foco); cerrar sin decidir deja el ejercicio abandonado. El modo manual usa el mismo expediente, plantilla, reloj y decisión, sin agente. `edit` guarda la edición como versión hija, dentro del reloj (C20). Hecho (C28 y C29): la ventana en `main` abre cada ejercicio sin utilidad preseleccionada y exige un motivo de al menos tres caracteres antes de decidir. Cada corrida guarda en `run.json` corte, versiones, huellas, commit, exclusiones y estado, con una huella lógica SHA-256 de señales, series y expedientes. Hecho, en `ew/integration` y pendiente de verificación de Sol (G05): tras ajustar los colores de la ventana, una auditoría con la fórmula de contraste de WCAG 2.x no encontró texto bajo el nivel AA en las cuatro vistas, a 1.100 y 1.440 px, en tema claro y oscuro.

**Datos.** Hecho: historias de HN y repositorios de GitHub del 30 de agosto al 18 de octubre de 2026, recolectados con las APIs de Algolia y de GitHub sin autenticación, con pausas. HN aporta 49.784 ítems en 50 días `complete`, exhaustivos respecto del índice; GitHub, 678 en 50 días `partial`, porque guarda 100 repositorios por consulta ordenados por estrellas actuales. Huella `sha256:5bf2d88a…177b`. Se excluyeron 121 ítems por idioma, 114 de GitHub, y 4.784 duplicados; quedaron 45.557 textos. Los extractos se recortan a 500 caracteres. `enrich` descarga los artículos enlazados en la corrida de v0.02, no en la canónica; su efecto sobre las fichas es una hipótesis.

**Alternativa seleccionada y tecnologías.** La fórmula se comparó con una línea base que ordena las mismas candidatas por ítems de los siete días previos (`items_7d`); la comparación de agrupadores no se portó a TypeScript (Anexo 3). Se mantiene la fórmula aunque la línea base gane: su desglose es visible en cada expediente, la línea base solo reordena lo que el motor ya filtró, y 16 frente a 18 aciertos en las cinco primeras posiciones, con cortes solapados, no permiten elegir con seguridad. Hecho: Earlyscript muestra en cada ficha la posición por volumen y por puntaje (Figura 3), como pedía la recomendación del 26 de octubre. Electron y TypeScript, porque Pi corre en Node; `node:sqlite`, con un archivo por almacén; Transformers.js en CPU, para no mantener otro lenguaje; apilado frente a BERTopic, porque cada asignación se explica con un coseno; Pi, por su sesión persistente y abstracción de proveedor.

**Versiones.** Hecho: macOS 27 en Apple M4 de 24 GB; Node 24.18.0; Electron 45.0.0; TypeScript 7.0.2; SQLite vía `node:sqlite`, con 3.53.1 en el manifiesto del ensayo de congelado reconstruido con Node 24.18.0 (la del runtime de Electron no se identificó); Pi coding agent 1.3.0 con `openai/gpt-6.1-sol` por OAuth; `@huggingface/transformers` 4.3.1 y `onnxruntime-node` 1.30.0. No se usó low-code ni no-code, porque el producto exige ejecución local y huellas por corrida. Los asistentes de programación (Claude Code con Opus 5.5 y Fable 5.1; Codex con GPT-6 Astra y GPT-6.1 Sol; coordinados con Orca hasta el 26 de octubre y desde T3 Code después) fueron recursos de desarrollo, no parte del sistema. Hecho, Earlyscript: Node 26.12.1, pnpm 12.14.0, TypeScript y Electron de T3 Code en `aa11ef6783`; el servidor en Linux (Debian 13) y el empaquetado en macOS. Hecho, en `ew/integration` y pendiente de verificación de Sol (G10): `docs/EXPERIMENTS.md` lista los 66 briefs de desarrollo con su asistente y commits, y `docs/CHANGELOG.md` registra fecha, SHA, autor y verificación de cada hito desde `d71dda2`. **[PENDIENTE: cita APA del uso de IA generativa según la política de la UDLA.]**

**Pruebas.** Hecho, batería del coordinador sobre `47c7d4d`, con salida 0 en todos los comandos: `npm test` 18; agente 49; motor 79, sin `todo`; exportación 15; fuentes 49 y 1 omitida, la prueba en vivo; retrospectiva 10; `corpus:verify` con la huella original; `E2E OK` con el fixture. C29 añadió `E2E OK` con 64 comprobaciones sobre la corrida de v0.02, `SMOKE OK` y `MANUAL WINDOW OK`. La última corrida de `test:embed` es de C19, con 7 pruebas en un commit anterior. Verifican contratos y flujos, no calidad editorial.

**Reproducibilidad.** Repositorio Git local, `main` en `47c7d4d`, sin remoto, con licencia de evaluación académica de Bistec LLC para que el tutor y el tribunal lean, ejecuten y verifiquen. El README documenta instalación, recolección, motor, ventana, exportación, retrospectiva y verificación. Hecho: el checkout de evaluación `ew-eval` está congelado en `47c7d4d`, compilado y con árbol limpio, y la guía de los ejercicios prohíbe compilar o cambiar de commit en él. `npm run freeze` copia corpus, base de ejercicios, corridas y configuraciones con huellas, y `freeze:verify` reconstruye cada corrida. Hecho: el ensayo del 26 empaquetó 295 archivos y 189.541.609 bytes con una base simulada y terminó `FREEZE VERIFY OK` con la huella de la corrida canónica. Hecho (C24): `npm run package:mac` generó desde `fdd986b` una `Earlywindow.app` de 529 MB con firma ad hoc, sin Developer ID ni notarización, que arrancó la prueba de SQLite; nadie la probó con el proveedor real. Hecho (G02): un clon limpio de `main` en `b48de89`, siguiendo solo el README, instaló, compiló, pasó la batería, reprodujo la corrida 2263f7 con los mismos `config_hash`, `corpus_hash` y `logical_hash` y terminó `FREEZE VERIFY OK`; los identificadores de expediente difieren por diseño. El README que documenta esa comparación y `npm run engine:discard`, que marca una corrida como descartada sin borrarla (G10), están en `ew/integration`, pendientes de verificación de Sol. Hecho, Earlyscript: repositorios privados de la tesis, de Earlywindow y de Earlyscript en el Forgejo del auspiciante (`git.r.biste.cc/miguel/tesis`, `/earlywindow` y `/earlyscript`), con `main` de Earlyscript en `3e4c6c0741`; los entregables de esta tarea (este documento, sus evidencias y los informes previos) se publican en la rama `tarea-10` del repositorio público https://github.com/mickroplastics/tesis, sin credenciales, corpus, correos ni opiniones de revisores; un clon en un segundo servidor instaló y compiló desde cero (39 paquetes, 38 archivos de prueba) y la corrida fresca `5e57bf` pasó `engine check`. Ninguno de los dos productos cabe en 20 MB. **[PENDIENTE: acceso de lectura efectivo del tutor y del tribunal a los repositorios o a un paquete; README de Earlyscript con instalación paso a paso para un tercero; video de la demo de tres minutos sobre Earlyscript.]**

## Resultados y Discusión.

Primero se presentan los resultados técnicos del motor (medidos en Earlywindow y, para la corrida fresca, en Earlyscript) y después los de la etapa sobre X. La evaluación humana no se ha hecho. El espacio Resultados de Earlyscript existe, pero solo mostró datos de prueba sembrados (Figura 6); no hay decisiones reales.

**Corrida canónica.** Hecho, `run_20261019_20261021T201022_fb1bd2`, corte del 19 de octubre, `engine.v0.01`: 13.701 señales, 86 `growing`, 11.922 `steady`, 1.693 `fading` y ninguna `unclassified`; 3.074 pasan el perfil y se emitieron 20 expedientes en 305,1 segundos; huella lógica `sha256:36ed7715…c518`. Según U6 y U9, el 89,25 % de las señales tiene un solo ítem, la mayor reúne 2.830 ítems bajo `video don life world` y 168 de las 177 evidencias tienen extracto vacío. **Interpretación.** El motor aísla señales en crecimiento en cinco minutos, pero la mayoría de los grupos son aislados, algunos mezclan temas y gran parte de la evidencia es un título. Un expediente acredita de dónde viene una señal, no que el artículo respalde la ficha.

**Corrida fresca en Earlyscript.** Hecho, `run_20261031_20261031T003855_5e57bf`, corte del 31 de octubre de 2026 a las 00:00 UTC, motor `trend-engine` 0.1.0 con la configuración `earlyscript.engine.v1` (equivalente a `engine.v0.02`: `include_min` 0,60), ejecutada en Linux con 6 procesos de embeddings: 28.311 historias de Hacker News en 28 días completos (3 a 30 de octubre) y 282 repositorios de GitHub en 28 días parciales, capturados en vivo; 26.037 textos embebidos tras excluir 55 por idioma y 2.501 duplicados; 8.776 señales, 99 `growing`, 6.576 `steady` y 2.101 `fading`; 251 pasan el perfil y 15 son elegibles; 374 segundos; huella lógica `sha256:4be4331a…`; `engine check` correcto. Las cinco primeras por volumen son "markets money street wall" (25 publicaciones de 24 autores en siete días), "anthropic ipo filing valuation", "workers job jobs work", "saas agent bootstrapped build" y "china american bubble burst"; por puntaje ponderado, "workers job jobs work" sube a la primera posición y "code read don still" a la tercera. **Interpretación.** El motor portado corre de punta a punta con datos frescos y en otra plataforma, con la misma clase de resultado que en Earlywindow: etiquetas por términos difíciles de leer, que motivaron los títulos redactados por el asistente, y señales cuya afinidad con el canal es moderada (0,60 a 0,76). La corrida no se cargó aún en la vista previa porque el lector del formato nativo está en rama; la Figura 3 usa la corrida del 19 de octubre importada desde el formato de Earlywindow.

**Prueba retrospectiva.** El motor se ejecutó a ciegas, solo con HN y sin ajuste, en cortes del 13, 20 y 27 de septiembre y 4 de octubre. Las historias de los 14 días siguientes se asignaron a cada candidata por coseno mayor que 0,70 contra su centroide congelado; una candidata es positiva el primer día en que acumula cinco historias de dos autores, y `lead_days` cuenta los días hasta ese evento. El análisis c04 añadió tres variantes de etiqueta, exploratorias porque se definieron tras ver la saturación (Tabla 9).

**Tabla 9**

*Precisión retrospectiva de la fórmula frente al orden por volumen, por corte, configuración y variante de etiqueta*

| Caso | Positivas sobre candidatas | P@5 fórmula / volumen | P@10 fórmula / volumen | Mediana de días hasta el evento |
|---|---:|---:|---:|---:|
| v0.01, 13 de sep. | 19 de 20 | 0,80 / 1,00 | 0,90 / 1,00 | 1 |
| v0.01, 20 de sep. | 13 de 20 | 0,80 / 1,00 | 0,80 / 0,90 | 1 |
| v0.01, 27 de sep. | 18 de 20 | 0,80 / 0,80 | 0,90 / 0,90 | 2 |
| v0.01, 4 de oct. | 18 de 20 | 0,80 / 0,80 | 0,90 / 0,90 | 1,5 |
| Agregado v0.01 | 68 de 80 | 0,80 / 0,90 | 0,875 / 0,925 | 2 |
| Agregado v0.02 | 64 de 67 | 0,95 / 1,00 | 0,95 / 0,975 | 1 |
| Variante: sin cruces el día del corte | 52 de 64 | 0,80 / 0,85 | 0,85 / 0,825 | 3 / 2 |
| Variante: crecimiento al doble | 2 de 80 | 0 / 0 | 0 / 0 | No evaluable |
| Variante: diez historias y tres autores | 59 de 80 | 0,75 / 0,90 | 0,75 / 0,825 | 2 / 2 |

Notas. Fuentes: `backtest-eval-1/backtest.md` para v0.01, que redondea los agregados de P@10 a 0,88 y 0,92, y `backtest-eval-2/backtest.json` e informe C16 para v0.02, cuyos cortes del 20 de septiembre y 4 de octubre emiten 12 y 15 candidatas; P@k usa `min(k, candidatas)`. La precisión agregada es la media de los cortes; la mediana agregada reúne todas las positivas. Las variantes usan v0.01 y dan la mediana de las cinco y las diez primeras de la fórmula (1 y 2 con la etiqueta original). Las 80 filas son 72 señales con ventanas solapadas, no observaciones independientes; no hay intervalo de confianza.

**Interpretación.** La fórmula no supera a la línea base: pierde en los dos primeros cortes y empata en los dos últimos. La etiqueta casi se satura y 16 positivas cruzan el umbral el día del corte; sin esos cruces la fórmula gana solo en P@10, por 0,025, y ninguna variante da una mediana de siete o más días. La mediana mide actividad mínima en HN, no interés de la audiencia. **La hipótesis de avisar una o dos semanas antes no queda respaldada por el motor 0.01.** Con v0.02 (Hecho, C16) las positivas con siete o más días bajan de 9 a 2, ninguna variante invierte la conclusión y la fórmula no gana en ningún corte. Como 0,60 se eligió mirando el corte del 19 de octubre, esa retrospectiva no es independiente, y con v0.02 la anticipación queda menos respaldada. Hipótesis de C16: el umbral alto filtra hacia temas que ya tienen volumen. Este motor no anticipa con estos datos; eso no prueba que ninguno pueda.

**Robustez.** Las cinco familias del spec se ejecutaron el 22 de octubre con semilla fija y sin proveedor real; C16 repitió el 26 con v0.02 las que dependen de la configuración (Tabla 10).

**Tabla 10**

*Pruebas de robustez de Earlywindow con `engine.v0.01` y `engine.v0.02`*

| Familia y perturbación | Efecto con v0.01 | Efecto con v0.02 (C16) | Lectura con los umbrales del curso |
|---|---|---|---|
| Pesos (c05): ±5, ±10 y ±20 % por peso; 90 escenarios | Tau de Kendall mínima 0,918; con ±5 % se movió como máximo el 25,6 % de las candidatas; 26 escenarios movieron más del 20 % | Ningún escenario supera el umbral de actuación; con ±5 %, máximo 20 % | Estable con 5 %; el orden interno exacto no es una certeza |
| Umbral de apilado (c06): 0,65 y 0,75 frente a 0,70 | 7.672 y 23.629 señales; Jaccard de ítems de los expedientes 0,159 y 0,151 | Con 0,65, de 18 a 5 expedientes (72 %), porque solo 77 señales superan `include_min` 0,60; con 0,75, 20 | Sensible al umbral: ±0,05 es ±7,14 % relativo y no corresponde a la regla del 5 %. Hipótesis central |
| Ítems quitados (c07): 5 % y 10 %, semilla fija | Se conservan 12 y 9 de 20 identificadores; tau 0,909 y 0,556 | Al 5 %, el top 10 sustituye 5 de 10 con la semilla de c07 y 2 de 10 con otra | Cerca del 40 % de expedientes perdidos al 5 %, en el límite; el identificador depende del primer ítem |
| Proveedor (c08): 429, 500, vacías y truncadas | Las ocho combinaciones terminan `failed` con motivo, sin ficha parcial; el reintento manual termina `settled` | No repetida | Esperado con proveedor simulado; no prueba fallos reales |
| Drift (c09): 13 de sep. frente a 4 de oct. | 62,09 % de 5.104 señales activas a 30 días y 11,78 % con actividad nueva; Jaccard de etiquetas 0,456 | Idéntico: `include_min` no cambia el apilado | El vocabulario cambia en tres semanas; recalcular a diario |

Notas. La verificación independiente recalculó c06 y c07 desde sus bases SQLite y coinciden. El contraste de drift con el 19 de octubre incorpora GitHub y se interpreta aparte. Un Jaccard bajo mide cambio de membresía, no pérdida de utilidad. La prueba de pesos no vuelve a agrupar: su estabilidad no equivale a estabilidad del motor.

**Interpretación.** La puntuación es robusta a sus pesos; el apilado es sensible a su umbral y a la muestra, y la salida depende de la combinación de umbral de apilado y umbral de perfil. Los expedientes sirven como material de trabajo, pero ni la lista ni la posición en el top 10 son una medida estable de qué temas importan. Ante fallos de fuentes, el recolector registra días `partial`, `unavailable` y `rate_limited`, que el expediente expone como `data_gaps`. Hecho (Earlywindow, G08, sin integrar en `main` de Earlywindow): perder un día de HN o GitHub en los 14 días previos al corte dejaba 0 expedientes; Earlyscript lo corrige con la regla `coverage_rule: per_source`, por la que un día sin datos queda `known: false` y en `data_gaps` sin vaciar la lista, probada con un día quitado del corpus. No se probó con una fuente caída en vivo.

**Recorridos con el modelo real.** Hecho: seis recorridos automáticos con `openai/gpt-6.1-sol`, del 21 al 26 de octubre, terminaron con ficha válida y decisión guardada en 59,2 a 82,3 segundos; el del 26 usó seis solicitudes, cuatro herramientas, 8.490 tokens de entrada y 1.944 de salida. Los seis usaron `researcher.v1`, sin `read_item`; C13 añadió un séptimo con `researcher.v2` y cuatro lecturas. El flujo funciona con el proveedor previsto; son tiempos automáticos con utilidad fija de 4, no valoraciones humanas.

**Verificación independiente, seguridad y calidad.** Hecho: un modelo distinto del que programó verificó tres veces. Sobre `d71dda2` concluyó "apto con correcciones para evaluación local controlada", con doce hallazgos (S01 a S12), entre ellos motivos privados en el paquete compartible. Sobre la integración en `fdd986b` (C25) dio otra vez apto con correcciones y reprodujo tres defectos: el enlace entre expediente y perfil se asignaba sin validar, el paquete compartible conservaba el consumo por corrida y un onboarding fallido no contaba contra el tope. C26, C27 y C28 los corrigieron, y C29 declaró `47c7d4d` "apto para main" tras repetir las sondas. En `main`, S04 y S11 quedan como opciones desactivadas en v0.02 para no invalidar su corrida. C29 no cubre fichas con proveedor real (Anexo 4). En Earlyscript el mismo esquema continuó: cada unidad de la Tabla 7 tiene veredicto de un segundo modelo, y las dos que tocan datos (importador y lector nativo) recibieron "no apto" en la primera pasada y se corrigieron antes de fusionar o siguen en rama.

**Etapa histórica sobre X (Tareas 5 a 7).** Sus cifras no describen a Earlywindow. La API de X devolvió el 29 de septiembre 100 publicaciones; quedaron 99 textos de 94 autores en 28 minutos y 37 segundos, partidos 59, 20 y 20. Con Qwen3-Embedding-0.6B (Qwen, s. f.), UMAP ajustado con 59 textos (McInnes et al., 2018) y cinco semillas, se compararon K-means 10, K-means 5 y BERTopic con HDBSCAN (Grootendorst, 2022) sobre los mismos 79 textos (Tabla 11).

**Tabla 11**

*Comparación de agrupamiento sobre X, media y desviación estándar de cinco ejecuciones (Tarea 6)*

| Métrica | K-means 10 | K-means 5 | BERTopic |
|---|---|---|---|
| Silueta, validación | −0,0182 ± 0,0243 | −0,0165 ± 0,0229 | No definida |
| Silueta, prueba | −0,0104 ± 0,0291 | 0,0349 ± 0,0101 | No definida |
| Cobertura de agrupamiento, validación y prueba | 100 % y 100 % | 100 % y 100 % | 0 % y 2 % |
| ARI medio, validación y prueba | 0,9028 y 0,8859 | 0,8848 y 0,8554 | No interpretable |
| Grupos de un texto, validación | 4,4 | 2,6 | No aplica |

K-means 5 se eligió el 6 de octubre, antes de abrir la prueba, por menor fragmentación y no por superioridad: su mejora de silueta de validación fue de 0,0017, con dos semillas a favor y tres en contra, y falta la claridad ciega. BERTopic no alcanzó la cobertura mínima. El prototipo de entonces tiene copia pública saneada en https://github.com/miwgel/singularidev-editorial-prototype (snapshot 3dff908). En el ensayo de la Tarea 6, el autor como único operador hizo dos fichas manuales (296,0 segundos con utilidad autovalorada 2, y otra incompleta al límite de 300 con 3) y dos asistidas (170,1 y 130,3 segundos, con 4 y 5). Un tiempo censurado impide calcular ahorro; es una señal favorable, no una medición del objetivo.

**Interpretabilidad (Tarea 7).** SHAP sobre un sustituto con fidelidad del 62 % (Lundberg y Lee, 2017), LIME con R² local de 0,45 a 0,60 (Ribeiro et al., 2016) y valores de Shapley exactos (Shapley, 1953) mostraron que la recencia decidía el orden, que la afinidad valía 1 en cuatro de cinco grupos porque "agent" aparecía en el 83 % de los textos elegibles y que el mismo grupo ganaba en las 171 combinaciones de pesos (Tarea 7; figura en `archive/output/tareas/evidencias-tarea-07/figura-1-shap-y-ranking.png`). Por eso Earlywindow reemplazó la recencia por crecimiento entre ventanas.

**Discusión frente a los criterios de éxito.** La Tabla 12 da el estado de cada criterio; el de cada objetivo está en el capítulo 8 y el de las observaciones del Comité, en el Anexo 6.

**Tabla 12**

*Estado de cada criterio de éxito al 31 de octubre de 2026*

| Criterio | Meta | Evidencia | Estado |
|---|---|---|---|
| Tiempo mediano, métrica principal | 40 % menos tiempo activo desde la búsqueda | Reloj por etapas en el servidor de Earlyscript; pantalla del hilo de video y modo manual en construcción; registro de dos semanas declarado por el autor, sin integrar; ejercicios sin iniciar | No evaluado |
| Respaldo factual | 90 %, dos juicios | En Earlyscript, el validador del guion cuenta afirmaciones con cita por versión (Figura 7 muestra "2 de 3"); el inventario humano de afirmaciones sin cita y los dos juicios siguen pendientes | No evaluado |
| Utilidad | 4 sobre 5, dos revisores externos | Sin revisores; la decisión de Earlyscript registra la del operador con anclas | No evaluable |
| Claridad de grupos | 3,5 sobre 5, ciega | No se traslada el resultado sobre X | No evaluable |
| Tres videos | Resultados descriptivos en siete días | Sin evidencia de publicación | Pendiente |
| Anticipación de una a dos semanas | Señal débil que se vuelve fuerte | Mediana de 2 días con v0.01 y 1 con v0.02; la fórmula no supera a la línea base | No respaldada |
| Presupuesto | 30 USD mensuales, aparte de X | Earlyscript usa los agentes instalados con la suscripción del operador, sin precio por solicitud; los títulos usan el modelo barato del proveedor; el motor no gasta inferencia. Earlywindow tenía tope con clave de API. Sin gasto real medido | No verificable |

**Lo demostrado.** El motor recolecta con procedencia, detecta señales de forma determinista y reproducible en dos plataformas, y Earlyscript las presenta con títulos legibles, evidencia enlazada y dos posiciones de ranking; su puntuación es explicable y robusta a los pesos. **Lo débil.** Avisar antes no quedó demostrado: el motor no ordena mejor que contar ítems de la última semana, el apilado depende de su umbral y de la plataforma de los vectores, la evidencia suele ser un titular y no hay métricas humanas. Lo defendible es que el arnés organiza señales y produce fichas de forma automática y que Earlyscript ya registra decisiones, versiones y tiempos por etapa; su efecto sobre el tiempo y la utilidad queda por medir con el protocolo del Anexo 5. Las Figuras 6 y 7 muestran lo que existe para esa medición, con dos advertencias: los datos de la Figura 6 son un fixture de prueba y la pantalla de la Figura 7 está en una rama sin fusionar.

**Figura 6**

*Espacio Resultados de Earlyscript con datos de prueba sembrados*

![Nota. Captura del 31 de octubre de 2026 en `main`. Las seis decisiones, los tiempos y las utilidades son un fixture de prueba de la unidad, no ejercicios reales; se incluye para mostrar la forma del reporte, que no calcula ahorro y declara que la comparación de la tesis es por pares y con revisores externos.](archive/output/tareas/evidencias-tarea-10/figura-earlyscript-resultados-datos-de-prueba.png)

**Figura 7**

*Hilo de video de Earlyscript con guion versionado y decisión registrada, en la rama `es/video-thread`, sin fusionar*

![Nota. Captura del 31 de octubre de 2026 en la rama `es/video-thread`, pendiente de verificación. A la derecha: ficha enlazada, guion con versión y conteo de afirmaciones con cita, decisión "Editar, utilidad 4 de 5" con motivo y tiempos por etapa, y bloque de resultado del video a mano. El hilo y el guion son una prueba del agente, no un ejercicio del operador.](archive/output/tareas/evidencias-tarea-10/figura-earlyscript-hilo-de-video-rama-sin-fusionar.png)

## Implicaciones éticas

El sistema apoya una decisión de riesgo limitado, qué video preparar, pero procesa textos de terceros, los envía a un proveedor de modelos de lenguaje y produce puntuaciones que pueden inducir más confianza de la debida. La referencia es el NIST AI RMF (Tabassi, 2023) y los principios de transparencia, rendición de cuentas, equidad y privacidad (Corrêa et al., 2023).

**Tabla 13**

*Riesgos éticos con evidencia. "Aplicada" consta en el código; "propuesta" no consta implementada*

| Riesgo y evidencia | Mitigación y estado |
|---|---|
| Falsa precisión: en X, 95 sobre 100 decidido por segundos de publicación (Tarea 7); en Earlywindow, la fórmula no supera a la línea base y el crecimiento aporta más de la mitad del puntaje en 10 de 18 expedientes (R13) | Desglose por componente, aplicada; orden presentado como apoyo de lectura |
| Respaldo aparente: 169 de 172 evidencias de 2263f7 sin extracto (168 de 177 en `fb1bd2`); el agente lee el artículo de 143 de 170 URL; una cita válida no confirma la afirmación (Gao et al., 2023) | Validación de identificadores, aplicada; auditoría por cita en `claims.csv` e inventario de afirmaciones sin cita, pendiente |
| Sesgo de fuente y agenda: dos fuentes técnicas en inglés; etiquetas dominadas por grandes proveedores | Perfil y exclusiones visibles, aplicadas; revisar concentración por tema y autor, propuesta |
| Exclusión silenciosa: el filtro ASCII excluye 121 ítems, 114 de GitHub; el texto en otro idioma que pasa es R02 | Exclusiones por motivo en `run.json`, aplicada; filtro de idioma validado, propuesta |
| Lectura causal de métricas comerciales | Reporte solo descriptivo, en el protocolo |

Notas. Las instrucciones incrustadas y la complacencia del modelo (Nguyen et al., 2026) pasan a la Tabla 14 como R01, y la divulgación en exportaciones como R09.

**Matriz de riesgos.** La Tabla 14 responde a la observación 4 del Comité. Probabilidad e impacto son juicios cualitativos con los controles aplicados, con la escala de la matriz d04 de la ola 7 (Supuesto de gestión). El responsable de todas las filas es Miguel, como Supuesto hasta que fije responsable, modalidad del proveedor y retención. "Aplicada" consta en Earlywindow `47c7d4d` o en Earlyscript `3e4c6c0741`; "en `ew/integration`" espera la verificación de Sol en Earlywindow; "en curso" tiene rama propia sin integrar; "propuesta" no existe. Evidencia y comprobación de cada fila: informe G09 de la ola 8 y Tabla 21 de la versión extensa del 26 de octubre.

**Tabla 14**

*Matriz de riesgos de Earlywindow con probabilidad, impacto y mitigación*

| ID y riesgo | P / I | Mitigación y estado |
|---|---|---|
| R01. Instrucciones incrustadas en textos de terceros (c15: 3 de 30 llegan sin marca al extracto) | Media / alto | Aplicada: agente sin shell, archivos ni red; `save_brief` exige aceptación humana; artículos marcados como contenido externo no confiable; `researcher.v2` trata el texto como datos. Propuesta: un recorrido real con la variante inyectada |
| R02. Texto en otro idioma pasa el filtro ASCII (español en 9 de 10 semillas) | Alta / medio | Aplicada: exclusiones por motivo en `run.json` y limitación declarada. Propuesta: rechazo con motivo "language" y recuento |
| R03. La selección depende de la combinación de umbrales (de 18 a 5 expedientes) | Alta / alto | Aplicada: configuración fijada por hash y umbrales declarados como hipótesis; todo cambio crea otra configuración y repite la prueba de umbral |
| R04. El top 10 cambia al quitar el 5 % de los ítems (0,20 a 0,50) | Media / alto | Aplicada: cobertura por fuente y día y aprobación humana; no presentar la posición como estable |
| R05. Una fuente caída deja la lista vacía sin explicar la causa | Media / medio | Aplicada en Earlyscript: cobertura por fuente, un día sin datos queda `known: false` y en `data_gaps` sin vaciar la lista; aviso de cobertura parcial en la ficha (Figura 3) |
| R06. Cambios de API o cuotas (403 de Bluesky, 429 de npm) | Alta / medio | Aplicada: corpus congelado verificable, respuestas grabadas en las pruebas, fuentes nuevas solo con `--sources`. En `ew/integration` (G03): npm tratado como fuente siempre parcial |
| R07. Términos de las fuentes no cubren todos los usos (Y Combinator, Bluesky, npm) | Alta / alto | Aplicada: corpus local sin redistribución. En `ew/integration` (G03): términos de las siete fuentes, gobernanza de npm y Bluesky y `corpus:purge`. Propuesta: aclaración de Y Combinator y retención en días |
| R08. Cambia el comportamiento del modelo conversacional (0 y 4 lecturas con v1 y v2) | Media / alto | Aplicada: versión y hash del prompt de títulos con estado "desactualizado"; T3 registra agente y modelo por hilo. Propuesta: fijar agente y modelo antes del primer ejercicio |
| R09. Las exportaciones divulgan datos privados | Baja / alto | Aplicada: lista blanca de columnas con prueba y sonda de C29 sin fugas. Propuesta: consentimiento de los revisores y revisión del paquete ciego |
| R10. Costo real de inferencia desconocido | Baja / medio | Aplicada: tope de 30 USD con `api_key` y consumo por corrida; costo reportado como estimado |
| R11. Anclaje en la nota de utilidad | Baja / medio | Aplicada: botones vacíos y utilidad obligatoria de 1 a 5, comprobado por C29 |
| R12. Un solo operador, que además desarrolló el sistema | Alta / alto | Propuesta, con instrumento construido: protocolo fijado antes de medir y paquete ciego para dos revisores. En `ew/integration` (G07): `npm run results` |
| R13. El crecimiento aporta más de la mitad del puntaje en 10 de 18 expedientes | Alta / medio | Aplicada: desglose visible y pesos estables ante ±20 %; orden presentado como apoyo de lectura |

**Permisos y términos.** Hacker News: la API de Algolia da acceso técnico, pero Y Combinator restringe copiar, extraer, crear obras derivadas y explotar comercialmente el contenido sin autorización expresa (Y Combinator, s. f.); el corpus se guarda en local para evaluación, y el uso comercial y la redistribución quedan bloqueados hasta una aclaración escrita. GitHub: los términos de su API rigen el acceso (GitHub, 2026), y el uso de identificadores, URL y agregados sigue sujeto a ellos. Que un dato sea público no acredita permiso ilimitado ni anonimato. Hecho, en `ew/integration` y pendiente de verificación de Sol (G03): el README da términos, acceso y cadencia de las siete fuentes, `docs/DATA.md` documenta origen, volumetría, datos personales, retención y borrado de npm y Bluesky, y `npm run corpus:purge` borra los ítems de una fuente recolectados antes de una antigüedad fijada y lo registra en el manifiesto; borra por antigüedad, no por publicación concreta. X limita la redistribución y exige borrar lo borrado (X Corp., s. f.); el lote histórico no se redistribuye. Reddit y YouTube no se usaron (Google, 2026).

**Privacidad.** Los embeddings son locales. En Earlywindow el agente enviaba a OpenAI, con la cuenta de ChatGPT del operador, el prompt, el historial, el expediente con extractos de hasta 500 caracteres y los ítems que leyera. En Earlyscript, el servicio de títulos envía al proveedor del agente instalado (Claude Code o Codex) los términos, los conteos y la evidencia con identificadores de cada ficha, y el hilo de video envía lo que el operador escriba y adjunte; la telemetría, la analítica de terceros y la comprobación de actualizaciones de T3 Code están apagadas por bandera, con cero salidas de red medidas en la unidad de banderas. Earlyscript no copia credenciales: lee las sesiones de los agentes instalados en su sitio. Borrar la copia local no prueba el borrado remoto. El corpus contiene nombres públicos y no es anónimo. **[PENDIENTE: política escrita de conservación y borrado por fuente, con revisión al registrar la calificación final, hasta el 27 de noviembre de 2026; registro de los controles de entrenamiento de la cuenta del proveedor; consentimiento de los revisores.]**

**Decisión humana.** El agente no puede aprobar ni escribir en una base. El operador acepta, edita, rechaza o difiere, y cada decisión queda ligada a actor, versión, motivo, utilidad, tiempo y la configuración que produjo su expediente, de modo que un cambio de motor no reescribe decisiones anteriores.

**Model Card de Earlywindow.** Sección integrante del informe con los seis elementos que pide el curso, según la estructura de Mitchell et al. (2019), en la Tabla 15. Describe el motor tal como se evaluó en Earlywindow (`47c7d4d`, `engine.v0.02`, corrida 2263f7) y su porte a Earlyscript (`trend-engine` 0.1.0 en `main` `3e4c6c0741`, corrida 5e57bf); las cifras de `engine.v0.01` son históricas. La Model Card del producto completo, con el hilo de video y el modo manual, se escribirá cuando esas unidades estén fusionadas.

**Tabla 15**

*Model Card del motor de tendencias, versión evaluada en Earlywindow y portada a Earlyscript*

| Elemento | Contenido |
|---|---|
| Versión | Earlywindow `47c7d4d`, `engine.v0.02` (`sha256:bbd96934…`), perfil `singularidev.v1`, corrida 2263f7, 18 expedientes. Earlyscript `main` `3e4c6c0741`, `trend-engine` 0.1.0, configuración `earlyscript.engine.v1` (`sha256:290b9dde…`), corrida 5e57bf del 31 de octubre, 15 fichas; prompt de títulos v3 con claude-haiku-5-5. |
| Propósito y usuario | Apoyar a un solo operador, Miguel, en la priorización de ideas de video en inglés para SingulariDev. El operador acepta, edita, rechaza o difiere cada ficha con motivo y utilidad. No entrena pesos de modelos: se calibran umbrales, pesos y perfil. |
| Componentes | Motor determinista; Qwen3-Embedding-0.6B ONNX en CPU (7.2), cuya tarjeta no declara licencia; en Earlywindow, Pi coding agent 1.3.0 (MIT) con `openai/gpt-6.1-sol`; en Earlyscript, T3 Code (MIT) con los agentes instalados en la máquina, servicio de generación de texto para títulos y resúmenes, y validador del guion. |
| Datos | Corpus congelado `sha256:5bf2d88a…`: 49.784 ítems de HN y 678 de GitHub del 30 de agosto al 18 de octubre de 2026; 45.557 con embedding. Corpus fresco de Earlyscript: 28.311 de HN y 282 de GitHub del 3 al 30 de octubre; 26.037 con embedding. El 91,49 % de HN es solo título y todos los días de GitHub son `partial`. Datos de inferencia y evaluación, en local y sin redistribución (7.4). |
| Métricas | Retrospectiva v0.02: P@5 0,95 frente a 1,00 de `items_7d`, P@10 0,95 frente a 0,975, mediana de 1 día y 2 de 64 positivas con 7 días o más; v0.01: P@5 0,80 frente a 0,90 y mediana de 2 días. No supera a la línea base en ningún corte. Robustez v0.02: tau mínima 0,905 ante pesos; de 18 a 5 expedientes con umbral de apilado 0,65; top 10 sustituido en 0,20 a 0,50 al quitar el 5 %. Tiempo, respaldo y utilidad humanos sin medir. |
| Explicabilidad | Desglose aditivo del puntaje y coseno de cada ítem con su centroide. En 2263f7 el crecimiento aporta del 33,8 % al 64,7 % del puntaje y más de la mitad en 10 de 18 expedientes, la fragilidad que señaló el tutor. SHAP y LIME de la Tarea 7 explican otro sistema; el modelo conversacional no tiene explicación validada. |
| Riesgos y limitaciones | Sin anticipación demostrada. Un operador que también desarrolló el sistema. El filtro ASCII deja pasar el español. Selección sensible a los umbrales, a la muestra y a la plataforma de los vectores (3 de 5 coincidencias en el top 5 entre macOS y Linux). Top 10 inestable. 169 de 172 evidencias sin extracto. Instrucciones incrustadas sin marca. Costo por suscripción, sin precio por solicitud. Detalle en la Tabla 14. |
| Uso recomendado y no previsto | Apoyo de lectura y redacción para un operador que revisa cada cita y decide. No usar para publicar sin aprobación, predecir tendencias o demanda, verificar hechos, trabajar en otros idiomas, fuentes o periodos sin evaluación ni atribuir clics, registros o pagos. Envío al proveedor y exportaciones: párrafo de privacidad y R09. |

# Conclusiones y Recomendaciones

Las conclusiones son preliminares: se basan en dos corridas del motor (canónica en macOS y fresca en Linux), una retrospectiva de cuatro cortes solapados, pruebas automáticas y verificaciones de un segundo modelo, y, para la etapa anterior, 99 textos de X y un ensayo de un operador. No se generalizan fuera de ese caso. Los criterios de éxito están en la Tabla 12.

1. **Objetivo 1, en curso.** La línea base manual no se acreditó en este avance: hay un diagrama preliminar, dos fichas manuales sobre X y un registro de dos semanas que el autor declara tener, reconstruido desde el 1 de octubre y sin integrar ni verificar. Las 20 horas semanales siguen siendo una estimación hasta integrar ese registro en S11.
2. **Objetivo 2, completo con validación externa pendiente.** La matriz (4,45 frente a 2,55), el spec v1, los principios del motor de Earlyscript y la arquitectura implementada reproducen la alternativa B: motor sin modelo, agente que solo lee y redacta, decisión por un camino que el modelo no invoca. Falta comunicar al tutor el cambio de corpus y el cambio de producto.
3. **Objetivo 3, parcial con desviación registrada.** El flujo es reproducible: un paquete congelado reconstruye la misma huella en Earlywindow y `engine check` reproduce la corrida fresca en Earlyscript; cambiar de plataforma cambia los vectores y parte de las señales, lo que se declara como limitación. La comparación de agrupadores existe solo sobre X, la de embeddings no se ejecutó y la claridad de grupos no es evaluable en el corpus nuevo. Sobre HN, la fórmula no superó a la línea base por volumen con v0.01 ni con v0.02, y la anticipación de una a dos semanas no quedó respaldada.
4. **Objetivo 4, parcial.** En Earlywindow la integración funcionó en siete recorridos reales y registra cada decisión. En Earlyscript la integración con los agentes de T3 Code existe por construcción, los títulos y resúmenes se redactaron con un modelo real (3 fichas en 12 a 22 s) y el servidor registra versiones del guion y decisiones; la pantalla del hilo de video y el modo manual están en rama. Faltan las seis fichas evaluadas por el operador. La personalización reversible del perfil existe en Earlywindow (C09) y no se portó aún.
5. **Objetivo 5, pendiente.** El protocolo está propuesto, sin adopción acreditada, y no hay ejercicios, revisores ni videos; las metas no son evaluables todavía. Decisión del 30 de octubre: si antes del 5 de noviembre un ejercicio completo con modelo real funciona en Earlyscript, los seis pares se hacen sobre Earlyscript; si no, se hacen sobre Earlywindow y Earlyscript pasa a trabajo futuro.

**Síntesis.** El arnés cumple la parte de trazabilidad de la necesidad: conserva fuentes, versiones y decisiones que el proceso manual pierde, y Earlyscript lo hace dentro de una herramienta que el operador quiere usar a diario. El tiempo queda por medir y la promesa de anticipación no se sostiene con el motor actual.

**Reflexión crítica y retroalimentación integrada.** Por la observación de la Tarea 1, el Anexo 2 incluye el bloque de firmas. Por S4, las versiones están fijadas en el lockfile y `freeze:verify` exige las mismas. Por S5, se añadió un modo manual con el mismo reloj y el protocolo de seis pares. S6 valoró el descarte honesto de BERTopic; la retrospectiva informa igual el resultado desfavorable de la fórmula. Las observaciones del Comité se responden en la Tabla 10, en 7.4 y en el Anexo 6. La revisión E26 llevó a describir el protocolo humano como propuesto, acotar la auditoría factual a citas, retirar la afirmación de aceleración y ajustar el formato en la versión 2. El error principal fue de calendario: construir el motor antes de medir el tiempo humano dejó la métrica principal para las dos últimas semanas, y el cambio de producto del 30 de octubre lo agrava si no se cumple el corte del 5 de noviembre. La corrección es el corte fijado, congelar el producto que se use para los ejercicios y separar mejoras de evaluación. A cambio, el fork redujo el código propio que hay que mantener: las unidades de Earlyscript son paquetes y carpetas aditivos con enganches de una línea, en lugar de una aplicación de escritorio completa.

**Recomendaciones.** Al operador: usar las fichas como apoyo de lectura, no como predicción, y abrir el artículo antes de aceptar una afirmación basada en un titular o en un resumen del asistente. Al desarrollo: fusionar solo con verificación, no presentar lo que está en rama como hecho, y probar señales con más contexto que el título. A la gobernanza: pedir a Y Combinator la aclaración de uso y aprobar la política de conservación antes de ampliar el corpus. **[PENDIENTE: conclusión por objetivo con cada meta alcanzada, no alcanzada o no evaluable, tras los ejercicios, el registro y el piloto.]**

# Trabajo futuro

**Lo que falta de esta tesis**, como plan y no como resultado:

- **Semana 12 (26 de octubre al 1 de noviembre).** Hecho: verificación de Earlywindow, traslado del entorno, decisión de producto y diez unidades de Earlyscript. Entrega S10 el 30: este PDF. Queda: fusionar el lector del formato nativo, la bandeja activa y la pantalla del hilo de video; correo al tutor con los dos cambios.
- **Semana 13 (2 al 8 de noviembre).** Modo manual y corrida nocturna; corte del 4 o 5 de noviembre con un ejercicio completo con modelo real; adopción del protocolo y congelado del producto elegido; sesiones de ejercicios; integración del registro de dos semanas; reclutamiento y calibración de revisores; demo de tres minutos y pitch. Entrega S11: informe ajustado y presentación.
- **Semana 14 (9 al 15 de noviembre).** Análisis descriptivo de tiempos y utilidad en el espacio Resultados, auditoría de afirmaciones, informe final y ensayo de defensa. Entrega S12 y defensa probable el 13.

Con un solo ejecutor, los seis pares y los revisores caben en dos semanas solo si el producto queda congelado el 5 de noviembre. Si faltan pares, se informan los ejercicios hechos y el mínimo incumplido, sin relajar reglas después de ver resultados.

**Tabla 16**

*Pendientes que dependen de terceros o de la evaluación, al 31 de octubre de 2026*

| Pendiente | De quién depende |
|---|---|
| Validar la Figura 1 con el operador y pasarla a BPMN; captura fechada de YouTube Analytics | Autor |
| Integrar y verificar el registro de dos semanas, declarado como reconstrucción | Autor |
| Sector formal, misión y visión, estado de la comunidad; lugar de operación y obligaciones legales | Autor y auspiciante |
| Tabla complementaria de viabilidad, costo, innovación, impacto y tiempo, si el tutor la pide | Tutor |
| Respuesta de Y Combinator sobre uso comercial; política escrita de conservación y borrado; controles de entrenamiento de los proveedores; consentimiento de los revisores | Terceros y autor |
| Calibrar la rúbrica de utilidad con los revisores; respuesta del tutor sobre las desviaciones de los objetivos 3, 4 y 5 y sobre el cambio de producto | Tutor y revisores |
| Horas registradas por semana, imputación del equipo, análisis financiero con TCO | Autor, tras la línea base |
| Ampliar la bibliografía sobre utilidad en recomendación y sesgos de modelos de lenguaje | Autor |
| Cita APA del uso de IA generativa según la política de la UDLA | Autor |
| Acceso de lectura efectivo del tutor y del tribunal; README para terceros; video de la demo | Autor y tutor |
| Bloque de firmas y grado académico del tutor en la portada | Tutor |
| Anexos compartibles numerados sin superar 20 MB y sin datos privados | Autor |
| Ejercicios, tiempos, utilidades, revisores y auditoría factual; conclusión por objetivo | Evaluación |

**Proyectos posteriores.** Portar a Earlyscript las fuentes con adaptador de Earlywindow (Wikipedia Pageviews, Stack Exchange, arXiv, Bluesky y npm); identidad estable de tendencias entre corridas y fusión de señales; "Preguntar a la ficha" con un agente de solo lectura; perfil editable; conectores de métricas en Ajustes; fusión regular del upstream de T3 Code; firma y notarización para distribuir; X bajo demanda; acceso comercial autorizado; ranking adaptativo, otros idiomas, CRM y medición causal de la adquisición.

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

Zechner, M. (2026). *Pi coding agent* (Versión 1.3.0) [Software]. GitHub. https://github.com/earendil-works/pi/releases/tag/v1.3.0

Zhang, Z., Fang, M., Chen, L., & Namazi-Rad, M.-R. (2022). Is neural topic modelling better than clustering? An empirical study on clustering with contextual embeddings for topics. En M. Carpuat, M.-C. de Marneffe, & I. V. Meza Ruiz (Eds.), *Proceedings of the 2022 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies* (pp. 3886–3893). Association for Computational Linguistics. https://doi.org/10.18653/v1/2022.naacl-main.285

Zhou, X., Zhao, Y., Jiang, O., Hu, T., Xu, C., Patwardhan, M., & Cohan, A. (2026). *BackTrend: Evaluating scientific weak-signal prediction via backward reconstruction* [Prepublicación]. arXiv. https://doi.org/10.48550/arXiv.2609.24921


# Anexos

**Anexo 1. Carta de auspicio de Bistec LLC.** Carta del 2 de agosto de 2026 en la que Bistec LLC apoya el proyecto y se compromete a dar acceso a la información y facilitar pruebas, sin relación laboral. Se adjunta el PDF existente, `archive/proyecto/Miguel Brito - Carta de Auspicio Bistec LLC.pdf`. Esta revisión no verificó la firma ni el sello.

**Anexo 2. Firmas de responsabilidad.**

| | Autor | Tutor |
|---|---|---|
| Nombre | Miguel Ángel Brito Espejo | Luis Fernando Aguas Bucheli |
| Firma | | |
| Fecha | | |

**[PENDIENTE: confirmar con el tutor si el bloque aplica al avance y su grado académico, PhD(c) o PhD, para la portada.]**

**Anexo 3. Registro de desviaciones.** Compromisos que la versión de evaluación no cumple tal cual; ninguno bloquea el producto y todos deben comunicarse al tutor. El registro completo, con 37 filas, sustituto, efecto por objetivo, estado y lo que puede decidir el autor, está en `archive/contexto/intento-actual/planificacion/2026-10-26-ola8/36-e28-informe.md`. Desviaciones nuevas del 30 de octubre, pendientes de añadir a ese registro: el producto final es un fork de T3 Code y no una aplicación propia sobre Pi; la ficha de ocho apartados generada por el agente se sustituye por un guion escrito por el operador con asistente y validador; el modelo de lenguaje pasa a ser el agente instalado en la máquina (Claude Code o Codex) y no un proveedor fijado por configuración; la interfaz editorial está en español. Las que más afectan a la evaluación se tratan en el texto: el corpus de HN y GitHub en lugar de X y Reddit (7.1), la comparación de embeddings no ejecutada (Tabla 3), el reloj desde un expediente preparado (capítulo 3 y Anexo 5), los agrupadores comparados solo sobre X y la anticipación no respaldada (7.3). Hecho: después de ese registro, `main` incorporó la exportación corregida, el tope mensual con clave de API, el `session_hash` por sesión y la ficha hija, así que esas filas quedan resueltas en código.

**Anexo 4. Fuentes técnicas del avance.** Informes en `archive/contexto/intento-actual/planificacion/`: spec v1 y unidades U0 a U9 en `2026-10-21-earlywindow-spec/`; ola 7 en `2026-10-22-ola7/` (c02 a c14 y d01 a d13, entre ellos el protocolo d07, los procesos d08 y el correo d09); ola 8 en `2026-10-26-ola8/` (verificación de d71dda2, c01 a c29, con las verificaciones C25 y C29, e24 guion del pitch, e26 revisión de este avance y e28 desviaciones y correo). Datos fuera de Git en `~/earlywindow-data/`: corrida canónica `runs/run_20261019_20261021T201022_fb1bd2`, corrida v0.02 `runs/run_20261019_20261027T003754_2263f7`, retrospectivas `runs/backtest-eval-1` y `-2`, ola 7 en `ola7/` y verificaciones en `ola8/verify/`, `ola8/c25/` y `ola8/c29/`. Earlyscript: decisiones y diseño en `planificacion/2026-10-30-earlyscript-motor/` (brief, dos diseños, principios y primitivos, maquetas y decisiones de uso, plan de construcción con el estado por unidad, mapa de integración) y estado de sesión en `2026-10-30-earlyscript-sesion-estado.md`; en el fork, `docs/upstream-divergence.md`, `AGENTS.md` y los README de `trend-engine` y `editorial-script`. Datos de Earlyscript fuera de Git en `~/earlyscript-data/`: corrida fresca `runs/run_20261031_20261031T003855_5e57bf`, corpus `live/corpus-2026-10-31/`, capturas e informes de verificación por unidad. La versión extensa del 26 de octubre está en `2026-10-26-ola8/45-e34-avance-extenso-27-pendientes.md`. El paquete de 41 archivos que propone E16 no equivale a autorización de divulgarlo. **[PENDIENTE: numerar y adjuntar los anexos compartibles sin superar 20 MB por archivo; revisar que ninguno contenga credenciales, corpus, sesiones ni motivos privados.]**

**Anexo 5. Protocolo de evaluación humana.** Propuesto el 22 de octubre de 2026 en el informe d07; su adopción, la selección de pares y la ejecución no están acreditadas al 31 de octubre. En Earlyscript el instrumento es el hilo de video (asistido o manual) con reloj por etapas y el espacio Resultados; las reglas siguientes se conservan.

- **Registro.** El autor declara un registro de dos semanas reconstruido desde el 1 de octubre, con búsqueda y escritura separadas; se integra en S11 declarado como reconstrucción; un día sin registro es faltante, no cero.
- **Pares y asignación.** Seis pares comparables fijados antes de conocer resultados; condición y orden por semilla registrada, tres sesiones con manual primero y tres con asistida, el 26, 28 y 30 de octubre y el 2, 4 y 6 de noviembre.
- **Tareas.** Ficha en inglés con los ocho apartados y 30 minutos como límite; en manual, sin modelo generativo. Antes del primer ejercicio se fijará qué textos leen ambas condiciones: el agente lee artículos de la corrida v0.02 con `read_item`, así que se dará el mismo acceso en manual o una condición sin artículos para ambos, y cualquier asimetría se declarará antes de medir.
- **Tiempo.** En Earlyscript, el reloj del hilo registra explorar, leer, escribir y decidir, con pausas registradas; el contraste principal es el proceso completo por par, y las etapas permiten comparar explorar a mano frente a la bandeja y escribir a mano frente a escribir con asistente. No mide el tiempo activo de semanas anteriores, que se informa con el registro. Un ejercicio al límite o abandonado se informa como censurado.
- **Calidad y análisis.** Utilidad por el operador y por dos revisores ciegos; auditoría de cada cita de `claims.csv` y de las afirmaciones sin cita, inventariadas aparte, con la misma lista para el segundo juicio. Medianas por condición y diferencias por par, descriptivas, sin prueba de significación ni atribución causal. Hecho, en `ew/integration` y pendiente de verificación de Sol (G07): `npm run results` calcula por modo completos, abandonados y censurados, mediana y cuartiles de tiempo, utilidad media y acciones, sin motivos ni textos; `test:export` pasa 21 de 21.

**[PENDIENTE: ejercicios ejecutados, tiempos, utilidades, revisores confirmados y resultados de la auditoría factual.]**

**Anexo 6. Observaciones del Comité y su estado al 31 de octubre.**

1. Diagramar el proceso manual: diagrama preliminar (Figura 1); BPMN pendiente.
2. Medir la carga con registros reales: el autor declara un registro de dos semanas reconstruido desde el 1 de octubre; sin integrar ni verificar en este avance.
3. Anclas de utilidad y validación de la rúbrica: anclas definidas; validación con revisores pendiente.
4. Riesgos con mitigaciones: hecho, matriz de 13 riesgos con probabilidad, impacto y mitigación (Tabla 14), con responsable Supuesto hasta que el autor lo fije; la Tabla 13 conserva los riesgos éticos que la matriz no cubre.
5. Algoritmo además de BERTopic: hecho sobre X (Tarea 6).
6. Sensibilidad de pesos: hecho sobre X (171 combinaciones) y sobre Earlywindow (90 escenarios, v0.01 y v0.02).
7. Datos, permisos, cuotas y términos: hecho para HN, GitHub, X, Reddit y YouTube; términos de las siete fuentes y gobernanza de npm y Bluesky en `ew/integration`, pendientes de verificación de Sol (G03); aclaración de Y Combinator pendiente.
8. Robustez ante fallos y variación de tendencias: hecho para pesos, umbral, pérdida de ítems, proveedor y drift; el día perdido vaciaba la lista en Earlywindow y Earlyscript lo corrige con cobertura por fuente; añadida la sensibilidad a la plataforma de los vectores.
9. Procedencia, herramientas, parámetros y decisiones: hecho, con huellas por corrida, decisiones ligadas a su corrida, reproducción desde un clon limpio (G02 en Earlywindow, `engine check` en Earlyscript) y registro de divergencia archivo por archivo en el fork.
10. Bibliografía sobre utilidad y sesgos: pendiente.
