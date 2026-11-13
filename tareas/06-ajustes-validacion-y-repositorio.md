# Ajustes y validación del prototipo

Miguel Ángel Brito Espejo · Grupo 5 · Maestría en Inteligencia Artificial
Bistec LLC · SingulariDev · Tarea 6
6 de octubre de 2026 · Resultados exploratorios

## 1. Ajustes y diseño de evaluación

El prototipo ayuda a priorizar ideas de videos en inglés para emprendedores de SingulariDev. El operador conversa con un asistente, revisa publicaciones de X, obtiene una ficha y conserva la decisión final. La Tarea 5 mostró una separación temática débil y grupos pequeños. Esta iteración compara una reducción de diez a cinco grupos en K-means y una alternativa BERTopic. También incorpora un ensayo cronometrado de elaboración manual y asistida.

Se reutilizaron los mismos 100 registros de X, 99 tras eliminar un duplicado, publicados en una ventana de 28 minutos y 37 segundos. La división temporal conserva 59 textos de ajuste, 20 de validación y 20 de prueba final. Los 79 textos de desarrollo reutilizan las representaciones numéricas de Qwen3-Embedding-0.6B, de 1.024 dimensiones. El modelo Qwen no se reentrena. UMAP se ajusta solo con los primeros 59 textos y transforma después los demás en cinco dimensiones. Las tres alternativas reciben exactamente la misma proyección dentro de cada ejecución.

| Alternativa | Ajuste aplicado | Motivo y resultado buscado |
|---|---|---|
| K-means, 10 grupos | Referencia de la Tarea 5; configuración conservada | Reproducir el punto de partida para comparar |
| K-means, 5 grupos | Reducir únicamente el número de grupos | Disminuir la fragmentación y mejorar la asignación de textos posteriores |
| BERTopic | HDBSCAN con grupo mínimo de 10 textos y min_samples de 5; c-TF-IDF describe los temas | Evaluar grupos de tamaño variable y exclusión de textos sin un grupo claro |

El protocolo se escribió antes de ejecutar las alternativas. Se repitieron las semillas 42 a 46, que cambian la inicialización de UMAP y K-means. La selección exigió cobertura de al menos 80 % en cada ejecución, silueta válida en las cinco, mejora media respecto de la referencia y una caída de estabilidad no mayor de 0,05. Son reglas prácticas, no umbrales de significación estadística. Se comparó también la silueta sobre los textos asignados por ambas alternativas para evitar premiar una mejora obtenida excluyendo casos difíciles.

La división temporal representa el uso previsto de asignar publicaciones posteriores a grupos ya aprendidos. Se evitó una validación cruzada aleatoria que mezclara pasado y futuro. La selección de K-means con cinco grupos quedó guardada a las 22:09:48 de Ecuador, antes de representar y evaluar los veinte textos finales. Se mantuvo la semilla operativa 42. No se cambiaron parámetros después de abrir la prueba. Esa partición ya está consumida y no podrá presentarse como una nueva prueba independiente.

## 2. Métricas empleadas

La silueta coseno mide separación entre grupos sobre las representaciones originales. Su rango va de -1 a 1; los valores próximos a cero indican poca separación. La cobertura es el porcentaje de textos asignados. El índice ARI mide acuerdo entre agrupaciones, con 1 como acuerdo perfecto, no coincidencia con categorías humanas. Se informa su media entre las diez parejas de semillas. No existen etiquetas de referencia para calcular accuracy ni una medida humana de claridad temática.

<!-- pagebreak -->

## 3. Resultados, variabilidad y decisión

Las cifras de silueta son media ± desviación estándar entre cinco ejecuciones. La referencia reproduce exactamente las cinco siluetas de la Tarea 5 y las asignaciones de su semilla 42. Así se comprueba que la diferencia no procede de cambiar los datos o el método de medición.

