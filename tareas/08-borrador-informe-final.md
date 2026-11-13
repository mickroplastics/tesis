---
title: "Arnés agéntico basado en modelos de lenguaje y análisis semántico de tendencias para priorizar ideas de contenido en YouTube orientadas a la adquisición de miembros para SingulariDev"
author: "Miguel Ángel Brito Espejo"
guide: "Luis Fernando Aguas Bucheli"
date: "20 de octubre de 2026"
---

# Resumen

SingulariDev, unidad de Bistec LLC, prepara una comunidad en inglés para emprendedores unipersonales interesados en agentes de inteligencia artificial y usa YouTube para atraerlos. Su fundador investiga y prioriza ideas de video a mano, estima esa carga en más de 20 horas semanales y no conserva un registro que una señales, evidencia, criterios y decisiones. El proyecto desarrolla y valida un arnés agéntico que detecta y prioriza oportunidades de contenido con análisis temporal, agrupamiento semántico y modelos de lenguaje, y deja la decisión final a una persona. Una matriz de valoración previa del autor, con criterios adaptados de ISO/IEC 25059:2023, favoreció un arnés híbrido y modular con 4,45 frente a 2,55 sobre 5 del agente generalista. El prototipo representó 99 publicaciones de X con Qwen3-Embedding-0.6B y UMAP, comparó K-means y BERTopic con cinco semillas, ordenó los grupos con una fórmula explícita y generó fichas en inglés con citas literales vinculadas a sus fuentes, mediante un agente construido sobre Pi. K-means con cinco grupos quedó como opción provisional: mejoró la silueta de validación en 0,0017 y siguió negativa. BERTopic no alcanzó la cobertura exigida en la configuración evaluada. En un ensayo exploratorio con un solo operador, este declaró completas las dos fichas asistidas en 170,1 y 130,3 segundos, con utilidad autovalorada de 4 y 5 sobre 5; una ficha manual tardó 296,0 segundos y otra quedó incompleta al límite de 300. El análisis de interpretabilidad mostró que el orden de los grupos dependía sobre todo de la recencia dentro de un lote de media hora, así que la puntuación no mide relevancia. Estos resultados no demuestran la reducción de tiempo del 40 %, el respaldo factual del 90 % ni la utilidad validada por revisores externos. La señal favorable está en la redacción asistida; la detección de tendencias no se evaluó. El 20 de octubre de 2026 el autor decidió construir Earlywindow, una aplicación de escritorio local con siete fuentes previstas y medición integrada de tiempo y utilidad, pendiente de construir, evaluar y comunicar al tutor.

**Palabras clave:** arnés agéntico, modelos de lenguaje, agrupamiento semántico, priorización editorial, trazabilidad.


# Abstract

SingulariDev, a unit of Bistec LLC, is building an English-language community for solo entrepreneurs interested in artificial intelligence agents and uses YouTube to reach them. Its founder researches and prioritizes video ideas by hand. He estimates that workload at more than 20 hours per week and keeps no record linking signals, evidence, criteria, and decisions. The project develops and validates an agentic harness that detects and prioritizes content opportunities through temporal analysis, semantic clustering, and language models, leaving the final decision to a person. A prior assessment matrix by the author, with criteria adapted from ISO/IEC 25059:2023, favored a hybrid modular harness, scoring 4.45 versus 2.55 out of 5 for a generalist agent. The prototype represented 99 X posts with Qwen3-Embedding-0.6B and UMAP, compared K-means and BERTopic across five seeds, ranked the clusters with an explicit formula, and generated English content briefs with literal quotations linked to their sources, through an agent built on Pi. K-means with five clusters was kept as a provisional option: it improved the validation silhouette by 0.0017 and remained negative. In the evaluated configuration, BERTopic did not reach the required 80 % coverage. In an exploratory trial with a single operator, the operator declared the two assisted briefs complete at 170.1 and 130.3 seconds, with self-rated usefulness of 4 and 5 out of 5; one manual brief took 296.0 seconds and another remained incomplete at the 300-second limit. The interpretability analysis, on the 79 development texts, showed that cluster ranking depended mainly on recency within a half-hour batch, so the score does not measure relevance. These results do not demonstrate the 40 % time reduction, the 90 % factual support, or usefulness validated by external reviewers, which remain pending. The favorable signal lies in evidence-based assisted writing; trend detection was not evaluated. On October 20, 2026, the author decided to build Earlywindow, a local desktop application with seven planned sources and built-in measurement of time and usefulness. Its construction, its evaluation, and the communication of the corpus change to the tutor remain pending.

**Keywords:** agentic harness, language models, semantic clustering, editorial prioritization, traceability.

# Introducción

**Cómo leer este borrador.** Integra lo hecho hasta el 20 de octubre de 2026 con la estructura del informe final. Cada cifra viene de una entrega anterior, citada como Tarea 1 a Tarea 7. Lo que falta está marcado como **[PENDIENTE: …]** y resumido en la Tabla 14 de los anexos. Las decisiones del 20 de octubre sobre la siguiente versión del prototipo se presentan como decisiones, no como resultados.

## Identificación y descripción del problema o necesidad

El fundador de SingulariDev busca ideas de video en varias fuentes, decide cuáles investigar, lee y compara, escribe una ficha y decide si graba. Todo lo hace una persona. Estima que investigar y priorizar le toma más de 20 horas semanales (Brito Espejo, 2026). Esa cifra es una estimación, no una medición; el registro real de dos semanas que pidió el Comité todavía no existe. Hay un segundo problema: casi nada queda registrado. No consta qué señal llevó a cada idea, con qué criterio se filtró ni por qué se descartó o se grabó, y las métricas de YouTube Analytics no se conectan con la decisión que originó el video. La Figura 1 muestra el proceso y los tres puntos donde probablemente se pierde el rastro.

![Figura 1. Proceso manual de investigación y selección de ideas. Reconstrucción preliminar a partir de la Tarea 1; los recuadros rojos marcan los posibles puntos de pérdida de trazabilidad.](archive/output/tareas/evidencias-tarea-08/figura-1-proceso-manual.png)

**Causas y efectos.** Son hipótesis de la Tarea 1. Las señales están repartidas entre fuentes, así que se investiga varias veces lo mismo; los criterios editoriales no están escritos, así que no se puede reconstruir una elección; una sola persona opera todo, e investigar compite con producir; y las fuentes cambian cuotas, precios y términos con frecuencia. La falta de miembros o de ventas no es el problema que se ataca, porque depende también del video, la distribución, la oferta y el precio. El proyecto lo trata como una necesidad de la organización, no como la falla de un sistema que exista; por eso el análisis usa un FODA, aceptado por el Comité al aprobar la propuesta (Comité de Evaluación de Proyectos MIA, 2026).

**Tabla 1.** FODA de SingulariDev (Brito Espejo, 2026, §2.3).

| | Interno | Externo |
|---|---|---|
| **Favorable** | Canal propio con unos 7.200 suscriptores al 2 de agosto de 2026 y acceso a sus métricas. Experiencia del fundador en software, IA y contenido. | APIs oficiales y datos públicos. Un segmento angloparlante nuevo de emprendedores unipersonales. Modelos de lenguaje con herramientas para sintetizar evidencia. |
| **Desfavorable** | Operación individual con más de 20 horas semanales estimadas. Audiencia histórica en español y comunidad inglesa sin historial. Criterios manuales sin registro. | Cambios de cuotas, precios y términos de las fuentes. Sesgo, saturación y variación rápida de los temas. Alucinación del modelo y dependencia del proveedor. |

**Por qué un asistente con trazabilidad y no una conversación con un modelo.** Noy y Zhang (2023) midieron un 40 % menos de tiempo con asistencia generativa en escritura profesional, pero preparar una idea incluye buscar y seleccionar, no solo escribir. Y la asistencia no garantiza mejores decisiones: en un experimento de campo con 640 emprendedores, Otis et al. (2026) no hallaron un efecto promedio concluyente. Una conversación directa con un modelo tampoco deja registro de fuentes, criterios y decisiones. La necesidad tiene dos partes: menos tiempo y más trazabilidad, sin delegar la decisión.

**Requerimientos de la organización.** Seis, según la propuesta: decisión final humana registrada con motivo y fecha; cada afirmación rastreable hasta su fuente; fichas en inglés; solo datos con acceso autorizado; inferencia de hasta 30 USD mensuales; y tiempo y calidad medibles frente al proceso manual. **[PENDIENTE: validar la Figura 1 con el operador y pasarla a BPMN; registro de carga de 14 días, previsto del 20 de octubre al 2 de noviembre; captura fechada de YouTube Analytics.]**

## Descripción de la organización

Bistec LLC es una sociedad de responsabilidad limitada registrada en Wyoming, Estados Unidos, dedicada a software y productos digitales, y auspicia el proyecto. SingulariDev es su unidad de aplicación: formación y comunidad en línea sobre IA aplicada. Miguel Ángel Brito Espejo representa a ambas. No se localizaron una misión ni una visión formales; el propósito consta en la propuesta: atraer desde YouTube a emprendedores unipersonales angloparlantes interesados en agentes, automatización y productos con IA hacia una comunidad en Skool. SingulariDev no tiene departamentos: una persona cumple cuatro funciones (investigación y planificación editorial, producción, comunidad y desarrollo de software), y la necesidad ocurre en la primera, antes de producir el video. **[PENDIENTE: organigrama funcional como figura.]**

