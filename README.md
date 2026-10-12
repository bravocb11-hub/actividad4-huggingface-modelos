# Actividad 4 — Comparación de modelos Hugging Face

Proyecto académico de clasificación binaria de sentimiento en **reseñas cinematográficas en inglés** de GLUE/SST-2, utilizado como aproximación experimental al análisis de comentarios de clientes. No clasifica tickets por área ni valida desempeño en una institución real.

## Modelos
- `distilbert/distilbert-base-uncased-finetuned-sst-2-english`
- `textattack/bert-base-uncased-SST-2`
- `textattack/roberta-base-SST-2`

## Entorno y ejecución
1. Abrir el archivo `.ipynb` que agregues a `notebooks/` en Google Colab.
2. Activar GPU T4 (Entorno de ejecución > Cambiar tipo de entorno de ejecución).
3. Ejecutar todas las celdas, incluida la instalación. La autenticación `HF_TOKEN` es **opcional** para estos recursos públicos; nunca publicar tokens.
4. Descargar las carpetas `data/` y `results/` generadas por la ejecución y agregarlas al repositorio. La instalación inicial desinstala paquetes de interfaz no utilizados del entorno temporal de Colab; se recomienda usar un runtime dedicado.
5. Revisar el reporte que agregues a `docs/` y contrastar sus cifras con las salidas del notebook y los CSV de `results/`.

## Resultados de referencia (verificar contra los documentos modificados)
| Modelo | Accuracy | F1 macro | Latencia mediana ms/texto | Parámetros (M) |
|---|---:|---:|---:|---:|
| DistilBERT | 0.875 | 0.874922 | 1.457 | 66.96 |
| BERT | 0.920 | 0.919992 | 4.070 | 109.48 |
| RoBERTa | 0.925 | 0.924953 | 2.974 | 124.65 |

Latencia: cinco pasadas de inferencia, lotes de 16, sincronización CUDA; mediana del tiempo total dividido entre 200 textos. No es latencia individual de una petición en producción.

## Selección y limitaciones
La regla académica del notebook recomienda RoBERTa, al superar F1 macro 0.85 y 100 ms/texto y obtener el mejor F1. La diferencia con BERT es de **un acierto en 200 ejemplos**, insuficiente para afirmar superioridad general. La muestra es pequeña, balanceada deliberadamente y está compuesta por reseñas de películas en inglés; requiere validación en datos representativos antes de cualquier aplicación empresarial.

## Archivos
- `notebooks/`: código ejecutado con salidas.
- `docs/`: análisis comparativo en Word.
- `data/`: guía y CSV generado por el notebook.
- `results/`: métricas transcritas y demás salidas a incorporar tras ejecución.
- `src/`: documentación de la implementación.
- `requirements.txt`: rangos de dependencias; los números exactos de versiones de una corrida están en `run_metadata.json` una vez exportado.

## Reproducibilidad
Semilla 42, 100 muestras por clase de SST-2 validation, batch 16, longitud máxima 128. Los checkpoints registran revisiones en los metadatos de ejecución, pero el notebook usa nombres de modelo sin fijar `revision` en la descarga: una futura actualización remota podría alterar resultados. Para reproducibilidad estricta, fijar hashes de revisión y versiones exactas después de validar el entorno.

## Archivos que debes añadir manualmente
- `notebooks/`: tu notebook modificado `.ipynb` (guardar con las salidas de ejecución).
- `docs/`: tu reporte Word modificado `.docx`.
- Si cambiaste métricas o metodología, actualiza también esta tabla, los CSV de `results/` y la conclusión para evitar inconsistencias.
