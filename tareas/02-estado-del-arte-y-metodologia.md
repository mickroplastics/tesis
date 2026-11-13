::: {.sintesis .inicio}
# Estado del arte y metodología

Miguel Ángel Brito Espejo · Proyecto MIA · Group 5  
Auspiciante: Bistec LLC · Unidad de aplicación: SingulariDev

**Título aprobado:** Arnés agéntico basado en modelos de lenguaje y análisis semántico de tendencias para priorizar ideas de contenido en YouTube orientadas a la adquisición de miembros para SingulariDev.

## 1. Síntesis crítica del estado del arte

### Agrupar señales para apoyar la decisión editorial

SingulariDev se dirige a emprendedores unipersonales interesados en agentes, automatización y productos con IA. Investigar ideas de videos en inglés exige revisar fuentes, comparar temas y preparar fichas de contenido. El fundador estima que este trabajo supera 20 horas semanales, cifra pendiente de medición. Además del tiempo, el problema es la falta de un registro completo que conecte fuentes, criterios y decisiones.

Una tendencia de la literatura es representar los textos mediante vectores, es decir, conjuntos de números que permiten comparar su significado. Grootendorst (2022) propone BERTopic para agrupar documentos y extraer palabras que describan cada tema. El método separa el agrupamiento de la descripción de los grupos. Esto permite revisar qué documentos sostienen un tema, en lugar de aceptar una etiqueta sin evidencia.

Egger y Yu (2022) comparan LDA, NMF, Top2Vec y BERTopic sobre 31.800 publicaciones de Twitter acerca de viajes y COVID-19. Su análisis favorece BERTopic y NMF para distinguir temas, pero recomienda interpretar los documentos originales. La cercanía con textos breves de redes sociales hace pertinente este antecedente. Sin embargo, sus resultados no prueban que BERTopic funcione igual con conversaciones sobre productos de IA, otro dominio y otra población.

Zhang et al. (2022) muestran que K-means también puede generar temas coherentes y diversos cuando utiliza buenas representaciones de los textos. En sus pruebas con tres conjuntos de textos, la selección de palabras representativas influye en el resultado. Por tanto, una técnica más compleja no debe considerarse mejor de antemano. Para SingulariDev se compararán BERTopic y K-means sobre los mismos textos y vectores, evitando confundir el efecto del agrupamiento con diferencias en los datos.

Ambos métodos tienen límites. BERTopic puede dejar documentos sin grupo; K-means asigna todos, aunque algunos no encajen bien. Se revisarán tanto ejemplos agrupados como descartados. La elección combinará claridad de los temas, estabilidad entre ejecuciones y cobertura de documentos, sin depender de una sola puntuación automática.

### Usar herramientas sin delegar toda la decisión

Otra tendencia es conectar los modelos de lenguaje, también llamados LLM, con herramientas de consulta. ReAct alterna acciones y observaciones para resolver preguntas y tareas interactivas. Yao et al. (2023) muestran beneficios frente a estrategias que usan solo acciones, aunque el resultado depende de la tarea y de la información recuperada. El acceso a herramientas no elimina los errores.

El proyecto aplicará esta idea mediante módulos separados para consultar fuentes, agrupar, puntuar y redactar. El modelo preparará la ficha; las reglas registradas determinarán su puntuación y Miguel decidirá si la acepta, edita o rechaza. Esta separación responde a la falta de trazabilidad del proceso actual. Sigue siendo una propuesta por evaluar, no una demostración de superioridad frente al trabajo manual.
:::

::: {.sintesis}
### Medir productividad, utilidad y respaldo por separado

Noy y Zhang (2023) estudiaron tareas de escritura con 453 profesionales. El uso de ChatGPT redujo el tiempo promedio en 40 % y elevó la calidad evaluada en 18 %. El resultado justifica medir ahorro de tiempo junto con calidad, pero no permite anticipar el mismo efecto en SingulariDev. Preparar una ficha incluye investigación y selección, además de escritura. La meta local de reducir 40 % el tiempo mediano deberá comprobarse con tareas propias; promedio y mediana tampoco son medidas equivalentes.

Csaszar et al. (2024) muestran que los modelos pueden generar y evaluar estrategias a un nivel comparable al de participantes de contextos empresariales específicos. Este antecedente respalda estudiar la IA como apoyo a decisiones. No demuestra que una recomendación produzca mejores ventas. En el proyecto, la calidad de una idea y los resultados del video serán medidas distintas, porque también intervienen producción, distribución y oferta.

