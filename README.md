# Predicción temprana de riesgo académico con OULAD

**Proyecto final de Machine Learning — notebook de Google Colab.**

## Resumen

Se compara el uso de características **estáticas (A)** con **estáticas + longitudinales (B)** en las semanas 2, 4, 6 y 8 de módulos del *Open University Learning Analytics Dataset* (OULAD). La unidad de análisis es la matrícula estudiante–módulo–presentación. La etiqueta favorable combina `Pass` y `Distinction`; la adversa combina `Fail` y `Withdrawn`. **Withdrawn significa retiro del módulo, no necesariamente abandono de la universidad.**

| Semana | F1 macro A (test) | F1 macro B (test) | Diferencia B − A |
|---|---:|---:|---:|
| 2 | 0,61375 | 0,68262 | +0,06887 |
| 4 | 0,60939 | 0,68584 | +0,07645 |
| 6 | 0,60307 | 0,70048 | +0,09741 |
| 8 | 0,60156 | 0,71665 | +0,11510 |

**Importante:** los resultados anteriores proceden de una ejecución independiente histórica previamente congelada; no son salidas regeneradas al preparar este repositorio. Los modelos candidatos Random Forest, Transformer y Optuna fueron evaluados como experimentos **de desarrollo**, no como nuevas pruebas independientes.

## Archivo principal

- `WP_Final_Proyecto_ML_GitHub.ipynb`: versión legible para GitHub, con código y metodología y con salidas embebidas eliminadas para facilitar su publicación; las figuras y resultados numéricos están explicados en el texto, y los archivos originales se conservan en el Drive del proyecto.
- `requirements.txt`: dependencias recomendadas; no es un lockfile que garantice reproducción bit a bit.
- `REVISION_FINAL.md`: auditoría de la revisión final, limitaciones y verificación previa a la defensa.
- `.gitignore`: evita incluir datos y artefactos potencialmente voluminosos o sensibles.

## Cómo usarlo en Colab

1. Abra el notebook en Google Colab y cree una copia en su **Google Drive**.
2. La celda 0 monta Drive y utiliza la ruta fija `RUTA_BASE = "/content/drive/MyDrive/Proyecto_ML"`. Ajuste la ruta **solo si su Drive usa otra carpeta**.
3. El cómputo, incluido el entrenamiento y la reducción dimensional, se realiza en `/content`. Los resultados se sincronizan con `Proyecto_ML/artefactos`, `snapshots` y `datos`.
4. El dataset es público. La descarga inicial depende del espejo de OULAD en Kaggle: https://www.kaggle.com/datasets/anlgrbz/student-demographics-online-education-dataoulad. Artículo original: https://doi.org/10.1038/sdata.2017.171. Las sesiones siguientes pueden copiar los CSV de Drive a `/content`.
5. Si su Drive contiene los artefactos del proyecto, restaure snapshots con `recuperar_estado_oulad("experimentos_oulad", "cv_splits_oulad", "pipelines_oulad")` después de ejecutar las celdas 0 y 0.1. Para obtenerlos por primera vez, ejecute las actividades de preparación 0, 2.4, 3.1–3.6 y sus snapshots en orden.
6. **No pulse «Ejecutar todo» indiscriminadamente** en un runtime sin los resultados históricos. Varias etapas exploran muchos modelos y el bloque 3.39 está expresamente diseñado para **reutilizar el test congelado**, no para abrirlo otra vez.

## Alcance de la reproducción

**Reproducción del código y metodología:** el notebook documenta los procedimientos y la fuente de datos. Con el dataset y las dependencias puede reconstruirse la fase de preparación y ejecutar los análisis de desarrollo, con el coste computacional correspondiente.

**Reproducción exacta de resultados congelados:** requiere también los artefactos históricos (por ejemplo, `protocolo_oulad_337.json`, modelos finales y CSV de test 3.39), guardados en el Drive del proyecto y **no incluidos en este repositorio**. Sin ellos, la carga de la evaluación 3.39 informará que faltan archivos; ello no demuestra un error en el método.

**Entorno:** resultados y serializaciones de scikit-learn/joblib pueden depender de versiones. Consigne las versiones de Colab en la ejecución de defensa, junto con las semillas aleatorias. `requirements.txt` indica mínimos de instalación, no el entorno histórico exacto.

## Rúbrica y organización

El notebook contiene motivación del problema, EDA, ingeniería y selección de características, validación agrupada y repetida, optimización mediante GridSearchCV y Optuna, comparación estadística, modelos clásicos y Transformer, métricas, curvas de aprendizaje, prueba independiente congelada, t-SNE y conclusiones. Incluye referencias IEEE y comentarios de asistencia de IA.

## Integridad y límites científicos

- Separación train/test por `id_student` para evitar identidades compartidas.
- Las señales longitudinales se construyen antes de los días 14/28/42/56, según la ventana.
- No interpretar `Withdrawn` como deserción universitaria permanente ni la anticipación retrospectiva como intervención causal.
- La comparación principal confirmatoria es A frente a B por Regresión Logística en el test independiente; las demás comparaciones de algoritmos son complementarias o exploratorias.
- La cohorte común se selecciona retrospectivamente y puede introducir sesgo de supervivencia.
- La proyección t-SNE es exploratoria, no una medida de exactitud predictiva.
- No hay validación externa entre instituciones.

## Privacidad y publicación

No incluya claves de Kaggle, OAuth, tokens de Drive, `studentVle.csv`, snapshots, modelos o archivos con `id_student` u otras claves por matrícula. Aunque OULAD es público, los artefactos derivados deben revisarse antes de compartirlos. Consulte la licencia original de OULAD antes de redistribuir los datos; este repositorio solo señala su fuente.

## Referencias

Las citas [1]–[13] están dentro del notebook al final y en las secciones pertinentes. La fuente original del dataset es Kuzilek, Hlosta y Zdrahal (2017), DOI: 10.1038/sdata.2017.171.

## Uso de IA

Se utilizó ChatGPT para colaborar con la construcción, revisión y explicación del código. Las solicitudes registradas aparecen como comentarios cuando están disponibles; las no preservadas en el historial del código no se presentan como citas textuales inventadas.