**Productos, activos y segmento.** El canal de YouTube Miguelito Hacks, con unos 7.200 suscriptores al 2 de agosto de 2026 y audiencia mayoritariamente hispanohablante; un piloto de tres videos en inglés, previsto y sin evidencia de publicación; y una comunidad en Skool, prevista, con modelo freemium en evaluación y sin historial para modelar conversión. El 20 de octubre de 2026 el autor acotó la validación de la tesis a contenido para programadores en inglés y decidió desarrollar Earlywindow, un producto de software con un solo código para la tesis y para su uso posterior, con Bistec LLC como titular; su modelo de negocio queda fuera del proyecto académico y la sección 7.1 lo describe como diseño. **[PENDIENTE: sector formal registrado; misión y visión; estado de la comunidad; relación entre el nicho validado y la audiencia amplia.]**

# Análisis de posibles soluciones

## Identificación y selección de la mejor solución

Las dos alternativas usan modelos de lenguaje para el mismo problema y difieren en dónde se calcula la prioridad y cuánto control conserva el operador. En la **alternativa A, agente generalista**, un solo agente con herramientas consulta fuentes, interpreta señales y redacta la recomendación; se construye rápido, pero su priorización queda implícita en la respuesta del modelo y puede cambiar entre ejecuciones con los mismos datos. La **alternativa B, arnés híbrido y modular**, separa la sesión del agente, los adaptadores de fuentes, el almacén de evidencia, el análisis determinista (agrupamiento y puntuación) y la generación; el modelo investiga y redacta, la puntuación se recalcula desde datos y pesos registrados, y el operador acepta, edita o rechaza cada ficha. Los modelos de contexto de ambas constan en la propuesta aprobada.

La selección usó ocho características de ISO/IEC 25059:2023, el modelo de calidad para sistemas de IA que extiende ISO/IEC 25010 (ISO e IEC, 2023). Es una estimación previa del autor, no un resultado experimental. Escala: 1, sin mecanismo claro; 3, cobertura parcial; 5, cobertura explícita y verificable.

**Tabla 2.** Matriz de selección (Brito Espejo, 2026, §6.4).

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

Se eligió B. Obtiene 5 en transparencia, control e intervención porque conserva fuentes, exige aprobación y permite revertir. No llega a 5 en corrección ni robustez porque el modelo y las APIs pueden fallar. Añadir controles externos a A la convertiría en B. Dentro de B se fijaron dos comparaciones técnicas de IA (Tarea 3), que la Tabla 3 resume. **[PENDIENTE: tabla complementaria de viabilidad, costo, innovación, impacto y tiempo que pide la guía del tutor, si confirma que complementa la matriz aprobada.]**

**Tabla 3.** Alternativas técnicas comparadas dentro de la solución.

| Comparación | Qué se fija | Criterio de decisión | Estado al 20 de octubre |
|---|---|---|---|
| BERTopic frente a K-means | Mismos textos, embeddings y proyección UMAP por semilla | Cobertura de al menos 80 %, silueta válida en cinco semillas, mejora media, caída de ARI de 0,05 o menos | Ejecutada (Tarea 6). K-means 5 provisional; BERTopic descartado en esta iteración |
| Qwen3-Embedding-0.6B local frente a text-embedding-3-large por API | Mismos textos y algoritmos | La API entra solo si mejora la claridad en 0,5 o más sobre 5 y cabe en 30 USD mensuales | No ejecutada. La decisión del 20 de octubre mantiene embeddings locales; desviación por registrar con el tutor |

## Impacto del proyecto en la sociedad

Los impactos son esperados, no observados. En lo económico, reducir el esfuerzo de investigación del único operador; el 40 % es una meta, con inferencia limitada a 30 USD mensuales aparte de X. En lo social, un emprendedor unipersonal podría investigar con varias fuentes y evidencia enlazada; el riesgo es amplificar anuncios de proveedores, porque en la Tarea 7 "claude", "openai" y "dots" definieron grupos enteros. En lo tecnológico, el sistema integra técnicas existentes y no aporta un algoritmo nuevo. En lo legal, los textos de terceros están sujetos a los términos de cada fuente y a la normativa de protección de datos aplicable (Asamblea Nacional del Ecuador, 2021). En lo ambiental, no se ha medido el consumo energético; la Tarea 5 registró 15,38 segundos de CPU para 79 textos. En lo ético, la aprobación humana en cada ficha y los riesgos de falsa precisión, sesgo circular y exclusión silenciosa se tratan en 7.4. **[PENDIENTE: efecto de la caída de cada fuente; lugar de operación y obligaciones legales por tratamiento.]**

# Objetivos

Los objetivos conservan las metas de la Tarea 1. El objetivo 3 incorpora la comparación de embeddings acordada en la Tarea 3; las fuentes se detallan en el alcance, porque cambiaron el 12 de septiembre y el 20 de octubre.

## Objetivo General

Desarrollar y validar, entre agosto y noviembre de 2026, un prototipo de arnés agéntico que combine detección temporal de señales, agrupamiento semántico y modelos de lenguaje bajo aprobación humana registrada, para reducir al menos 40 % el tiempo mediano de preparación de fichas de contenido en inglés de SingulariDev y apoyar así la adquisición de miembros.

## Objetivos Específicos

1. Caracterizar el proceso manual de investigación y selección de ideas mediante un diagrama del flujo actual, un registro de carga de al menos dos semanas y seis fichas manuales, para sustituir la estimación de 20 horas semanales por una línea base observada.
2. Diseñar la arquitectura, los permisos y los criterios de aceptación del arnés, y documentar la comparación previa de dos alternativas con criterios de ISO/IEC 25059:2023, para justificar la solución seleccionada.
3. Implementar un flujo reproducible que recolecte evidencia de fuentes autorizadas con su procedencia y compare BERTopic con K-means, y Qwen3-Embedding-0.6B con text-embedding-3-large, sobre los mismos textos, para elegir el agrupamiento con métricas registradas.
4. Integrar Pi coding agent con herramientas acotadas y una interfaz gráfica para generar al menos seis fichas en inglés con evidencia, registrar cada decisión humana con su motivo y demostrar una personalización reversible.
5. Evaluar el prototipo frente al proceso manual con seis pares de temas y dos revisores externos ciegos, para determinar si alcanza 40 % de reducción del tiempo mediano, 90 % de respaldo factual y utilidad media de 4 sobre 5, y publicar tres videos cuyos resultados se reporten sin atribución causal.

El estado de cada objetivo está en la sección 8 y el de cada criterio en la Tabla 12. La utilidad se mide con anclas de 1 a 5 fijadas en la Tarea 1: 1, no utilizable; 2, cambios mayores; 3, revisión sustancial; 4, cambios menores; 5, lista para decidir. La meta se calcula con los dos revisores externos; la valoración del autor se informa aparte. El tiempo de la meta del 40 % es el tiempo activo desde el inicio de la búsqueda hasta la decisión, sin pausas; el cronómetro previsto para Earlywindow mide solo un tramo de ese proceso. **[PENDIENTE: calibrar la rúbrica con los revisores; resolver cómo se satisface la comparación de embeddings con el diseño local; registrar búsqueda, filtrado y pausas en ambas condiciones o declarar la desviación.]**

# Alcance

## Alcance de la solución seleccionada

El alcance cambió dos veces desde la propuesta. La Tabla 4 separa lo acordado, lo construido y lo decidido el 20 de octubre de 2026, que aún no está construido ni comunicado al tutor.

**Tabla 4.** Evolución del alcance.

| Elemento | Acordado en la Tarea 3 | Construido (Tareas 5 a 7) | Decidido el 20 de octubre |
|---|---|---|---|
| Fuentes | X principal; Reddit con permiso; YouTube de respaldo | 100 publicaciones de X, 99 tras limpieza | Motor diario con siete fuentes (Tabla 7); X bajo demanda; Reddit y YouTube fuera |
| Embeddings | Qwen3 local y text-embedding-3-large | Qwen3-Embedding-0.6B en CPU | Modelo local en la aplicación |
| Plataforma | Interfaz gráfica sobre Pi | Servidor Node local con Pi por RPC y navegador | Escritorio macOS en Electron y TypeScript sobre Pi; SQLite local |
| Modelo de lenguaje | Proveedor intercambiable | gpt-5.5 y GPT-6.1 Sol | Lo aporta el usuario; tope de pasos |
| Medición | Cronómetro externo | Ensayo de la Tarea 6 | Tiempo, decisión, motivo y utilidad registrados en la aplicación |