Feng et al. (2026) comparan explicaciones genéricas y contextualizadas de recomendaciones de películas. Su experimento incluye 759 participantes y entrevistas con 30 personas. Reportan beneficios de contextualizar las explicaciones para las percepciones del usuario y su intención de consumo. Para SingulariDev, esto sugiere explicar por qué una idea responde a su audiencia. Sin embargo, una explicación convincente no demuestra exactitud ni garantiza utilidad editorial. La rúbrica evaluará relevancia, respaldo, diferenciación, factibilidad y claridad.

Gao et al. (2023) distinguen fluidez, corrección y calidad de las citas mediante ALCE. Sus resultados muestran que una respuesta legible puede carecer de respaldo completo. Por eso no bastará con incluir enlaces al final de cada ficha: la fuente deberá sostener la afirmación concreta. Min et al. (2023) ofrecen un procedimiento pertinente con FActScore, que divide un texto en afirmaciones pequeñas y verifica su respaldo. Sus pruebas se concentran en biografías y Wikipedia. El proyecto adaptará ese principio a tendencias tecnológicas, con revisión humana, sin asumir que un evaluador automático tendrá el mismo desempeño.

### Sesgos y vacío de aplicación

Klimashevskaia et al. (2024) advierten que los recomendadores pueden favorecer contenidos ya populares y reforzar su exposición. Su revisión también encuentra predominio de evaluaciones computacionales y poca evidencia con usuarios. Promover temas minoritarios no garantiza mayor utilidad. SingulariDev necesita distinguir popularidad, crecimiento y afinidad con su audiencia, en lugar de copiar siempre lo más visto o descartar todo tema conocido.

Se revisará si las primeras posiciones dependen de pocas cuentas y si pequeños cambios en los pesos alteran la selección. También se considerará el cambio de audiencia: el canal histórico es principalmente hispanohablante, mientras la comunidad se dirige a personas angloparlantes. Sus métricas previas no representan automáticamente al público objetivo.

Ninguno de los diez estudios seleccionados valida el proceso completo del proyecto: reunir señales de YouTube y X, convertirlas en fichas en inglés y medir el esfuerzo de un único operador. El aporte será integrar técnicas existentes y evaluar su uso conjunto, no crear un algoritmo nuevo. La prueba comparará tareas manuales y asistidas, con revisores externos. Los tres videos del piloto servirán para registrar resultados exploratorios, sin atribuir al sistema la adquisición de miembros o los pagos observados.
:::

::: {.metodologia}
## 2. Propuesta metodológica preliminar

Se desarrollará un prototipo con módulos separados y una interfaz de revisión. Pi coordinará el modelo y las herramientas. Miguel operará el proceso manual y el asistido; no se entrenará un modelo de lenguaje ni se automatizará la publicación.

**Datos y preparación.** YouTube Data API y X API aportarán textos, identificadores, marcas temporales y métricas públicas en formato JSON. Antes de recolectar se verificarán permisos, cuotas, costos y restricciones de conservación. Se eliminarán duplicados, identificarán idiomas y marcarán campos ausentes, conservando la procedencia. El volumen real dependerá de estas pruebas. Google Trends será respaldo temporal si X no resulta viable.

**Técnicas.** Se compararán BERTopic y K-means con los mismos textos y vectores, según Grootendorst (2022), Egger y Yu (2022) y Zhang et al. (2022). Se revisará si los temas son claros, cuántos textos quedan agrupados y cuánto cambian los resultados entre cinco ejecuciones. Después se puntuarán actualidad, crecimiento, afinidad, novedad y factibilidad. Se cambiará cada peso en 10 % y 20 %, hacia arriba y abajo, ajustando el total al 100 %, para comprobar si cambia el orden. El crecimiento requerirá mediciones comparables. El modelo redactará fichas con fuentes mediante herramientas limitadas, siguiendo el principio de ReAct.

**Evaluación.** Se registrará el trabajo cotidiano durante dos semanas. La prueba controlada usará doce temas en seis pares comparables, asignando al azar uno de cada par al proceso manual y otro al asistido. El tiempo activo incluirá búsqueda, elaboración y decisión, sin interrupciones. Dos revisores externos acordarán cómo usar la rúbrica y evaluarán las doce fichas sin conocer su origen. La valoración de Miguel se reportará aparte.

| Métrica | Medición y criterio de éxito |
|---|---|
| Tiempo, principal | Reducción = 100 × (mediana manual − mediana asistida) / mediana manual. Meta ≥40 %. |
| Respaldo factual | Afirmaciones verificables respaldadas / total verificable × 100. Meta ≥90 %. Se contrastará el contenido, no solo el enlace, según Gao et al. (2023) y Min et al. (2023). |
| Utilidad | Media de los revisores externos para las seis fichas asistidas ≥4/5. Escala: 1, no utilizable; 2, cambios mayores; 3, revisión sustancial; 4, cambios menores; 5, lista para decidir. |
| Interpretabilidad y riesgo | Mostrar fuentes y factores del puntaje; registrar concentración de cuentas y fallos de acceso. Una afirmación central falsa exige corrección aunque se cumpla el 90 %. |

