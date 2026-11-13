::: {.pagina .inicio}
# S4. Documento técnico

Miguel Ángel Brito Espejo · Proyecto MIA · Group 5  
Auspiciante: Bistec LLC · Unidad de aplicación: SingulariDev

**Título aprobado:** Arnés agéntico basado en modelos de lenguaje y análisis semántico de tendencias para priorizar ideas de contenido en YouTube orientadas a la adquisición de miembros para SingulariDev.

## 1. Pipeline de datos y solución

El prototipo apoyará la investigación y selección de ideas para videos en inglés. Reunirá publicaciones relacionadas, formará grupos temáticos y preparará fichas con evidencia para la decisión humana. Este documento define el diseño y las pruebas iniciales; no presenta resultados experimentales. La primera validación se concentrará en el agrupamiento, antes de evaluar las fichas completas.

### Origen, formato y condiciones de acceso

| Fuente | Unidad de análisis y texto | Volumen inicial previsto |
|---|---|---|
| X, principal | Una publicación pública en inglés. | 500 publicaciones brutas por corte. |
| Reddit, candidata | Título y cuerpo de una publicación en inglés, sin comentarios. | 500 publicaciones brutas por corte, sujeto a autorización. |
| YouTube, respaldo de Reddit | Título y descripción de un video, sin transcripción ni resumen audiovisual. | Sustituye el cupo previsto de Reddit. |

La meta de 1.000 registros por corte es provisional, no observada. Se registrarán consultas, comunidades seleccionadas, ventana de publicación, cuotas y número real de registros. Como punto de partida se propone una ventana común de siete días. Las respuestas autorizadas se conservarán en JSONL, un registro por línea, y los datos preparados en una tabla CSV.

El acceso a Reddit y su uso con IA requieren autorización compatible con el proyecto y su vinculación empresarial. El navegador automatizado no sustituye ese permiso. Si Reddit no resulta viable, se activará YouTube, también sujeto a sus condiciones. Solo se enviará a OpenAI contenido cuyo tratamiento externo esté permitido. No se publicarán textos restringidos ni credenciales; las solicitudes de borrado alcanzarán los datos y derivados afectados (Reddit, s. f.-a, s. f.-b).

### Preparación y selección de variables

Se validarán identificador, fuente, URL, fechas de publicación y captura en UTC, y texto. Se descartarán registros sin texto o fecha válida, duplicados por identificador o texto normalizado y publicaciones que no estén en inglés. Los casos de idioma dudoso se revisarán manualmente. Se limpiarán etiquetas HTML y espacios, conservando el significado y el título al comienzo cuando exista.

Cada entrada tendrá como máximo 4.000 caracteres. Los recortes quedarán marcados; no se generarán resúmenes previos. Se verificará además el límite de tokens de ambos modelos y, si fuera necesario, se reducirá la misma entrada para los dos. El texto será la única entrada al agrupamiento. Las métricas públicas, identificadores y fechas se conservarán aparte para trazabilidad y priorización.

### Partición y flujo

Después de limpiar, se ordenarán los registros por fecha de publicación e identificador. El 60 % más antiguo servirá para **entrenamiento**, entendido como ajuste de grupos y transformaciones; el siguiente 20 %, para **validación**; y el resto, para **prueba final**. Se guardarán los identificadores de cada partición y no se mezclarán duplicados entre ellas. Los modelos de lenguaje preentrenados no se volverán a entrenar.

::: {.flujo}
Fuentes autorizadas → limpieza y partición → representación numérica → agrupamiento y evaluación → priorización → ficha con fuentes → decisión humana
:::

:::

::: {.pagina}
## 2. Baseline y comparación técnica

El **baseline será K-means con 10 grupos y embeddings locales de Qwen3-Embedding-0.6B**. Un embedding es una representación numérica del significado del texto. K-means reúne los textos alrededor de centros similares y permite asignar nuevas publicaciones al centro más cercano. Su sencillez facilita repetir la prueba e interpretar los cambios.