**Qué aborda.** El diagrama y el registro del proceso manual (objetivo 1). La arquitectura modular con permisos y matriz de selección (objetivo 2). La recolección con procedencia y la comparación de agrupamientos con parámetros y semillas registrados (objetivo 3). Una puntuación versionada con desglose visible, un agente con herramientas acotadas que redacta fichas en inglés con evidencia, y la decisión humana registrada (objetivo 4). La evaluación con seis pares de temas, dos revisores y tres videos (objetivo 5).

**Qué no aborda.** Publicación autónoma. Generación final de videos o imágenes. CRM, facturación, multiusuario o modelo de negocio. Predicción de conversión, abandono o valor de vida del cliente. Aprendizaje automático de pesos por retroalimentación. Comentarios, transcripciones y otros idiomas. El navegador integrado con humano en paralelo. Atribución causal de resultados comerciales.

**Supuestos.** La cercanía entre embeddings refleja temas útiles, con indicios en la Tarea 7 pero sin evaluación ciega. Las siete fuentes siguen sin tarifa durante la tesis, sin garantía contractual, y la gratuidad no acredita permiso para todos los tratamientos. El inicio de sesión con la cuenta de ChatGPT sigue disponible para uso gratuito y local. Habrá dos revisores externos calibrados antes de evaluar.

## Limitaciones y restricciones del proyecto

**Limitaciones**, impuestas por el entorno. La comunidad en inglés no tiene historial y el canal es hispanohablante, así que no se puede modelar conversión y los resultados comerciales se reportan solo de forma descriptiva. X cobra 0,005 USD por publicación leída según la tarifa observada el 19 de octubre de 2026, lo que limita cuánto se recolecta. El corpus de las Tareas 5 a 7 es una sola captura de 28 minutos y 37 segundos y no permite estimar crecimiento. Reddit no cuenta con autorización documentada y YouTube impone borrado a los 30 días para los metadatos previstos; ambas salen de la primera versión. Los términos de Anthropic prohíben usar sus suscripciones desde software de terceros. No existe un banco de pruebas que valide directamente la anticipación de temas editoriales: BERTrend se validó con casos (Boutaleb et al., 2024) y BackTrend (Zhou et al., 2026) cubre señales científicas. Sin dos revisores externos, la meta de utilidad queda no evaluable.

**Restricciones**, decididas por el proyecto o la institución. Periodo del 10 de agosto al 15 de noviembre de 2026. Un integrante que desarrolla, opera y es evaluado, mitigado con revisores ciegos. Hasta 30 USD mensuales de inferencia, aparte de X. Aprobación humana antes de usar una ficha, según la propuesta y el NIST AI RMF (Tabassi, 2023). Producto en inglés y textos de hasta 4.000 caracteres. macOS primero, Electron y TypeScript, todo local en SQLite. Tope de pasos por expediente, con 40 llamadas como valor ilustrativo. Sin credenciales, datos crudos de X ni opiniones de revisores en Git. **[PENDIENTE: volumen observado por fuente; términos de la integración con ChatGPT.]**

# Planificación y costos del proyecto

**Marco de gestión.** Iteraciones semanales con un incremento verificable ligado a cada entrega del sílabo: entregable, archivo de decisiones fechado y commit del prototipo. El trabajo delegado a agentes de programación se coordina con Orca y requiere autorización del autor por ronda. No se usó Scrum ni Kanban formal.

**Tabla 5.** Cronograma de 14 semanas: previsto (Tarea 1) y real.

| Semanas de 2026 | Previsto | Real al 20 de octubre |
|---|---|---|
| 1 (10 a 16 ago.) | Observaciones del Comité e instrumentos | Hecho (Tarea 1) |
| 2 a 4 (17 ago. a 6 sep.) | Credenciales, fuentes, línea base | Parcial: Tarea 2; fuentes el 12 de sep.; línea base sin iniciar |
| 5 (7 a 13 sep.) | Arquitectura, permisos y datos | Hecho (Tarea 3) |
| 6 a 7 (14 a 27 sep.) | Recolección; BERTopic frente a K-means | Con retraso: X el 29 de sep.; comparación el 6 de oct. |
| 8 (28 sep. a 4 oct.) | Puntuación; revisores | Parcial: ranking provisional (Tarea 5); revisores sin identificar |
| 9 a 10 (5 a 18 oct.) | Pi, interfaz, fichas; videos 1 y 2 | Parcial: Tareas 6 y 7; videos sin verificar |
| 11 (19 a 25 oct.) | Prueba ciega; video 3 | En curso: fuentes, Earlywindow y este borrador |
| 12 a 14 (26 oct. a 15 nov.) | Análisis, corrección, prototipo reproducible | **[PENDIENTE]** |

La integración de Pi se adelantó; la recolección y la comparación se retrasaron; la línea base, los revisores y los videos son la deuda principal. El tutor anunció el 13 de noviembre de 2026 como fecha probable de entrega final y defensa; el periodo oficial termina el 15. El prototipo final previsto es Earlywindow; una evaluación final sobre el prototipo de la Tarea 6 exigiría registrar una nueva decisión.

**Costos.** Un costo desconocido se informa como desconocido, nunca como cero. X costó hasta 0,55 USD por 100 publicaciones más una prueba de 10, estimado con la tarifa observada y sin factura verificada. La inferencia tiene un presupuesto de hasta 30 USD mensuales aparte de X; el servicio conversacional de las Tareas 5 y 6 tiene tarifa desconocida. Los embeddings locales no tuvieron cargo y las siete fuentes del motor no tienen tarifa encontrada, sin garantía contractual. Claude Max, ChatGPT Pro y Cursor son recursos de desarrollo, no créditos del sistema. **[PENDIENTE: diagrama de Gantt; cierres de Brightspace de las semanas 10 a 12; calendario de construcción de Earlywindow; imputación de equipo, dominio, Apple Developer y horas del autor; análisis financiero sin retorno mientras no exista línea base.]**

# Descripción de estudios realizados

La Tarea 2 revisó diez estudios de 2022 a 2026. La Tabla 6 los condensa.

**Tabla 6.** Estudios revisados.

| Autor y año | Enfoque y resultado | Límite para este proyecto |
|---|---|---|
| Grootendorst (2022) | BERTopic (UMAP, HDBSCAN y c-TF-IDF) da temas coherentes y separa agrupamiento y descripción | Prepublicación |
| Egger y Yu (2022) | Cuatro modelos temáticos en 31.800 tuits; BERTopic y NMF distinguen temas | Otro dominio |
| Zhang et al. (2022) | K-means sobre embeddings contextuales, competitivo frente a modelos neuronales | No mide utilidad editorial |
| Yao et al. (2023) | ReAct, razonar y actuar, mejora frente a solo actuar | Errores de búsqueda persisten |
| Gao et al. (2023) | Generación con citas: texto fluido sin respaldo completo | Preguntas, no fichas |
| Min et al. (2023) | Verificación por afirmación atómica detecta errores ocultos | Biografías y Wikipedia |
| Noy y Zhang (2023) | Experimento con 453 profesionales: 40 % menos tiempo, 18 % más calidad | Solo escritura |
| Csaszar et al. (2024) | Un modelo genera y evalúa estrategias de forma comparable a humanos | No mide adquisición |
| Feng et al. (2026) | Explicaciones contextualizadas, 759 participantes: mejor percepción e intención | Intención no es utilidad |
| Klimashevskaia et al. (2024) | Revisión del sesgo de popularidad: la exposición se concentra | Poca evidencia con usuarios |

Dos lecciones guiaron el diseño. Un agrupamiento más complejo no es mejor de antemano (Zhang et al., 2022); por eso se compararon BERTopic y K-means sobre las mismas representaciones. Una cita no garantiza respaldo (Gao et al., 2023; Min et al., 2023); por eso la meta del 90 % cuenta afirmaciones respaldadas, no enlaces.

**Detección temporal y anticipación.** Las Tareas 5 y 6 agruparon un corte estático de media hora. BERTrend (Boutaleb et al., 2024) muestra lo que ese diseño no puede hacer: entrena un modelo por corte temporal, fusiona temas de cortes consecutivos, acumula popularidad que decae sin documentos nuevos y separa ruido, señal débil y señal fuerte con percentiles sobre una ventana deslizante. La siguiente iteración toma de ahí la idea de señales que persisten día a día. BERTrend señaló la falta de métricas para señales débiles; BackTrend (Zhou et al., 2026) propone un banco de pruebas para señales científicas, con F1 de 10,1 % para su mejor sistema. Los ciclos de atención se acortan con los años (Crane y Sornette, 2008; Lorenz-Spreen et al., 2019). Ninguna herramienta de ideación para YouTube revisada el 19 de octubre de 2026 documenta la combinación de fuentes externas, series temporales por tema y fichas con afirmaciones enlazadas; es una hipótesis sin cuentas de prueba.

**Vacío.** Los diez estudios no evalúan el ciclo completo para un operador único: señales de varias fuentes, agrupamiento temporal, ficha con respaldo verificable y decisión registrada, frente al proceso manual. La revisión fue exploratoria. **[PENDIENTE: decidir si una prueba retrospectiva entra en la tesis; ampliar la bibliografía sobre utilidad en recomendación y sesgos de modelos de lenguaje, como pidió el Comité.]**