| Métrica | K-means 10 | K-means 5 | BERTopic |
|---|---|---|---|
| Silueta en ajuste | 0,1257 ± 0,0198 | 0,0904 ± 0,0023 | 0,1129 ± 0,0248* |
| Silueta en validación | -0,0182 ± 0,0243 | -0,0165 ± 0,0229 | No definida |
| Silueta en prueba final | -0,0104 ± 0,0291 | 0,0349 ± 0,0101 | No definida |
| Cobertura, validación / prueba | 100 % / 100 % | 100 % / 100 % | 0 % / 2 %** |
| ARI, validación / prueba | 0,9028 / 0,8859 | 0,8848 / 0,8554 | No interpretable |
| Mediana de ajuste y validación, sin UMAP | 6,00 ms | 3,97 ms | 10,78 ms |

* BERTopic tiene cuatro siluetas de ajuste válidas de cinco ejecuciones, sobre conjuntos asignados distintos. Su cobertura de ajuste varió de 0 % a 91,53 %. Esta media no implica mejor calidad sobre los mismos textos. ** En prueba final asignó cero o un texto de veinte por ejecución; el 2 % es la media de cinco ejecuciones. Sin al menos dos grupos evaluables, no se calcula silueta.

K-means con cinco grupos cumple la regla, pero la mejora media de validación es solo 0,0017 y sigue siendo negativa. Dos semillas lo favorecen y tres favorecen la referencia. La desviación de esas diferencias es 0,0432. Los grupos de un solo texto en validación bajan de 4,4 a 2,6 en promedio. Se integra como ajuste provisional por menor fragmentación y facilidad de despliegue, sin afirmar superioridad robusta. En prueba final su silueta fue positiva en las cinco ejecuciones, con rango de 0,0169 a 0,0394, frente a -0,0585 a 0,0133 de la referencia. Los valores absolutos siguen siendo bajos.

La estabilidad tampoco mejora de forma uniforme. En prueba final el ARI medio baja de 0,8859 a 0,8554 y el rango del ajuste es de 0,6385 a 1,0000. Una ejecución produce asignaciones distintas. Las cinco semillas reutilizan el mismo lote y las diez parejas ARI son dependientes. Sus desviaciones y rangos describen sensibilidad del algoritmo, no intervalos de confianza sobre publicaciones futuras. No se calculan pruebas de significación ni se presenta este lote como evidencia poblacional.

BERTopic no supera el mínimo de cobertura. En la semilla 42, HDBSCAN directo también dejó los veinte textos de validación como ruido, sin pasar por BERTopic. El resultado se limita a esta configuración y muestra; no demuestra que BERTopic sea inadecuado en general. Se descarta su integración en esta iteración y se conserva como alternativa para un corpus posterior más amplio.

Los tiempos son orientativos. El orden de ejecución fue fijo y BERTopic incluye la descripción de temas en su cronómetro. UMAP requirió una mediana de 0,0862 segundos, con 6,2343 segundos en la primera ejecución por calentamiento. Los veinte embeddings finales tardaron 7,05 segundos, incluida la carga del modelo. Estas diferencias de milisegundos no justifican afirmar un ahorro del trabajo editorial. No hubo nuevas consultas a X ni inferencia pagada de embeddings. El costo del servicio conversacional proporcionado por el autor no está verificado.

## 4. Prototipo ajustado

La interfaz usa los 79 textos de desarrollo con la configuración seleccionada. Pi 1.0.0 conecta con el servicio compatible con OpenAI del autor, mediante GPT-6.1 Sol y razonamiento high. Se conservaron las cuatro herramientas editoriales, la revisión humana y el registro de decisiones. Cada ejercicio dispone solo de su paquete de fuentes y una conversación nueva para evitar arrastrar información del anterior. Diez controles locales de regresión y ocho de integración pasaron. Una ficha sintética de 147 palabras, con dos fuentes y citas literales comprobadas, se generó en 38,992 segundos. Es una prueba funcional, no una opinión del operador.

<!-- pagebreak -->

## 5. Ensayo de uso

Miguel realizó cuatro fichas en dos bloques temáticos, con orden manual, asistida, asistida y manual. Cada ejercicio usó cuatro fuentes distintas, equilibradas antes de observar resultados: 134/135 palabras en permisos y 153/161 en programación. El límite fue de cinco minutos. El cronómetro incluye lectura, espera, edición y revisión, sin descontar pausas. En ambas asistidas el operador pidió un borrador y un cambio de enfoque.