Zhang et al. (2022) muestran que el agrupamiento con representaciones contextuales es una alternativa competitiva a modelos temáticos más complejos. La comparación será BERTopic, que permite formar grupos de distinto tamaño y dejar textos sin asignar (Grootendorst, 2022). No se asumirá que el método más complejo es mejor.

| Componente | Configuración inicial propuesta |
|---|---|
| Representación local | `Qwen/Qwen3-Embedding-0.6B`, 1.024 dimensiones, sin ajuste adicional ni instrucciones añadidas (Qwen, s. f.). |
| Alternativa por API | `text-embedding-3-large`, 3.072 dimensiones. Se guardarán los vectores para no repetir llamadas (OpenAI, s. f.). |
| Transformación común | Normalización L2 y UMAP con 5 dimensiones, 15 vecinos, distancia mínima 0 y métrica coseno. Se ajustará solo con entrenamiento y se aplicará a validación y prueba. |
| K-means | `k=10`, inicialización `k-means++`, `n_init=10` y máximo de 300 iteraciones. |
| BERTopic | HDBSCAN con `min_cluster_size=20`, `min_samples=5`, distancia euclídea y `prediction_data=True` para asignar textos posteriores. |

Dentro de cada modelo de embeddings y semilla, los dos algoritmos usarán exactamente los mismos textos y coordenadas UMAP. Las etiquetas de validación y prueba se obtendrán con los modelos ya ajustados, sin recalcular grupos con esos datos.

**Supuestos y límites.** La cercanía numérica debe reflejar temas útiles para SingulariDev. K-means fuerza la asignación y puede reunir textos poco relacionados; BERTopic puede excluir demasiados. La separación temporal evalúa publicaciones posteriores, pero no demuestra por sí sola que el sistema descubra tendencias nuevas. Esto requerirá repetir el flujo con nuevos lotes, después de la prueba inicial.

## 3. Plan inicial de experimentación

Se cruzarán los dos modelos de embeddings con los dos algoritmos. K-means probará **5, 10 y 15 grupos**; BERTopic, tamaños mínimos de **10, 20 y 30 textos**. Cada configuración se repetirá con las semillas **42, 43, 44, 45 y 46**, compartidas entre métodos. Son 60 ejecuciones de agrupamiento, no 60 llamadas de generación. Los embeddings se calcularán una vez por modelo y lote.

Se mantendrán constantes corpus, partición, limpieza, texto recortado, transformación común y parámetros no incluidos en la comparación. Se registrarán equipo y tiempos por etapa. La semilla 42 será la referencia para revisión humana; las otras medirán estabilidad. Ningún parámetro se elegirá mirando la prueba final.

| Métrica preliminar | Medición |
|---|---|
| Claridad temática | Revisión humana ciega de textos de cada grupo, en escala de 1 a 5. |
| Cobertura | Porcentaje de textos asignados a un grupo; los no asignados se informan aparte. |
| Estabilidad | Acuerdo entre agrupamientos de las cinco semillas mediante ARI, sobre textos asignados en ambos resultados. |
| Separación | Silueta coseno sobre los embeddings originales de los textos agrupados. Se compara dentro de cada modelo de embeddings. |
| Eficiencia | Tiempo de representación y agrupamiento por separado, tokens facturados y costo de API. |

:::

::: {.pagina .cierre}
## 4. Validación, mejoras y reproducibilidad

### Selección y criterios de aceptación

En validación se preseleccionará una configuración por combinación de modelo y algoritmo con cobertura ≥80 % y métricas válidas. Se elegirá la mayor puntuación de estabilidad, cobertura y silueta, con pesos de 25, 20 y 15 puntos. Cobertura y silueta se promediarán entre semillas; estabilidad, entre sus diez pares. Dos revisores externos, sin conocer la variante, evaluarán las cuatro finalistas sobre la ejecución de referencia. Verán hasta cinco textos por grupo elegidos con semilla 42. Los grupos pequeños mostrarán todos sus textos.