# Desarrollo del proyecto

El proyecto construyó un arnés híbrido y modular sobre Pi coding agent: piezas deterministas recogen publicaciones, las agrupan y ordenan las ideas con una fórmula visible; un modelo de lenguaje redacta la ficha y el operador la acepta, edita o rechaza con motivo. Entre el 29 de septiembre y el 13 de octubre de 2026 se midieron tres iteraciones sobre un lote de 99 publicaciones de X (Tareas 5, 6 y 7). El 20 de octubre se decidió el diseño de la siguiente iteración, Earlywindow, que todavía no tiene código.

## Diseño de la solución

**Enfoque.** Desarrollo tecnológico aplicado con comparación intrausuario (Tarea 1, §6.1). Cada iteración fija un protocolo, ejecuta, mide y registra la decisión. El rediseño del 19 y 20 de octubre no estaba en el cronograma y responde a dos hallazgos: un corte estático no permite medir tendencias y el ranking actual no mide relevancia.

**Principios de diseño.** Cuatro responsabilidades separadas:

1. **Evidencia.** Adaptadores de solo lectura traen ítems con fuente, fecha, URL y texto.
2. **Cálculo.** Agrupamiento y puntuación deterministas, recalculables desde datos, pesos y semillas guardados.
3. **Síntesis.** El modelo de lenguaje explica las opciones y redacta la ficha. No calcula el puntaje base.
4. **Decisión.** Solo el operador aprueba. El modelo no tiene herramienta para aprobar ni publicar.

De Pi se adoptaron el ciclo modelo, herramienta y resultado, la sesión persistente, la lista de herramientas permitidas, los eventos para auditoría y la abstracción del proveedor (Earendil Works, 2026), siguiendo la idea de ReAct (Yao et al., 2023). Se rechazaron las herramientas de terminal y escritura de archivos.

**Pipeline de datos.** Siete pasos: fuentes autorizadas, limpieza y partición, embeddings, agrupamiento y evaluación, priorización, ficha con fuentes y decisión humana. Reglas fijadas antes de recolectar (Tarea 3): se descartan registros sin texto o fecha, duplicados y textos que no estén en inglés; cada entrada se limita a 4.000 caracteres; los registros se ordenan por fecha y se dividen 60/20/20 en ajuste, validación y prueba final, y UMAP y los agrupadores se ajustan solo con el 60 % más antiguo. De las tres fuentes previstas solo se usó X, con 100 publicaciones, lejos de la meta de 500 por fuente; el acceso no autoriza redistribuir los textos. El prototipo guardó en JSON locales las entidades ítem de evidencia, oportunidad, ficha versionada, decisión con motivo obligatorio, evento y configuración de ejecución; la entidad resultado, que vincula video y métricas, no existe.

**Ranking explicable.** La propuesta define cinco criterios con pesos versionados; el prototipo implementó una fórmula provisional con tres:

Puntuación = 100 × (0,60 A + 0,25 D + 0,15 R)

donde A es la afinidad (proporción de textos elegibles del grupo que contienen algún término del enfoque), D la diversidad (autores coincidentes sobre cinco, con tope en 1) y R la recencia (media de las fechas normalizadas de los textos elegibles). Un filtro léxico excluyó 16 de 79 textos de desarrollo antes de puntuar (Tarea 5). La interfaz muestra el desglose por criterio y las publicaciones de apoyo. La fórmula es explicable, pero la Tarea 7 mostró que no es informativa (sección 7.3).

**Agente conversacional sobre Pi.** Corre en Pi por RPC dentro de un servidor Node local, con cuatro herramientas y nada más: calcular el ranking, entregar la evidencia de una oportunidad, leer fichas y decisiones, y guardar un borrador de ficha. Los textos recuperados se tratan como datos, no como instrucciones. Al guardar una ficha se validan identificadores, versión y citas literales; esa validación prueba la procedencia de una cita, no su veracidad. Aceptar, editar y rechazar son botones del operador con motivo obligatorio.

**Criterios de evaluación, fijados antes de ejecutar.** Para el agrupamiento: cobertura de al menos 80 %, silueta coseno válida en cinco semillas, estabilidad ARI y claridad humana ciega de al menos 3,5 sobre 5 (Tarea 3); la Tarea 6 añadió mejora media sobre la referencia y caída de ARI de 0,05 o menos. Para el sistema: reducción de al menos 40 % en el tiempo mediano de seis pares manual y asistido, respaldo factual de al menos 90 % y utilidad media de al menos 4 sobre 5 según dos revisores externos (Tarea 1). La silueta mide separación entre grupos de −1 a 1 (Rousseeuw, 1987); el ARI mide acuerdo entre dos agrupamientos (Hubert y Arabie, 1985). Ninguna mide calidad editorial, por eso la claridad humana es condición de elegibilidad.

**Diseño de la siguiente iteración: Earlywindow.** Es diseño, no resultado: no hay código y el cambio de fuentes está pendiente de comunicar al tutor. Cambia porque el ensayo de la Tarea 6 midió la ayuda en la redacción, no la detección de tendencias, y porque el lote estático no permite medir evolución. La idea central es la ventana de oportunidad: el tramo en que un tema pasa de señal débil a señal fuerte; la hipótesis, no medida, es que grabar en ese tramo rinde más que grabar cuando el tema ya está saturado.

Dos capas. Un **motor de tendencias** responde qué se mueve y desde cuándo: corre a diario, es determinista y no usa el modelo de lenguaje salvo para nombrar señales. Apila ítems en señales persistentes, mide por señal ítems, fuentes y autores, clasifica cada una por su curva (ruido, débil, fuerte, apagándose) y la filtra por el perfil del canal, con BERTrend como antecedente. Un **agente investigador** responde por qué importa, solo sobre expedientes filtrados, con herramientas y tope de pasos. El expediente es el contrato entre ambos: etapa, curva de 30 días, confianza y entre 5 y 10 ítems con URL y fecha por señal; el agente devuelve dos o tres ángulos con sus ítems. Con pocos días de datos, un indicador marca el tablero como "exploración".

**Tabla 7.** Fuentes del motor en la primera versión, según los informes de investigación del 19 y 20 de octubre de 2026; no es asesoría legal.

| Fuente | Señal que aporta | Condición documentada |
|---|---|---|
| Hacker News | Historias, puntos y comentarios | API disponible; tensión con los términos del sitio |
| GitHub | Repositorios y estrellas | API pública; restricciones sobre contenido y datos personales |
| Bluesky | Publicaciones e interacción | Lectura pública; atender borrados |
| Wikipedia Pageviews | Visitas diarias por artículo | CC0 |
| npm | Descargas diarias por paquete | API; condiciones por verificar |
| Stack Exchange | Preguntas, etiquetas y votos | CC BY-SA con atribución; 10.000 solicitudes diarias |
| arXiv | Artículos nuevos por categoría | Metadatos CC0; tres segundos entre solicitudes |

X pasa a evidencia puntual bajo demanda del agente, con presupuesto acotado. Reddit queda fuera por falta de autorización documentada y YouTube por su borrado a los 30 días. El cambio sustituye el corpus acordado en la Tarea 3 y responde a la petición del Comité de verificar permisos, cuotas y términos; la gratuidad de acceso no autoriza por sí sola todos los tratamientos.

**Forma de la aplicación.** Escritorio macOS en Electron y TypeScript, sobre las librerías de Pi sin bifurcarlas. Todo local en SQLite y exportable; un proceso en segundo plano correrá el motor a diario. Embeddings con un modelo local del tipo Qwen3-Embedding-0.6B. El modelo de lenguaje lo aporta el usuario con su cuenta de ChatGPT o una clave de API. Tope de pasos por expediente con botón para continuar. Perfil del canal creado con texto libre y tres o cuatro preguntas del agente, versionado. La aplicación registra tiempo de expediente a decisión, decisión con motivo y utilidad de 1 a 5; ese cronómetro mide un tramo del proceso y no sustituye la métrica de tiempo activo de la Tarea 1. **[PENDIENTE: reglas versionadas de asociación, crecimiento, clasificación y confianza; unidad de análisis por fuente; fórmula y pesos de Earlywindow fijados antes de evaluar; auditoría de cada fuente por operación; maquetas; política de conservación y borrado; calendario de construcción y congelación del protocolo.]**

## Desarrollo de la solución

**Datos.** Una sola solicitud a la API oficial de X el 29 de septiembre de 2026, en inglés, sobre agentes de IA, agentes de programación, Claude Code y Cursor AI, sin retuits ni respuestas. Se recuperaron 100 publicaciones y quedaron 99 textos de 94 autores tras eliminar un duplicado, en una ventana de 28 minutos y 37 segundos. Partición: 59 de ajuste, 20 de validación y 20 de prueba final. Costo: hasta 0,55 USD con una prueba previa, sin factura verificada. Sesgo declarado: "agent" domina el lote. La ventana impide medir crecimiento y la prueba final pertenece a la misma ventana.