**Ética y viabilidad.** Se minimizarán datos personales y no se inferirán atributos sensibles. Los textos recuperados se tratarán como datos, no como instrucciones para el agente. Se registrarán configuración, costo y decisión humana, con un límite previsto de 30 USD mensuales para inferencia, separado de X. Tras corregir fallos se publicarán tres videos con una ventana común de siete días. Clics, registros y pagos serán descriptivos; la muestra pequeña y el único operador limitan la generalización.

### Registro breve de búsqueda

Se realizó una búsqueda bibliográfica en la web y se verificaron publicaciones en ACL Anthology, Frontiers, Springer y arXiv. Los datos bibliográficos y resúmenes editoriales se contrastaron con Crossref. Se priorizaron artículos y congresos de 2021–2026 con relación directa al método; se admitió la prepublicación original de BERTopic. Se excluyeron blogs y duplicados. Se ejecutaron, entre otras, estas cadenas con ocho resultados solicitados por consulta:

- `("topic modeling" OR "topic modelling") AND (BERTopic OR "K-means" OR "contextual embeddings") AND (Twitter OR "social media" OR evaluation) after:2020 before:2027`
- `("language agents" OR "ReAct") AND (tools OR architecture OR evaluation) after:2020 before:2027`
- `("language models" OR "topic models") AND ("citation quality" OR "factual precision" OR "human evaluation" OR coherence) after:2020 before:2027`

Se completó la selección mediante búsquedas por título y autor. Los filtros de publicación se comprobaron manualmente. No hubo consulta directa a Scopus o IEEE. Para Noy, Csaszar y Feng se usaron resúmenes editoriales; para los otros siete, secciones del texto académico. La revisión es inicial y no exhaustiva.
:::

::: {.matriz}
## 3. Matriz de literatura y referencias APA 7

| Cita en APA 7 | Objetivo | Método o técnica de IA | Hallazgos relevantes | Vacíos o limitaciones | Relación con SingulariDev |
|---|---|---|---|---|---|
| Grootendorst, M. (2022). *BERTopic: Neural topic modeling with a class-based TF-IDF procedure* [Prepublicación]. arXiv. https://doi.org/10.48550/arXiv.2203.05794 | Identificar temas y palabras representativas en documentos. | Vectores de texto, UMAP, HDBSCAN y c-TF-IDF; noticias y publicaciones sociales. | Coherencia y diversidad competitivas; separación entre agrupamiento y descripción de temas. | Un tema por documento y posibles palabras redundantes. Es una prepublicación. | Probar BERTopic conservando ejemplos y documentos sin grupo para revisión. |
| Egger, R., & Yu, J. (2022). A topic modeling comparison between LDA, NMF, Top2Vec, and BERTopic to demystify Twitter posts. *Frontiers in Sociology, 7*, Article 886498. https://doi.org/10.3389/fsoc.2022.886498 | Comparar métodos para interpretar textos breves de redes sociales. | LDA, NMF, Top2Vec y BERTopic; 31.800 publicaciones sobre viajes y COVID-19. | BERTopic y NMF distinguen temas; la interpretación requiere revisar documentos originales. | Corpus de un dominio y contexto específicos. Requiere interpretación cualitativa. | Sustenta analizar X, pero exige validar el método en contenidos sobre IA. |
| Zhang, Z., Fang, M., Chen, L., & Namazi-Rad, M.-R. (2022). Is neural topic modelling better than clustering? An empirical study on clustering with contextual embeddings for topics. En *Proceedings of the 2022 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies* (pp. 3886–3893). Association for Computational Linguistics. https://doi.org/10.18653/v1/2022.naacl-main.285 | Contrastar agrupamiento sencillo con modelos temáticos neuronales. | CETopic: vectores contextuales, UMAP, K-means y ponderación de palabras; tres corpus. | Agrupamiento coherente y diverso; representación y selección de palabras influyen en los resultados. | Evalúa conjuntos de prueba, no utilidad editorial.* | Justifica comparar K-means con BERTopic usando los mismos textos y vectores. |
| Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2023). ReAct: Synergizing reasoning and acting in language models. En *The Eleventh International Conference on Learning Representations*. https://openreview.net/forum?id=WE_vluYUL-X | Integrar acciones y observaciones para resolver tareas. | LLM con herramientas; HotpotQA, FEVER, ALFWorld y WebShop. | Mejora frente a estrategias de solo acciones; no domina todas las comparaciones. | Persisten errores de búsqueda y razonamiento. | Limitar herramientas y registrar evidencia; conservar la decisión humana. |
| Gao, T., Yen, H., Yu, J., & Chen, D. (2023). Enabling large language models to generate text with citations. En H. Bouamor, J. Pino, & K. Bali (Eds.), *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing* (pp. 6465–6488). Association for Computational Linguistics. https://doi.org/10.18653/v1/2023.emnlp-main.398 | Evaluar respuestas generadas con citas. | ALCE: recuperación y generación; evalúa fluidez, corrección y citas en tres conjuntos de preguntas. | Una respuesta fluida puede carecer de respaldo completo. | Pruebas de preguntas y respuestas, no de fichas editoriales.* | Comprobar que cada fuente sostenga la afirmación que acompaña. |
:::