La escala de claridad será: **1**, sin tema común; **2**, relación débil; **3**, tema reconocible con varias mezclas; **4**, tema claro con pocas mezclas; **5**, tema claro y consistente. Se promediarán las valoraciones por grupo y por revisor. Esta claridad aportará los 40 puntos restantes. Para puntuar, claridad se dividirá por 5; cobertura, por 100; ARI y silueta se llevarán de su intervalo de −1 a 1 al de 0 a 1. El acuerdo de estabilidad se acompañará del número de textos comparados.

ARI y silueta se reportarán como no calculables si faltan textos o grupos válidos. Solo serán elegibles configuraciones con **cobertura ≥80 % y claridad ≥3,5/5**. La ponderación elegirá el agrupamiento dentro de cada modelo de embeddings. Si faltan métricas válidas o ninguna variante cumple, se revisarán datos o parámetros en desarrollo, sin abrir la prueba final. Los empates se resolverán por menor tiempo.

La opción de OpenAI se justificará si la configuración seleccionada con API mejora la claridad al menos **0,5 puntos** frente a la local, mantiene los umbrales y cabe en el límite previsto de **30 USD mensuales de inferencia**, incluyendo embeddings y fichas. El acceso a fuentes se presupuestará aparte. Tras fijar las configuraciones, se evaluarán una sola vez en el 20 % reservado. La integración opcional dependerá de que la mejora se mantenga; el umbral es práctico, no una prueba de significación estadística.

### Registro reproducible y alcance de los resultados

Cada ejecución conservará, dentro de los permisos aplicables, el lote autorizado, su huella, los identificadores de partición, configuración, semillas, vectores, asignaciones y métricas. Git registrará código y cambios, no credenciales ni contenido restringido. Un archivo de dependencias fijará versiones exactas de Python, PyTorch, Transformers, Sentence Transformers, scikit-learn, UMAP y HDBSCAN/BERTopic; se registrarán también la revisión del modelo local, el identificador de la API y el equipo. **Esas versiones aún deben validarse y fijarse antes del primer ensayo.** El README indicará cómo ejecutar el flujo completo con un lote y una configuración.

Una vez elegida la configuración, el arnés puntuará actualidad, crecimiento, afinidad, novedad y factibilidad con reglas versionadas. El crecimiento necesitará capturas comparables. Un modelo generativo redactará las fichas; Miguel podrá aceptarlas, editarlas o rechazarlas. No habrá publicación autónoma.

La evaluación posterior mantendrá las seis fichas manuales y seis asistidas, con metas de reducción del tiempo mediano ≥40 %, respaldo factual ≥90 % y utilidad externa ≥4/5. Estos resultados no se deducen de la calidad del agrupamiento. Las métricas comerciales de los tres videos seguirán siendo descriptivas.

### Referencias

::: {.referencias}
Grootendorst, M. (2022). *BERTopic: Neural topic modeling with a class-based TF-IDF procedure* [Prepublicación]. arXiv. https://doi.org/10.48550/arXiv.2203.05794

OpenAI. (s. f.). *Vector embeddings*. https://developers.openai.com/api/docs/guides/embeddings

Qwen. (s. f.). *Qwen3-Embedding-0.6B* [Modelo de embeddings]. Hugging Face. https://huggingface.co/Qwen/Qwen3-Embedding-0.6B

Reddit. (s. f.-a). *Data API terms*. https://redditinc.com/policies/data-api-terms

Reddit. (s. f.-b). *User agreement*. https://redditinc.com/policies/user-agreement

Zhang, Z., Fang, M., Chen, L., & Namazi-Rad, M.-R. (2022). Is neural topic modelling better than clustering? An empirical study on clustering with contextual embeddings for topics. En *Proceedings of the 2022 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies* (pp. 3886–3893). Association for Computational Linguistics. https://doi.org/10.18653/v1/2022.naacl-main.285
:::
:::