**Preprocesamiento.** Reglas de 7.1. Cada texto se representó con Qwen3-Embedding-0.6B (1.024 dimensiones, normalización L2, en CPU; Qwen, s. f.) y se redujo con UMAP a 5 dimensiones con 15 vecinos, distancia mínima 0 y métrica coseno, ajustado solo con los 59 textos de ajuste (McInnes et al., 2018). Semillas 42 a 46. Los 20 textos de prueba no entraron en inferencia, agrupamiento ni conversación hasta la Tarea 6.

**Alternativas técnicas comparadas.** Tres agrupadores sobre los mismos 79 textos de desarrollo, embeddings y coordenadas UMAP por semilla (Tarea 6), en respuesta a la petición del Comité de probar un algoritmo adicional a BERTopic: K-means 10 (k-means++, 10 inicializaciones, 300 iteraciones), referencia de la Tarea 5; K-means 5, igual con cinco grupos; y BERTopic con HDBSCAN de grupo mínimo 10 y min_samples 5, con c-TF-IDF para describir temas (Grootendorst, 2022). La comparación se apoya en Zhang et al. (2022). No se ejecutaron text-embedding-3-large por API ni K-means 15.

**Justificación de la alternativa seleccionada.** K-means 5 se seleccionó a las 22:09:48 del 6 de octubre de 2026, antes de representar los 20 textos de prueba, porque cumplió las reglas de la Tarea 6: cobertura del 100 %, silueta válida en las cinco semillas, mejora media sobre la referencia y caída de ARI de 0,018. No se completó la condición de claridad humana de la Tarea 3, así que la selección es provisional y una desviación del protocolo. La mejora es mínima, 0,0017 en silueta de validación, con dos semillas a favor y tres en contra; se adoptó por menor fragmentación, no por superioridad demostrada. BERTopic dejó como ruido los 20 textos de validación. El resultado no justifica usar el mismo método en Earlywindow sin repetir la comparación.

**Arquitectura del prototipo construido.** La Figura 2 muestra las piezas, en un repositorio Git independiente: scripts de Python para el baseline, la comparación y la interpretabilidad; un módulo de Node para filtro, ranking, evidencia y fichas; un servidor local con puente RPC a Pi y la interfaz; una extensión de Pi para búsqueda en X con tope de costo; y archivos JSON con parámetros, versiones, huellas, métricas y tiempos. En la Tarea 5 el agente usó gpt-5.5 sobre Pi 0.99.1; su primera conversación no propuso ideas porque buscaba frases completas, y el fallo corregido quedó registrado. En la Tarea 6 se pasó a Pi 1.0.0 con GPT-6.1 Sol en un servicio compatible con OpenAI, de tarifa desconocida.

![Figura 2. Arquitectura del prototipo construido en las Tareas 5 y 6. Pendiente: diagrama formal de componentes y despliegue, del prototipo y de Earlywindow.](archive/output/tareas/evidencias-tarea-08/figura-5-arquitectura-prototipo.png)

![Figura 3. Interfaz del prototipo de la Tarea 5: a la izquierda la conversación; arriba a la derecha las tres oportunidades con puntuación (94,7; 91,2 y 91,0), desglose por criterio y aviso de que la muestra cubre 28 minutos; abajo la ficha en inglés aceptada, con motivo y botones Aceptar, Guardar edición y Rechazar.](archive/output/tareas/evidencias-tarea-08/interfaz-completa.png)

**Pruebas.** Diez controles locales sin inferencia (ranking, cambio de enfoque, falta de evidencia, citas inválidas, motivo obligatorio, edición y recuperación), 10 de 10 en las Tareas 5 y 6; seis controles HTTP y con Pi real, 6 de 6 tras corregir una falsa abstención; ocho controles integrados del ensayo, 8 de 8. No son un benchmark de calidad ni una auditoría de seguridad.

**Tabla 8.** Herramientas y versiones.

| Ámbito | Herramienta |
|---|---|
| Lenguajes y entorno | Python 3.12.12; Node 26.10.0; macOS arm64 con CPU local; uv; Git y GitHub |
| Arnés y modelos de lenguaje | Pi coding agent 0.99.1 (Tarea 5) y 1.0.0 (Tarea 6); gpt-5.5 (Tarea 5); GPT-6.1 Sol (Tarea 6) |
| Embeddings | Qwen3-Embedding-0.6B; sentence-transformers 5.7.0; transformers 4.57.6; torch 2.14.0 |
| Agrupamiento | umap-learn 0.5.12; scikit-learn 1.9.1; hdbscan 0.8.44; bertopic 0.17.4 |
| Interpretabilidad | shap 0.53.0; lime 0.2.0.1 |

No se usaron herramientas low-code ni no-code. Los asistentes de programación (Claude Max y ChatGPT Pro con Codex) son recursos de desarrollo, separados de la inferencia del sistema.

**Control de versiones y reproducibilidad.** Las Tareas 5 y 6 tienen commits identificados en el repositorio privado: c4dda35 y 5c6b2c4, 5bb006f y e42394f; la Tarea 7 sigue sin commit. La copia pública saneada está en https://github.com/miwgel/singularidev-editorial-prototype, snapshot 3dff908, sin credenciales, textos de X ni sesiones. El manifiesto fija las versiones y los archivos de resultados guardan parámetros, semillas, huellas SHA-256, métricas y tiempos. La Tarea 6 reprodujo exactamente las siluetas y asignaciones de la Tarea 5; la Tarea 7 reprodujo los grupos de K-means 5 y las puntuaciones de K-means 10 de la Tarea 5 (94,67; 91,15 y 90,97). El lote de X no se redistribuye, así que repetir el experimento exige datos autorizados, y la conversación depende de un proveedor no determinista. **[PENDIENTE: comparación de embeddings o desviación registrada; pruebas de robustez ante fallos de fuentes; inventario de asistentes de IA usados; commit de la Tarea 7; ejemplo sintético compartible; reproducibilidad de Earlywindow ante el tribunal; personalización reversible.]**

## Resultados y Discusión.

Los resultados vienen de tres iteraciones sobre el mismo lote de X: baseline y prototipo conversacional (Tarea 5), comparación de agrupamiento y ensayo humano (Tarea 6) e interpretabilidad (Tarea 7). La evaluación final con revisores externos no se ha hecho.

**Comparación de agrupamiento**

**Tabla 9.** Media y desviación estándar de cinco ejecuciones (Tarea 6).

| Métrica | K-means 10 | K-means 5 | BERTopic |
|---|---|---|---|
| Silueta, ajuste | 0,1257 ± 0,0198 | 0,0904 ± 0,0023 | 0,1129 ± 0,0248 (a) |
| Silueta, validación | −0,0182 ± 0,0243 | −0,0165 ± 0,0229 | No definida |
| Silueta, prueba | −0,0104 ± 0,0291 | 0,0349 ± 0,0101 | No definida |
| Cobertura, validación y prueba | 100 % y 100 % | 100 % y 100 % | 0 % y 2 % (b) |
| ARI medio, validación y prueba | 0,9028 y 0,8859 | 0,8848 y 0,8554 | No interpretable |
| Grupos de un texto, validación | 4,4 | 2,6 | No aplica |

Notas. K-means 10 es la referencia. ARI medio de las diez parejas de semillas. (a) Cuatro ejecuciones válidas de cinco. (b) Asignó cero o un texto de veinte por ejecución.

La referencia se reprodujo exactamente respecto de la Tarea 5. K-means 5 cumplió la regla y quedó seleccionado antes de abrir la prueba final: su ventaja en validación es 0,0017, la silueta sigue negativa y dos semillas lo favorecen frente a tres. Reduce la fragmentación de 4,4 a 2,6 grupos de un solo texto. En prueba final su silueta fue positiva pero cercana a cero, y el ARI baja de 0,8859 a 0,8554. BERTopic no alcanzó la cobertura mínima; HDBSCAN directo también dejó como ruido los veinte textos de validación. **Interpretación:** K-means 5 es una elección provisional por menor fragmentación, no por superioridad demostrada; los grupos tuvieron poca separación; la prueba final ya se consumió. Hay una desviación frente a la Tarea 1, que ponderaba la coherencia humana ciega con 40 %: la selección usó solo cobertura, silueta y estabilidad.

**Prototipo conversacional y ensayo humano**

El operador conversa con el sistema, revisa ideas ordenadas con sus fuentes, recibe una ficha en inglés y decide con motivo. Tiempos de respuesta en la Tarea 5: tres ideas en 22,48 segundos, guardar una ficha en 24,08, cambiar de tema en 16,14 y detectar falta de evidencia en 6,39. El 29 de septiembre a las 21:16 el operador aceptó la ficha "Agent Permissions for Solo Founders" (Figura 3). Sus cinco afirmaciones tienen citas que coinciden con los textos originales; eso identifica la fuente, pero no confirma que la respalde.

**Ensayo cronometrado.** El operador elaboró cuatro fichas en dos temas, en orden manual, asistida, asistida, manual, con cuatro fuentes preseleccionadas y un límite de cinco minutos por ejercicio. El cronómetro incluye lectura, espera, edición y revisión.

**Tabla 10.** Ensayo de uso con un solo operador (Tarea 6).

