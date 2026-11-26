# Damm Thermometer

**English** · [Castellano](README.es.md) · [Català](README.ca.md)

Continuous employee listening and workplace analytics for Estrella Damm. Built for the Estrella Damm challenge at UAB THE HACK 2026.

![Damm Thermometer](ui/assets/readme-damm-cover.jpg)

## Demo

**[Watch the demo (1:24, MP4, 74 MiB)](demo.mp4)** · [Demo walkthrough in Spanish](DEMO_SCRIPT.md)

Damm Thermometer helps HR measure workplace climate across production, logistics, field sales and offices. The Python statistics engine computes report metrics. AI helps draft pulse surveys and write qualitative summaries. HR approves surveys before publication.

## How it works

Use the sidebar to switch between **Dashboard**, **Generador Asistido**, **Insights**, **Historial y Acciones** and **Configuración**.

![Project portal and sidebar](ui/assets/readme-portal-navigation.png)

### Workplace climate dashboard

Track the overall workplace climate score, participation and trends. The dashboard covers well-being, leadership, working conditions, professional development, recognition and alignment with company values.

![Workplace climate dashboard](ui/assets/readme-dashboard.png)

### Pulse survey builder and distribution

Draft questions from a written objective or dictate it locally with Vosk. Preview the flow in Typeform Studio, then review and approve the draft in **Historial y Acciones**. Share the survey via printed QR codes, mobile links or Microsoft Teams. Plant teams can open the response form on shared devices. HR can track campaigns and create follow-up surveys.

![Survey builder and Typeform Studio](ui/assets/readme-generator-studio.png)

The approval history shows each survey’s status and actions such as editing, approval and publication.

![HR campaign history and approval](ui/assets/readme-admin-history.png)

### Statistical analysis

In **Insights**, compare participation with the configured workforce shares to see which groups are underrepresented. The engine produces census-weighted averages, 95% bootstrap confidence intervals, dispersion measures and tests for changes between periods. Inspect Likert responses by question and use the data lab to try synthetic scenarios or upload a CSV independently of live survey responses.

![Statistical analysis and data lab](ui/assets/readme-insights-lab.png)

Filter by survey, four-month period or year. For each question, review the distribution alongside the mean, standard deviation and response count.

![Likert response distribution by question](ui/assets/readme-question-chart.png)

### Executive reports and PDF

In **Insights**, generate or reopen a synthesis with a summary, coverage table, alerts, proposed actions and follow-up questions. Select **Exportar PDF** to download the report or **Imprimir / Guardar PDF** to open the browser’s A4 print dialog. From there, choose a printer or **Save as PDF**.

![Executive synthesis and PDF export](ui/assets/readme-llm-synthesis.png)

## Privacy controls

- Cohort averages are hidden when fewer than five people responded.
- Free-text responses pass through a pattern-based filter for common identifiers such as emails, phone numbers, DNI/NIE and IBANs.
- Responses are stored in local SQLite. The retention policy removes records older than 90 days.

## Quick start

You need Git and Python 3.10 or later. The local demo uses synthetic data.

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

Open [http://127.0.0.1:8000](http://127.0.0.1:8000) once the server starts.

## Optional integrations

External AI requires your own API key. Enter it under **Configuración → Clave API del modelo de IA** and select **Guardar Configuración**. API clients can send the `api_key` field in a JSON request to `POST /api/settings`. A key entered through settings lasts until the server restarts. To load it on startup, set `UTH_KEY` in your environment or copy [.env.example](.env.example) to the local `.env` file and add it there. Without a key, surveys and summaries use local templates.

- `UTH_KEY`, `AI_MODEL`, `AI_BASE_URL`, `GEMINI_API_KEY` · AI provider credentials and model.
- `TYPEFORM_API_TOKEN` · Typeform publishing and response import.
- `TEAMS_WEBHOOK_URL` · Microsoft Teams webhook.
- `VOSK_MODEL_PATH` · Extracted Spanish Vosk model directory.
- `PULSO_PUBLIC_URL` · Public base URL for shareable QR codes.
- `PULSO_DATABASE` · SQLite database path. The default is `data/pulso.sqlite3`.
- `PORT` · HTTP port. The default is `8000`.

## Repository layout

- [backend/](backend/) contains the HTTP API, survey workflows and statistics engine.
- [ui/](ui/) contains the web interface and assets.
- [dataset/](dataset/) and [test_dataset/](test_dataset/) contain the synthetic data generator and validation datasets.
- [tests/](tests/) covers the API and statistical calculations.

## Tests

**Windows (PowerShell)**

```powershell
.\.venv\Scripts\python.exe -m unittest discover -s tests -v
```

**Linux / macOS**

```bash
.venv/bin/python -m unittest discover -s tests -v
```

## License

The project is available under the **PolyForm Free Trial License 1.0.0**. It permits evaluation for fewer than 32 consecutive calendar days and prohibits redistribution of copies. See the full terms in [LICENSE](LICENSE).
