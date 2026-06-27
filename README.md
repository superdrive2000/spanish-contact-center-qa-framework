# spanish-contact-center-qa-framework

Artifacts para un framework exploratorio ASR-NLP-LLM orientado a evaluación de calidad en contact centers (español).

Este repositorio contiene notebooks y ejemplos para transcribir, analizar y generar reportes inteligentes sobre llamadas de atención al cliente usando modelos de ASR (por ejemplo WhisperX), un LLM local (ej.: Ollama / Llama 3.1) y procesamiento en Python.

Principales funcionalidades

- Procesado de transcripciones con diarización y normalización.
- Análisis por llamada mediante prompts a un LLM que devuelve un JSON con KPIs: empatía del agente, frustración del cliente, resolución, tipo de llamada y un resumen.
- Generación de reportes PDF agregados con KPIs y gráficas (ReportLab + matplotlib).
- Ejemplos de intercambio con LLM y plantillas de salida en Examples/.

Estructura del repositorio (resumen)

```
Examples/                Ejemplos de salidas y reportes (PDF / JSON)
  ├─ Transcription_example.json
  ├─ Sentiment_analysis_example.json
  └─ LLM_analyssis_example.json
Scripts/                 Notebooks con procesamiento, análisis y generación de PDF
  ├─ ASR.ipynb
  ├─ WER evaluation.ipynb
  └─ llama_test.ipynb   Notebook principal: procesa transcripciones, llama al LLM y genera PDF
README.md                Este archivo (documentación básica y guía de uso)
LICENSE                 Licencia del proyecto
.gitignore
```

Cómo encajar las piezas

- Las transcripciones JSON (con segmentos y etiquetas de speaker) se transforman a texto mediante funciones en los notebooks (build_transcription_from_json).
- Cada transcripción se envía al LLM (ej.: Ollama) con un prompt que pide únicamente un JSON con las métricas.
- Los JSON individuales se agregan a un DataFrame (pandas) para calcular KPIs y generar visualizaciones.
- Finalmente se crea un PDF resumen por agente con ReportLab.

Requisitos (estimado)

- Python 3.10+ (se usó .venv310 en ejemplos).
- Dependencias Python: ollama (cliente), pandas, matplotlib, reportlab, pillow. Opcional: whisperx o la herramienta ASR que use sus transcripciones.
- Ollama (o el backend LLM elegido) instalado y con el modelo configurado (en los notebooks se usa `llama3.1:8b`).

Instalación rápida (ejemplo)

```bash
# crear entorno
python -m venv .venv
source .venv/bin/activate   # o .\.venv\Scripts\activate en Windows
pip install --upgrade pip
pip install ollama pandas matplotlib reportlab pillow
# instalar otras dependencias ASR si las necesita (p. ej. whisperx)
```

Ejecución (notebooks)

- Abrir y ejecutar los notebooks en Scripts/ con JupyterLab/Jupyter Notebook.
- Notebook recomendado para análisis y generación de reporte: Scripts/llama_test.ipynb.
- Si prefiere ejecutar como script, extraer las celdas relevantes y ejecutar con `python` (los notebooks contienen código ejecutable claramente separado en funciones).

Archivos importantes a revisar

- Scripts/llama_test.ipynb — flujo principal: lectura de JSONs de transcripción, llamadas al LLM, creación de JSONs de análisis y generación del PDF final.
- Scripts/ASR.ipynb — ejemplos de integración ASR.
- Examples/ — muestras de salida (PDF, JSON) que muestran el formato esperado.

Cómo contribuir

- Abrir issues para sugerencias o bugs.
- Proponer mejoras vía Pull Requests. Incluya ejemplos reproducibles y requisitos de entorno.

Licencia

Este repositorio incluye un archivo LICENSE. Revíselo para conocer los términos de uso.

Contacto

Para preguntas o colaboración: abrir un issue o contactar al dueño del repositorio (superdrive2000).