| Ejercicio | Tiempo | Estado declarado | Utilidad autovalorada | Palabras |
|---|---|---|---|---|
| 1. Manual, tema permisos | 296,034 s | Completa | 2 | 97 |
| 2. Asistida, tema permisos | 170,119 s | Completa | 4 | 160 |
| 3. Asistida, tema programación | 130,293 s | Completa | 5 | 168 |
| 4. Manual, tema programación | 300 s, límite | Incompleta | 3 | 77 |

Se completaron dos de dos asistidas y una de dos manuales; la mediana asistida fue 150,2 segundos y solo las asistidas cumplieron la extensión sugerida de 120 a 180 palabras. **No se calcula un porcentaje de ahorro**: la ficha manual incompleta tiene tiempo censurado en 300 segundos y no se imputa como terminada. Con dos tareas por condición, un operador que es también el autor y orden fijo, el ensayo es una señal favorable, no una medición del objetivo. Los costos observados: X hasta 0,55 USD, embeddings sin cargo y servicio conversacional de tarifa desconocida, por lo que el límite de 30 USD mensuales no se puede verificar.

**Interpretabilidad**

La Tarea 7 explicó las dos piezas que deciden qué ve primero el operador, el agrupamiento K-means 5 y el ranking, sobre los 79 textos de desarrollo, con tres técnicas. SHAP (Lundberg y Lee, 2017) sobre un sustituto, una regresión logística con 103 palabras y 6 rasgos de formato que imita el agrupamiento en el 62 % de los casos, frente a 25 % de la clase mayoritaria. LIME (Ribeiro et al., 2016) sobre el pipeline real, con 500 variaciones del texto más central de cada grupo y R² local de 0,45 a 0,60. Y valores de Shapley exactos (Shapley, 1953) del ranking, exactos porque la fórmula es lineal, aunque no validan relevancia. La Figura 4 resume SHAP y Shapley; la Tabla 11, los hallazgos.

![Figura 4. a) Importancia SHAP de los rasgos que acercan un texto a su grupo; naranja indica formato o filtro, no tema. b) Puntos que aporta cada criterio a cada grupo (Tarea 7).](archive/output/tareas/evidencias-tarea-07/figura-1-shap-y-ranking.png)

**Tabla 11.** Hallazgos de interpretabilidad (Tarea 7).

| Pieza y hallazgo | Qué significa |
|---|---|
| Recencia (15 %) decide el orden; el primer grupo gana por 290 segundos de diferencia media | El primero es el más fresco, no el más relevante |
| Afinidad (60 %) vale 1 en cuatro de cinco grupos; "agent", término de búsqueda, aparece en 52 de 63 textos elegibles (83 %) | Mide la consulta, no el enfoque editorial |
| Diversidad (25 %) está al tope en todos los grupos; su valor de Shapley es cero | Un cuarto de la fórmula no distingue posiciones |
| El mismo grupo gana en las 171 combinaciones de pesos probadas | Solo la recencia distingue; no demuestra robustez fuera de este lote |
| El filtro léxico es el rasgo más fuerte del sustituto y excluye 12 de 17 textos de un grupo; enlaces, hashtags, menciones, emoji y longitud reúnen el 19 % de la importancia | Una regla manual decide qué se ve; los grupos parecen mezclar tema y estilo |
| Tres grupos con tema claro (Dots de OpenAI, Claude Code, finanzas) y uno difuso; al borrar tres palabras, 2 de 5 textos cambian de grupo | Temas reconocibles sin evaluación ciega; asignaciones frágiles |

**Interpretación.** Para el enfoque y el lote analizados, el orden de los cuatro primeros grupos depende de la recencia, así que el ranking no puede tomarse como medida de valor editorial; el valor observado está en organizar fuentes y acelerar la redacción. Esto responde a la petición del Comité de analizar la sensibilidad de los pesos con un resultado que cambia el enfoque: ajustar pesos no sirve mientras las señales estén saturadas. Límites: SHAP explica un sustituto con fidelidad del 62 %, LIME llega a R² de 0,60 y los datos cubren media hora.

**Discusión frente a los objetivos y criterios de éxito**

**Tabla 12.** Estado de cada criterio de éxito al 20 de octubre de 2026. El estado por objetivo está en la sección 8.

| Criterio | Meta | Evidencia y estado |
|---|---|---|
| Tiempo mediano, métrica principal | Reducción de al menos 40 % en seis pares | Dos asistidas completas y una manual censurada; sin porcentaje calculable |
| Respaldo factual | Al menos 90 %, dos revisores | Citas literales prueban procedencia, no respaldo; falta |
| Utilidad | Al menos 4 sobre 5 según dos revisores externos | Solo autovaloración de 4 y 5; falta la evaluación externa |
| Claridad de los grupos | Al menos 3,5 sobre 5, ciega | Sin calificar; falta |
| Piloto de tres videos | Resultados descriptivos en siete días | Sin evidencia de publicación; falta |
| Sensibilidad de pesos (Comité) | Analizar el efecto de los pesos | 171 combinaciones, mismo ganador; hecho, con hallazgo negativo |
| Presupuesto de inferencia | Hasta 30 USD mensuales, aparte de X | Conversación de costo desconocido; no verificable |

**Lo demostrado.** El prototipo conversa, ordena ideas, redacta fichas con citas literales y registra la decisión humana. Los resultados se reproducen entre entregas y existe una copia pública saneada. Se compararon dos algoritmos de agrupamiento y se mostró, con Shapley exacto, que en este lote el orden lo decide la recencia. La fortaleza es la trazabilidad, que el proceso manual no ofrece.

**Lo preliminar y lo débil.** Cuatro ejercicios de un operador no permiten afirmar el 40 %, y las valoraciones de 4 y 5 son del autor. La selección de K-means 5 es una mejora pequeña y dependiente de la semilla sobre un lote de 28 minutos. La debilidad es la señal: los grupos tienen separación cercana a cero y el ranking reproduce la consulta y la hora de publicación. El prototipo de las Tareas 5 a 7 queda como referencia experimental, no como base de código; sus resultados de agrupamiento no se trasladan a las nuevas fuentes sin repetir la comparación, y es una hipótesis que un motor diario permita medir crecimiento en lugar de recencia. **[PENDIENTE: registro de carga; seis pares con temas al azar; dos revisores calibrados y calificación ciega de claridad; auditoría factual por afirmación; tres videos; costo real del servicio conversacional; comunicar al tutor el cambio de corpus y reprogramar la evaluación sobre Earlywindow.]**

## Implicaciones éticas

El sistema apoya una decisión de riesgo limitado: qué video preparar. Aun así, procesa textos de terceros, envía contenido a proveedores de modelos de lenguaje y produce puntuaciones que pueden inducir más confianza de la que merecen. El análisis toma como referencia el NIST AI RMF (Tabassi, 2023) y los principios de transparencia, rendición de cuentas, equidad y privacidad (Corrêa et al., 2023).

**Tabla 13.** Riesgos éticos con evidencia. "Aplicada" consta en el prototipo; "propuesta" no consta implementada.

| Riesgo y evidencia | Mitigación y estado |
|---|---|
| Falsa precisión: 95 sobre 100 decidido por segundos de publicación (Tarea 7) | Desglose visible por criterio, aplicado; aviso de empate bajo 3 puntos, propuesto |
| Sesgo circular: "agent" en el 83 % de los textos elegibles | Afinidad semántica sin términos de búsqueda y aviso si un término supera 50 %; propuesta |
| Exclusión silenciosa: el filtro elimina 12 de 17 textos de un grupo, incluido uno sobre seguridad | Exclusión como etiqueta visible con conteo; propuesta |
| Sesgo de formato y popularidad: formato con 19 % de la importancia en el sustituto; los recomendadores refuerzan lo popular (Klimashevskaia et al., 2024) | Limpiar formato antes del embedding y revisar concentración de cuentas; propuesta |
| Agenda de proveedores: "claude", "openai" y "dots" definen grupos | Exigir fuente primaria en fichas sobre productos; propuesta |
| Respaldo aparente: una cita literal no confirma la afirmación (Gao et al., 2023) | Citas comprobadas por código, aplicada; auditoría humana, pendiente |
| Complacencia del modelo (Nguyen et al., 2026) e instrucciones ocultas en textos externos; ninguna se midió aquí | Herramientas acotadas, textos tratados como datos y decisión humana, aplicadas en parte; prueba con textos maliciosos pendiente |
| Exclusión lingüística y lectura causal de métricas: solo inglés, sin videos publicados | Límite declarado; reporte solo descriptivo, en el protocolo |

**Permisos y términos de las fuentes.** La política de X limita la redistribución y exige borrar en 24 horas lo borrado en X tras solicitud (X Corp., s. f.); el proyecto no redistribuye textos. Reddit exige acuerdo comercial y no se usó. YouTube impone conservación y borrado según el tipo de dato, 30 días para los metadatos previstos, y métricas derivadas solo con aprobación (Google, 2026); no se usó. Las siete fuentes del motor tienen las condiciones de la Tabla 7 y ninguna está implementada. Entregar textos de X a los revisores podría ser redistribución; la contingencia es compartir identificadores o enlaces públicos.

