# Damm Thermometer

[English](README.md) · **Castellano** · [Català](README.ca.md)

Plataforma de escucha activa y analítica de clima laboral para Estrella Damm. Desarrollada para el reto de Estrella Damm en UAB THE HACK 2026.

![Damm Thermometer](ui/assets/readme-damm-cover.jpg)

## Demostración

**[Ver el vídeo de la demo (1:24, MP4, 74 MiB)](demo.mp4)** · [Guion de la demostración](DEMO_SCRIPT.md)

Damm Thermometer ayuda a RRHH a medir el clima laboral en planta, logística, equipos comerciales en ruta y oficinas. El motor estadístico en Python calcula las métricas de los informes. La IA ayuda a redactar microconsultas y síntesis cualitativas. RRHH aprueba las consultas antes de publicarlas.

## Cómo funciona

Usa la barra lateral para cambiar entre **Dashboard**, **Generador Asistido**, **Insights**, **Historial y Acciones** y **Configuración**.

![Portal y barra de navegación lateral](ui/assets/readme-portal-navigation.png)

### Panel de clima laboral

Consulta el índice global de clima, la participación y su evolución. El panel abarca bienestar, liderazgo, condiciones de trabajo, desarrollo profesional, reconocimiento y alineación con los valores de la empresa.

![Panel de clima laboral](ui/assets/readme-dashboard.png)

### Generador y distribución de microconsultas

Redacta preguntas a partir de un objetivo escrito o díctalo localmente con Vosk. Previsualiza la consulta en Typeform Studio y revisa y aprueba el borrador en **Historial y Acciones**. Comparte la encuesta mediante códigos QR impresos, enlaces móviles o Microsoft Teams. En planta se puede abrir el formulario desde dispositivos compartidos. RRHH puede seguir las campañas y crear consultas de seguimiento.

![Generador de microconsultas y Typeform Studio](ui/assets/readme-generator-studio.png)

El historial muestra el estado de cada consulta y permite editarla, aprobarla o publicarla.

![Historial de campañas y aprobación de RRHH](ui/assets/readme-admin-history.png)

### Análisis estadístico

En **Insights**, compara la participación con los pesos del censo configurado para detectar qué colectivos están infrarrepresentados. El motor calcula medias ponderadas, intervalos de confianza bootstrap al 95 %, medidas de dispersión y contrastes entre periodos. Consulta la distribución Likert por pregunta y prueba escenarios sintéticos o un CSV en el laboratorio sin modificar las respuestas de las encuestas.

![Análisis estadístico y laboratorio de datos](ui/assets/readme-insights-lab.png)

Filtra por consulta, cuatrimestre o año. Para cada pregunta, consulta la distribución junto con la media, la desviación típica y el número de respuestas.

![Distribución de respuestas Likert por pregunta](ui/assets/readme-question-chart.png)

### Informes ejecutivos y PDF

En **Insights**, genera o vuelve a abrir una síntesis con el resumen, la tabla de cobertura, las alertas, el plan de acción y las preguntas de seguimiento. Pulsa **Exportar PDF** para descargar el informe o **Imprimir / Guardar PDF** para abrir el diálogo de impresión A4 del navegador. Allí puedes seleccionar una impresora o **Guardar como PDF**.

![Síntesis ejecutiva y exportación a PDF](ui/assets/readme-llm-synthesis.png)

## Controles de privacidad

- Se ocultan las medias de los colectivos con menos de cinco participantes.
- Los comentarios abiertos pasan por un filtro de patrones para eliminar identificadores comunes como correos, teléfonos, DNI/NIE e IBAN.
- Las respuestas se guardan en SQLite local. La política de retención elimina los registros de más de 90 días.

## Inicio rápido

Necesitas Git y Python 3.10 o superior. La demo local utiliza datos sintéticos.

### Windows (PowerShell)

```powershell
git clone https://github.com/IgnaciDM/Damn.git
cd Damn
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m backend.app
```

### Linux / macOS

```bash
git clone https://github.com/IgnaciDM/Damn.git
cd Damn
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python -m backend.app
```

Abre [http://127.0.0.1:8000](http://127.0.0.1:8000) una vez iniciado el servidor.

## Integraciones opcionales

La IA externa requiere tu propia clave. Introdúcela en **Configuración → Clave API del modelo de IA** y pulsa **Guardar Configuración**. Los clientes de la API pueden enviar el campo `api_key` en una petición JSON a `POST /api/settings`. La clave introducida desde Configuración dura hasta que se reinicia el servidor. Para cargarla al arrancar, define `UTH_KEY` en el entorno o copia [.env.example](.env.example) al archivo local `.env` y añádela allí. Sin clave, las encuestas y síntesis usan plantillas locales.

- `UTH_KEY`, `AI_MODEL`, `AI_BASE_URL`, `GEMINI_API_KEY` · Credenciales y modelo del proveedor de IA.
- `TYPEFORM_API_TOKEN` · Publicación en Typeform e importación de respuestas.
- `TEAMS_WEBHOOK_URL` · Webhook de Microsoft Teams.
- `VOSK_MODEL_PATH` · Directorio del modelo Vosk de castellano ya extraído.
- `PULSO_PUBLIC_URL` · URL base pública para compartir códigos QR.
- `PULSO_DATABASE` · Ruta de SQLite. El valor por defecto es `data/pulso.sqlite3`.
- `PORT` · Puerto HTTP. El valor por defecto es `8000`.

## Estructura del repositorio

- [backend/](backend/) contiene la API HTTP, los flujos de encuestas y el motor estadístico.
- [ui/](ui/) contiene la interfaz web y sus recursos.
- [dataset/](dataset/) y [test_dataset/](test_dataset/) contienen el generador de datos sintéticos y los conjuntos de validación.
- [tests/](tests/) cubre la API y los cálculos estadísticos.

## Pruebas

**Windows (PowerShell)**

```powershell
.\.venv\Scripts\python.exe -m unittest discover -s tests -v
```

**Linux / macOS**

```bash
.venv/bin/python -m unittest discover -s tests -v
```

## Licencia

El proyecto se ofrece bajo la **licencia PolyForm Free Trial 1.0.0**. Permite evaluarlo durante menos de 32 días naturales consecutivos y prohíbe redistribuir copias. Consulta el texto completo en [LICENSE](LICENSE).
