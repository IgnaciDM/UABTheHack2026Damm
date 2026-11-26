# Damm Thermometer

[English](README.md) · [Castellano](README.es.md) · **Català**

Plataforma d’escolta activa i seguiment del clima laboral per a Estrella Damm. Desenvolupada per al repte d’Estrella Damm a UAB THE HACK 2026.

![Damm Thermometer](ui/assets/readme-damm-cover.jpg)

## Demostració

**[Mira el vídeo de la demo (1:24, MP4, 74 MiB)](demo.mp4)** · [Guió de la demostració en castellà](DEMO_SCRIPT.md)

Damm Thermometer ajuda Recursos Humans a mesurar el clima laboral a planta, logística, equips comercials en ruta i oficines. El motor estadístic en Python calcula les mètriques dels informes. La IA ajuda a redactar microconsultes i resums qualitatius. Recursos Humans aprova les consultes abans de publicar-les.

## Com funciona

Fes servir la barra lateral per canviar entre **Dashboard**, **Generador Asistido**, **Insights**, **Historial y Acciones** i **Configuración**.

![Portal i barra de navegació lateral](ui/assets/readme-portal-navigation.png)

### Tauler de clima laboral

Consulta l’índex global de clima, la participació i la seva evolució. El tauler cobreix el benestar, el lideratge, les condicions de treball, el desenvolupament professional, el reconeixement i l’afinitat amb els valors de l’empresa.

![Tauler de clima laboral](ui/assets/readme-dashboard.png)

### Generador i distribució de microconsultes

Redacta preguntes a partir d’un objectiu escrit o dicta’l localment amb Vosk. Previsualitza la consulta a Typeform Studio i revisa i aprova l’esborrany a **Historial y Acciones**. Comparteix l’enquesta amb codis QR impresos, enllaços per a mòbil o Microsoft Teams. A planta es pot obrir el formulari des de dispositius compartits. Recursos Humans pot fer el seguiment de les campanyes i crear consultes de seguiment.

![Generador de microconsultes i Typeform Studio](ui/assets/readme-generator-studio.png)

L’historial mostra l’estat de cada consulta i permet editar-la, aprovar-la o publicar-la.

![Historial de campanyes i aprovació de Recursos Humans](ui/assets/readme-admin-history.png)

### Anàlisi estadística

A **Insights**, compara la participació amb els pesos del cens configurat per detectar quins col·lectius estan infrarepresentats. El motor calcula mitjanes ponderades, intervals de confiança bootstrap del 95 %, mesures de dispersió i contrastos entre períodes. Consulta la distribució Likert per pregunta i prova escenaris sintètics o un CSV al laboratori sense modificar les respostes de les enquestes.

![Anàlisi estadística i laboratori de dades](ui/assets/readme-insights-lab.png)

Filtra per consulta, quadrimestre o any. Per a cada pregunta, consulta la distribució juntament amb la mitjana, la desviació típica i el nombre de respostes.

![Distribució de respostes Likert per pregunta](ui/assets/readme-question-chart.png)

### Informes executius i PDF

A **Insights**, genera o torna a obrir una síntesi amb el resum, la taula de cobertura, les alertes, el pla d’acció i les preguntes de seguiment. Prem **Exportar PDF** per descarregar l’informe o **Imprimir / Guardar PDF** per obrir el diàleg d’impressió en A4 del navegador. En aquest diàleg pots triar una impressora o **Desa com a PDF**.

![Síntesi executiva i exportació a PDF](ui/assets/readme-llm-synthesis.png)

## Controls de privacitat

- S’amaguen les mitjanes dels col·lectius amb menys de cinc participants.
- Els comentaris oberts passen per un filtre de patrons que elimina identificadors habituals com ara adreces de correu, telèfons, DNI/NIE i IBAN.
- Les respostes es desen en una base de dades SQLite local. La política de retenció elimina els registres de més de 90 dies.

## Inici ràpid

Cal tenir Git i Python 3.10 o posterior. La demo local fa servir dades sintètiques.

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

Obre [http://127.0.0.1:8000](http://127.0.0.1:8000) un cop arrenqui el servidor.

## Integracions opcionals

La IA externa requereix la teva pròpia clau. Introdueix-la a **Configuración → Clave API del modelo de IA** i prem **Guardar Configuración**. Els clients de l’API poden enviar el camp `api_key` en una petició JSON a `POST /api/settings`. La clau introduïda des de Configuració dura fins que es reinicia el servidor. Per carregar-la a l’inici, defineix `UTH_KEY` a l’entorn o copia [.env.example](.env.example) al fitxer local `.env` i afegeix-la allà. Sense clau, les enquestes i les síntesis fan servir plantilles locals.

- `UTH_KEY`, `AI_MODEL`, `AI_BASE_URL`, `GEMINI_API_KEY` · Credencials i model del proveïdor d’IA.
- `TYPEFORM_API_TOKEN` · Publicació a Typeform i importació de respostes.
- `TEAMS_WEBHOOK_URL` · Webhook de Microsoft Teams.
- `VOSK_MODEL_PATH` · Directori del model Vosk de castellà ja extret.
- `PULSO_PUBLIC_URL` · URL base pública per compartir codis QR.
- `PULSO_DATABASE` · Camí de la base SQLite. El valor per defecte és `data/pulso.sqlite3`.
- `PORT` · Port HTTP. El valor per defecte és `8000`.

## Estructura del repositori

- [backend/](backend/) conté l’API HTTP, els fluxos d’enquestes i el motor estadístic.
- [ui/](ui/) conté la interfície web i els recursos.
- [dataset/](dataset/) i [test_dataset/](test_dataset/) contenen el generador de dades sintètiques i els conjunts de validació.
- [tests/](tests/) cobreix l’API i els càlculs estadístics.

## Proves

**Windows (PowerShell)**

```powershell
.\.venv\Scripts\python.exe -m unittest discover -s tests -v
```

**Linux / macOS**

```bash
.venv/bin/python -m unittest discover -s tests -v
```

## Llicència

El projecte s’ofereix amb la **llicència PolyForm Free Trial 1.0.0**. Permet avaluar-lo durant menys de 32 dies naturals consecutius i prohibeix redistribuir-ne còpies. Consulta el text complet a [LICENSE](LICENSE).