**Privacidad y envío de datos a proveedores.** Los embeddings se calculan en local. La conversación envía publicaciones al proveedor del modelo mediante la cuenta configurada en Pi. Credenciales, publicaciones, vectores y sesiones quedan fuera de Git; la copia pública solo incluye métricas agregadas autorizadas. La retención del servicio conversacional es desconocida. Las opiniones textuales de los revisores no se publicarán. El autor decidió usar la vía abierta de inicio de sesión con la cuenta de ChatGPT durante la tesis, con una aplicación gratuita y local, y solicitar acceso comercial antes de cobrar. No se usarán suscripciones de Anthropic en el arnés porque sus términos lo prohíben.

**Decisión humana y rendición de cuentas.** El modelo no puede aprobar una ficha. El operador acepta, edita o rechaza, y el sistema registra actor, versión, acción, motivo y fecha. Una puntuación alta puede inducir sobreconfianza aunque mida la hora de publicación; el ranking debe presentarse como apoyo de lectura, no como predicción.

**Riesgos operativos solicitados por el Comité.** Aplicados: el cambio de modelo entre tareas se registra con modelo, versión de Pi y configuración por ejecución; la variabilidad entre ejecuciones (ARI de prueba de 0,6385 a 1,0000 en la Tarea 6) se controla con semillas y versiones fijadas y selección antes de la prueba. Decididos, no implementados: fuentes sin tarifa identificada y X bajo demanda ante cambios de costo o términos; varias fuentes con relleno desde las que tienen historial ante el fallo de una; motor diario sin recencia hasta tener siete días ante la variación de tendencias. Los revisores siguen sin identificar; se prevén cuatro invitaciones para dos y un suplente. El calendario es el riesgo mayor: construir Earlywindow antes de la evaluación final. **[PENDIENTE: política escrita de conservación, borrado y envío a proveedores por fuente; condiciones de Hacker News, Stack Exchange y Bluesky por operación; consentimiento de los revisores; condiciones vigentes de cada vía de acceso al modelo; vincular cada ficha aprobada con su video; prueba con una fuente caída; matriz de riesgos con responsable, probabilidad e impacto.]**

# Conclusiones y Recomendaciones

Las conclusiones son preliminares. Se basan en un lote de 99 textos de X publicados en 28 minutos y en un ensayo con un único operador, y no se generalizan fuera de ese caso.

1. **Objetivo 1.** La línea base no está acreditada. Hay un diagrama preliminar y dos fichas manuales cronometradas, una completa en 296,0 segundos y otra incompleta al límite de 300. La estimación de 20 horas semanales sigue siendo una estimación.
2. **Objetivo 2.** El diseño histórico está documentado: la matriz previa favoreció el arnés modular y la Tarea 3 fijó pipeline, reglas y criterios. El rediseño hacia Earlywindow está decidido, pero su arquitectura detallada, sus permisos por operación y su validación están pendientes.
3. **Objetivo 3.** La comparación de agrupamiento se ejecutó con selección provisional. Los grupos tuvieron poca separación: la silueta de validación fue negativa con K-means 10 y con K-means 5, que ganó por 0,0017; BERTopic asignó casi ningún texto. El ranking no mide relevancia: la recencia decidió el orden, la afinidad valió 1 en cuatro grupos por el término de búsqueda y la diversidad no distinguió posiciones; cambiar los pesos no lo corrige, porque el mismo grupo ganó en las 171 combinaciones. La comparación de embeddings por API no se ejecutó.
4. **Objetivo 4.** La integración y el registro funcionan: el sistema registra actor, versión, acción, motivo y fecha de cada decisión, y pasaron diez regresiones y ocho controles integrados. Una cita literal identifica la fuente, pero no prueba que la respalde. Las seis fichas evaluadas y la personalización reversible no están acreditadas.
5. **Objetivo 5.** Las metas no son evaluables todavía. El ensayo mostró una señal favorable para la redacción asistida (170,1 y 130,3 segundos, utilidad autovalorada 4 y 5), insuficiente para estimar el ahorro. No hay revisores externos, auditoría factual ni videos.

**Síntesis.** El prototipo conservó fuentes y decisiones. El ensayo mostró una señal favorable para la redacción asistida, insuficiente para estimar el ahorro previsto. No se evaluó la detección temporal de tendencias. Esa brecha motiva el rediseño decidido el 20 de octubre de 2026.

**Recomendaciones.** Para el operador: tratar el ranking como apoyo de lectura, con desglose visible y empate declarado bajo 3 puntos; exigir una fuente primaria antes de aceptar una ficha sobre un producto; mantener la aprobación humana registrada. Para el desarrollo: medir afinidad por similitud semántica sin los términos de búsqueda; retirar la recencia hasta tener siete días de datos y medir crecimiento entre ventanas; mostrar las exclusiones del filtro; no optimizar sobre el mismo lote, porque la prueba de la Tarea 6 ya está consumida. Para la gobernanza: aprobar una política de conservación y borrado antes de ampliar el corpus, y comprobar los términos de cada fuente antes de recolectar, porque el navegador no sustituye un permiso. **[PENDIENTE: una conclusión por objetivo con cada meta en estado alcanzada, no alcanzada o no evaluable, tras el ensayo con revisores, el registro de carga y el piloto.]**

# Trabajo futuro

**Lo que falta de esta tesis.** El tutor anunció el 13 de noviembre como fecha probable de entrega final y defensa; el periodo oficial termina el 15. Todo lo siguiente es plan, no resultado.

Siete frentes, en orden de dependencia:

1. **Aviso al tutor.** Comunicar el cambio de corpus principal (de X a siete fuentes con X bajo demanda), la meta de 500 publicaciones no alcanzada, el ranking con tres señales, la comparación de embeddings no ejecutada y la personalización sin verificar. Pendiente.
2. **Earlywindow 1.0.** Construir el prototipo final, empezando por integrar Pi con el módulo de tendencias, hasta una versión de evaluación congelada con regresiones. Decidido, sin código.
3. **Registro de carga y proceso manual.** Catorce días de registro real, previstos del 20 de octubre al 2 de noviembre, y diagrama validado en BPMN. Inicio no consta.
4. **Ensayo con revisores.** Seis pares de fichas evaluados a ciegas por dos revisores externos, auditoría factual por afirmación y tiempo activo en ambas condiciones. Revisores sin confirmar; calendario por reprogramar.
5. **Piloto.** Tres videos con ventana común de siete días y tabla descriptiva sin atribución causal. No verificado.
6. **Prueba retrospectiva.** Correr el motor sobre historial de Hacker News y GitHub en cortes semanales, solo con variables disponibles en cada corte, contra líneas base sin modelo. Propuesta, de resultado exploratorio.
7. **Entrega final.** Informe, presentación, demo de tres minutos y defensa, con las mismas cifras en los tres artefactos. Fechas de Brightspace pendientes.

**Riesgo de plazo.** El plan anterior congelaba la versión de evaluación el 26 de octubre sobre el prototipo de la Tarea 6 y preveía la evaluación externa hasta el 5 de noviembre. Construir Earlywindow antes de esa fecha no es realista con un solo ejecutor. Si no llega a tiempo, el cambio de alcance deberá registrarse y las Tareas 5 a 7 seguirán siendo evidencia histórica. **[PENDIENTE: fecha de congelación de Earlywindow y calendario del ensayo.]**

**Proyectos posteriores, fuera de la tesis.** SaaS multiusuario, versión para Windows, navegador integrado con el humano en paralelo, YouTube y Reddit en el motor cuando haya permisos, acceso comercial con cuenta de ChatGPT, ranking adaptativo con aprendizaje de pesos, otros idiomas, CRM y métricas de conversión, publicación autónoma y medición causal de la adquisición.

# Referencias bibliográficas

Las referencias consolidan las Tareas 1 a 7. **[VERIFICAR]** marca las que no se confirmaron en su fuente o tienen datos incompletos.

Asamblea Nacional del Ecuador. (2021). *Ley Orgánica de Protección de Datos Personales*. Registro Oficial Suplemento 459. [VERIFICAR]

Boutaleb, A., Picault, J., & Grosjean, G. (2024). BERTrend: Neural topic modeling for emerging trends detection. En *Proceedings of the Workshop on the Future of Event Detection (FuturED)* (pp. 1–17). Association for Computational Linguistics. https://doi.org/10.18653/v1/2024.futured-1.1

Brito Espejo, M. Á. (2026). *Arnés agéntico basado en modelos de lenguaje y análisis semántico de tendencias para priorizar ideas de contenido en YouTube orientadas a la adquisición de miembros para SingulariDev* [Propuesta de proyecto de titulación no publicada]. Universidad de Las Américas.

Comité de Evaluación de Proyectos MIA. (2026). *Reporte ejecutivo de evaluación de proyecto* [Informe no publicado]. Universidad de Las Américas. [VERIFICAR: nombre oficial del Comité]

