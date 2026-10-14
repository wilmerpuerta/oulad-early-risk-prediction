# Auditoría final del notebook OULAD

## Alcance y resultado

- Archivo original: `WP_Final_Proyecto_ML.ipynb`; 183 celdas (72 código / 111 Markdown).
- Notebook validado estructuralmente con `nbformat` y comprobada la sintaxis Python de las celdas (exceptuando las líneas mágicas propias de Colab).
- **No se cambió ninguna celda de código experimental.** SHA-256 del contenido concatenado del código antes y después: `25d65d39d2d31270978fc57a46b24364c9993947858ebf4898e0afb4fcf5ae1c`.
- Se conservó la copia íntegra con sus salidas. La versión para GitHub reduce los resultados embebidos y conserva 5 visualizaciones t-SNE cuando estaban disponibles como PNG.
- **Limitación de esta auditoría:** no se ejecutó el notebook de principio a fin en Google Colab, ni se hicieron nuevos entrenamientos, descargas del dataset o nuevos accesos al test histórico. No se certifica reproducibilidad bit a bit en otro runtime.

## Correcciones aplicadas

1. Se mantuvieron las ocho referencias iniciales del notebook y se añadieron cinco fuentes académicas pertinentes, comprobadas contra publicaciones primarias: Guyon y Elisseeff (selección), Kohavi (validación cruzada), Bergstra y Bengio (optimización), Saito y Rehmsmeier (métricas en desbalance), Paszke *et al.* (PyTorch).
2. Se añadieron notas de citación **en contexto** dentro de las secciones de metodología, validación, pipelines, Transformer, Optuna, evaluación y t-SNE, en lugar de dejar todas las citas únicamente al final.
3. Se desplazó la sección de metodología estadística que estaba después de las referencias, y se cambió a pasado la descripción de Optuna ya ejecutada.
4. Se agregó una nota de cierre para distinguir test independiente congelado, resultados de desarrollo, análisis visual exploratorio y limitaciones de reproducibilidad.
5. Se creó `README.md`, `.gitignore` y `requirements.txt` para preparar la publicación futura en GitHub.
6. Se preparó una copia GitHub sin tablas o salidas voluminosas de ejecución ni potenciales identificadores presentes en esas salidas. Se conservaron los resultados documentados en el texto del notebook.

## Fortalezas verificadas por inspección del código

- La partición train/test se organiza por estudiante; hay controles de intersección de grupos.
- La ingeniería longitudinal filtra accesos VLE y entregas por fecha de corte. El código de la actividad 3.3 señala expresamente que no usa `score` como predictor.
- Se implementan pipelines con preprocesamiento y selección y existe validación repetida con agrupación.
- La actividad 3.39 en el notebook actual **solo recupera archivos históricos** y no vuelve a calcular predicciones del test.
- t-SNE trabaja con matrices de **desarrollo** y no modifica modelos ni evaluación independiente.
- La celda de persistencia protege el protocolo congelado y los CSV originales del test contra sobreescritura con distinto SHA.

## Precauciones pendientes de verificación en Colab

- **Ejecución limpia:** probar un ciclo de recuperación de snapshots y una ejecución parcial planificada en una sesión distinta. No ejecutar todos los experimentos y el test indiscriminadamente.
- **Versiones:** los checkpoints joblib y las dependencias de PyTorch pueden requerir versiones compatibles con la ejecución histórica. Registrar `pip freeze`/versiones del runtime real.
- **Prompts de IA:** varias celdas auxiliares conservan su propósito pero no un prompt literal de origen. No inventar prompts históricos; si el profesor exige la literalidad, adjuntar evidencia del historial o documentar las solicitudes que realmente se conserven.
- **GitHub privado/público:** validar el contenido del repositorio antes de publicar; nunca subir Drive privado, dataset, CSV con `id_student`, credenciales o checkpoints restringidos.
- **Presentación académica:** preparar defensa de la diferencia A/B y límites de t-SNE. Las conclusiones causales, institucionales y de abandono definitivo no están sustentadas.
- **Rúbrica:** la declaración "todo en el notebook" se respeta; README acompaña el repositorio, sin sustituir los resultados y la argumentación interna.

## Datos del trabajo previo preservados

Test independiente en cuatro ventanas, comparación F1 macro LR B menos LR A: semanas 2 (+0,06887), 4 (+0,07645), 6 (+0,09741) y 8 (+0,11510). Son resultados históricos del notebook, no recalculados aquí.

## Nota sobre la interpretación de t-SNE

Los resultados descriptivos se mantienen cualitativamente en 2.000, 10.000 y 19.233 estudiantes, con salvedades por distinta prevalencia, muestreo y proyecciones independientes. Ni la persistencia visual ni el color de los puntos constituyen evidencia estadística independiente de rendimiento.