::: {.matriz}
## Matriz de literatura, continuación

| Cita en APA 7 | Objetivo | Método o técnica de IA | Hallazgos relevantes | Vacíos o limitaciones | Relación con SingulariDev |
|---|---|---|---|---|---|
| Min, S., Krishna, K., Lyu, X., Lewis, M., Yih, W.-t., Koh, P. W., Iyyer, M., Zettlemoyer, L., & Hajishirzi, H. (2023). FActScore: Fine-grained atomic evaluation of factual precision in long form text generation. En H. Bouamor, J. Pino, & K. Bali (Eds.), *Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing* (pp. 12076–12100). Association for Computational Linguistics. https://doi.org/10.18653/v1/2023.emnlp-main.741 | Medir respaldo factual en textos generados. | Afirmaciones simples y verificación humana o con búsqueda y un modelo de lenguaje. | La evaluación por afirmación distingue errores ocultos en un juicio global. | Pruebas centradas en biografías y Wikipedia; dificultades con hechos debatibles. | Adaptar la revisión factual con dos revisores; no depender solo de un juez automático. |
| Noy, S., & Zhang, W. (2023). Experimental evidence on the productivity effects of generative artificial intelligence. *Science, 381*(6654), 187–192. https://doi.org/10.1126/science.adh2586 | Estimar efectos de ChatGPT sobre tiempo y calidad. | Experimento aleatorio con 453 profesionales en tareas de escritura. | El resumen reporta 40 % menos tiempo promedio y 18 % más calidad. | No estudia el flujo editorial completo; lectura limitada al resumen.* | Medir tiempo junto con calidad, sin trasladar sus efectos como predicción local. |
| Csaszar, F. A., Ketkar, H., & Kim, H. (2024). Artificial intelligence and strategic decision-making: Evidence from entrepreneurs and investors. *Strategy Science, 9*(4), 322–345. https://doi.org/10.1287/stsc.2024.0190 | Analizar IA en decisiones estratégicas empresariales. | LLM para generar y evaluar estrategias; evidencia de aceleradora y competencia de emprendimientos. | Capacidades comparables a participantes en las tareas empresariales estudiadas. | No demuestra adquisición de miembros; lectura limitada al resumen.* | Registrar recomendaciones aceptadas y separar calidad de ficha de ventas. |
| Feng, Y., Feuerriegel, S., & Shrestha, Y. R. (2026). Contextualizing recommendation explanations with LLMs: A user study. *Proceedings of the International AAAI Conference on Web and Social Media, 20*(1), 788–803. https://doi.org/10.1609/icwsm.v20i1.42667 | Evaluar explicaciones contextualizadas de recomendaciones. | LLM para explicar películas; experimento con 759 participantes y 30 entrevistas. | Mejoras en percepciones e intención de consumo; demasiado detalle puede ser redundante. | Intención no equivale a consumo efectivo ni utilidad editorial. Se usó el resumen final.* | Explicar afinidad con la audiencia y evaluar utilidad mediante rúbrica. |
| Klimashevskaia, A., Jannach, D., Elahi, M., & Trattner, C. (2024). A survey on popularity bias in recommender systems. *User Modeling and User-Adapted Interaction, 34*, 1777–1834. https://doi.org/10.1007/s11257-024-09406-0 | Revisar causas y mitigación del sesgo de popularidad. | Revisión de algoritmos de recomendación, métricas y técnicas de mitigación. | La exposición puede concentrarse y reforzarse. Predominan evaluaciones computacionales. | Escasa evidencia con usuarios; mejorar exposición no garantiza utilidad. | Revisar concentración de cuentas y sensibilidad de pesos, sin favorecer automáticamente lo minoritario. |

\* Las limitaciones marcadas indican diferencias con este proyecto o límites de acceso detectados en la revisión, no conclusiones atribuidas a los autores. Las diez referencias corresponden a estudios distintos; la prepublicación de Feng no se cuenta aparte.
:::