Corrêa, N. K., Galvão, C., Santos, J. W., Del Pino, C., Pinto, E. P., Barbosa, C., Massmann, D., Mambrini, R., Galvão, L., Terem, E., & de Oliveira, N. (2023). Worldwide AI ethics: A review of 200 guidelines and recommendations for AI governance. *Patterns, 4*(10), Article 100857. https://doi.org/10.1016/j.patter.2023.100857 [VERIFICAR: lista de autores]

Crane, R., & Sornette, D. (2008). Robust dynamic classes revealed by measuring the response function of a social system. *Proceedings of the National Academy of Sciences, 105*(41), 15649–15653. https://doi.org/10.1073/pnas.0803685105 [VERIFICAR]

Csaszar, F. A., Ketkar, H., & Kim, H. (2024). Artificial intelligence and strategic decision-making: Evidence from entrepreneurs and investors. *Strategy Science, 9*(4), 322–345. https://doi.org/10.1287/stsc.2024.0190

Earendil Works. (2026). *Pi coding agent* (Versión 1.0.0) [Software]. GitHub. https://github.com/earendil-works/pi [VERIFICAR: versión a citar en la entrega final]

Egger, R., & Yu, J. (2022). A topic modeling comparison between LDA, NMF, Top2Vec, and BERTopic to demystify Twitter posts. *Frontiers in Sociology, 7*, Article 886498. https://doi.org/10.3389/fsoc.2022.886498

Feng, Y., Feuerriegel, S., & Shrestha, Y. R. (2026). Contextualizing recommendation explanations with LLMs: A user study. *Proceedings of the International AAAI Conference on Web and Social Media, 20*(1), 788–803. https://doi.org/10.1609/icwsm.v20i1.42667

Gao, T., Yen, H., Yu, J., & Chen, D. (2023). Enabling large language models to generate text with citations. En H. Bouamor, J. Pino, & K. Bali (Eds.), *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing* (pp. 6465–6488). Association for Computational Linguistics. https://doi.org/10.18653/v1/2023.emnlp-main.398

Google. (2026, 15 de octubre). *YouTube API Services: Developer policies*. https://developers.google.com/youtube/terms/developer-policies

Grootendorst, M. (2022). *BERTopic: Neural topic modeling with a class-based TF-IDF procedure* (arXiv:2203.05794) [Prepublicación]. arXiv. https://doi.org/10.48550/arXiv.2203.05794

Hubert, L., & Arabie, P. (1985). Comparing partitions. *Journal of Classification, 2*(1), 193–218. https://doi.org/10.1007/BF01908075

International Organization for Standardization & International Electrotechnical Commission. (2023). *Software engineering: Systems and software Quality Requirements and Evaluation (SQuaRE): Quality model for AI systems* (ISO/IEC 25059:2023). https://www.iso.org/standard/80655.html

Klimashevskaia, A., Jannach, D., Elahi, M., & Trattner, C. (2024). A survey on popularity bias in recommender systems. *User Modeling and User-Adapted Interaction, 34*, 1777–1834. https://doi.org/10.1007/s11257-024-09406-0

Lorenz-Spreen, P., Mønsted, B. M., Hövel, P., & Lehmann, S. (2019). Accelerating dynamics of collective attention. *Nature Communications, 10*, Article 1759. https://doi.org/10.1038/s41467-019-09311-w [VERIFICAR]

Lundberg, S. M., & Lee, S.-I. (2017). A unified approach to interpreting model predictions. En *Advances in Neural Information Processing Systems 30* (pp. 4765–4774). Curran Associates. [VERIFICAR: páginas]

McInnes, L., Healy, J., & Melville, J. (2018). *UMAP: Uniform manifold approximation and projection for dimension reduction* (arXiv:1802.03426) [Prepublicación]. arXiv. https://doi.org/10.48550/arXiv.1802.03426

Min, S., Krishna, K., Lyu, X., Lewis, M., Yih, W.-t., Koh, P. W., Iyyer, M., Zettlemoyer, L., & Hajishirzi, H. (2023). FActScore: Fine-grained atomic evaluation of factual precision in long form text generation. En H. Bouamor, J. Pino, & K. Bali (Eds.), *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing* (pp. 12076–12100). Association for Computational Linguistics. https://doi.org/10.18653/v1/2023.emnlp-main.741

Nguyen, H., Kamruzzaman, M., Chhabra, A., & Kim, G. L. (2026). *Token-level diagnosis of sycophancy in LLMs with attribution-guided steering* [Prepublicación]. arXiv. https://doi.org/10.48550/arXiv.2607.28906 [VERIFICAR]

Noy, S., & Zhang, W. (2023). Experimental evidence on the productivity effects of generative artificial intelligence. *Science, 381*(6654), 187–192. https://doi.org/10.1126/science.adh2586

Otis, N. G., Clarke, R., Delecourt, S., Holtz, D., & Koning, R. (2026). *The uneven impact of generative AI on entrepreneurial performance: Evidence from a field experiment in Kenya* (Working Paper 24-042). Harvard Business School. https://www.hbs.edu/ris/download.aspx?name=24-042.pdf

Qwen. (s. f.). *Qwen3-Embedding-0.6B* [Modelo de embeddings]. Hugging Face. https://huggingface.co/Qwen/Qwen3-Embedding-0.6B

Ribeiro, M. T., Singh, S., & Guestrin, C. (2016). "Why should I trust you?": Explaining the predictions of any classifier. En *Proceedings of the 22nd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining* (pp. 1135–1144). Association for Computing Machinery. https://doi.org/10.1145/2939672.2939778

Rousseeuw, P. J. (1987). Silhouettes: A graphical aid to the interpretation and validation of cluster analysis. *Journal of Computational and Applied Mathematics, 20*, 53–65. https://doi.org/10.1016/0377-0427(87)90125-7

Shapley, L. S. (1953). A value for n-person games. En H. W. Kuhn & A. W. Tucker (Eds.), *Contributions to the theory of games* (Vol. 2, pp. 307–317). Princeton University Press.

Tabassi, E. (2023). *Artificial Intelligence Risk Management Framework (AI RMF 1.0)* (NIST AI 100-1). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.AI.100-1

X Corp. (s. f.). *Developer agreement and policy*. https://docs.x.com/developer-terms/agreement-and-policy

Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2023). ReAct: Synergizing reasoning and acting in language models. En *The Eleventh International Conference on Learning Representations*. https://openreview.net/forum?id=WE_vluYUL-X

Zhang, Z., Fang, M., Chen, L., & Namazi-Rad, M.-R. (2022). Is neural topic modelling better than clustering? An empirical study on clustering with contextual embeddings for topics. En *Proceedings of the 2022 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies* (pp. 3886–3893). Association for Computational Linguistics. https://doi.org/10.18653/v1/2022.naacl-main.285

Zhou, X., Zhao, Y., Jiang, O., Hu, T., Xu, C., Patwardhan, M., & Cohan, A. (2026). *BackTrend: Evaluating scientific weak-signal prediction via backward reconstruction* [Prepublicación]. arXiv. https://doi.org/10.48550/arXiv.2609.24921

# Anexos

**Anexos previstos.** Disponibles: carta de auspicio de Bistec LLC del 2 de agosto de 2026; rúbrica de utilidad con anclas de 1 a 5; registro de decisiones; evidencias de las Tareas 5, 6 y 7, con revisión pendiente de lo compartible; copia pública saneada del prototipo. Pendientes: diagrama BPMN y registro de carga; protocolos y resultados del ensayo con revisores y de la prueba retrospectiva; auditoría de fuentes y pruebas de robustez; política de conservación y borrado; matrices de riesgos y de observaciones del Comité; tabla del piloto; demo de tres minutos; acceso de lectura al repositorio de Earlywindow. Ningún anexo incluirá credenciales, textos crudos de X, sesiones ni opiniones de revisores.

**Tabla 14.** Estado del borrador: qué falta en cada sección. Todas están en estado preliminar, con brechas declaradas.

| Sección | Qué falta |
|---|---|
| Resumen y Abstract | Actualizar con la evaluación final; revisión humana de la traducción |
| 1 Introducción | Registro de carga; diagrama en BPMN; misión y visión; captura de suscriptores |
| 2 Análisis de soluciones | Tabla complementaria de la guía del tutor; medir efectos y consumo |
| 3 Objetivos y 4 Alcance | Registrar las modificaciones de corpus y diseño tras el aviso al tutor |
| 5 Planificación y costos | Gantt gráfico; tarifa del servicio conversacional; fechas de Brightspace |
| 6 Estudios realizados | Literatura sobre detección de tendencias y sesgos |
| 7.1 Diseño y 7.2 Desarrollo | Diagrama formal; fórmula de Earlywindow; Earlywindow construido; comparación de embeddings o desviación registrada |
| 7.3 Resultados y Discusión | Ensayo con revisores, registro de carga, piloto, robustez |
| 7.4 Implicaciones éticas | Política de conservación y borrado |
| 8 Conclusiones y 9 Trabajo futuro | Tabla de metas final; fechas y versión de evaluación |
| 10 Referencias y 11 Anexos | Resolver los [VERIFICAR]; producir los anexos pendientes |