| Ejercicio y método | Tiempo observado | Estado declarado | Utilidad, 1 a 5 |
|---|---|---|---|
| 1. Manual, permisos | 296,034 s | Completa | 2 |
| 2. Asistido, permisos | 170,119 s | Completa | 4 |
| 3. Asistido, programación | 130,293 s | Completa | 5 |
| 4. Manual, programación | 300 s, límite | Incompleta | 3 |

Se terminaron dos de dos asistidas y una de dos manuales. La mediana asistida fue 150,206 segundos; la tarea manual incompleta tiene tiempo censurado y no se imputa como terminada. No se calcula un porcentaje de ahorro. La utilidad media autovalorada fue 4,5/5 frente a 2,5/5. El autor no pidió más cambios al valorar las asistidas; en las manuales cuestionó el enfoque y la falta de evidencia. La primera manual recibió respaldo percibido afirmativo, aunque su única fuente no sustenta todas sus afirmaciones. Percepción no equivale a auditoría factual.

Las fichas manuales tuvieron 97 y 77 palabras, las asistidas 160 y 168, contando por espacios. Solo estas últimas cumplieron la extensión sugerida de 120 a 180. La finalización fue autodeclarada. Un operador, dos tareas por método, fuentes preseleccionadas, orden fijo y productos de distinta extensión limitan la comparación. Es una señal favorable al apoyo editorial, no prueba del ahorro objetivo del 40 % ni validación externa de utilidad o del 90 % de respaldo factual.

## 6. Riesgos y próximos pasos

| Prioridad | Riesgo o hallazgo | Mitigación y evidencia siguiente |
|---|---|---|
| Inmediata | Mejora pequeña y sensible a la semilla | Mantener selección provisional. Repetir con otro corte temporal y exigir cobertura ≥80 %, silueta positiva y estabilidad consistente |
| Inmediata | Muestra estrecha, noticias repetidas y autores compartidos | Registrar dependencias. Ampliar días y fuentes cuando exista presupuesto y separar duplicados y autores relacionados antes de comparar |
| Siguiente | BERTopic rechaza publicaciones posteriores | Revisar densidad y proyección solo en nuevos datos de desarrollo. Congelar parámetros antes de una nueva prueba |
| Siguiente | Una ficha incompleta y calidad autovalorada | Ampliar a seis fichas por condición y dos revisores externos. Exigir ahorro ≥40 %, utilidad ≥4/5 y respaldo factual ≥90 %, con extensión comparable |
| Permanente | Citas válidas pueden sostener afirmaciones incorrectas | Mantener atribución, límites de herramientas y revisión humana. Las credenciales y publicaciones quedan fuera de Git |

## 7. Repositorio y síntesis reflexiva

El respaldo público está en [github.com/miwgel/singularidev-editorial-prototype](https://github.com/miwgel/singularidev-editorial-prototype), versión 3dff908. Incluye código, README, protocolo y resultados agregados; excluye credenciales, publicaciones y sesiones privadas. El historial original queda local: c4dda35 conserva la referencia y 5bb006f el ajuste evaluado. Las huellas corresponden a esa versión original. La copia pública retira referencias personales y hace configurable el proveedor. No se alteraron métricas. La evidencia humana se distingue de las pruebas automáticas.

La decisión más relevante fue aceptar un ajuste pequeño con límites explícitos y rechazar una alternativa que no logró cobertura. La prioridad siguiente es comprobar utilidad editorial con más evidencia, no optimizar una puntuación del mismo lote hasta obtener un resultado favorable.

Referencias técnicas: [BERTopic, agrupamiento](https://maartengr.github.io/BERTopic/getting_started/clustering/clustering.html); [HDBSCAN, predicción de nuevos puntos](https://hdbscan.readthedocs.io/en/latest/prediction_tutorial.html). Evidencia primaria: archivos de resultados y bitácora del repositorio, 6 de octubre de 2026.
