# Synthetisches Interview System 🎤

Automatisierte synthetische Interviews mit AI-Personas für Lifestyle-Marken-Forschung mit LangChain und OpenRouter

**AI-Modell wechseln** (in `.env`):
```
DEFAULT_MODEL=mistralai/mistral-small-24b-instruct-2501:free
```

- 🤖 **3 einzigartige AI-Personas** (Anna, Tom, Julia)
- 🎯 **Flexibler Interview-Modus** (alle Personas oder einzeln)
- 📁 **Batch-Processing** (automatisierte Studien + Cron-Unterstützung)
- 🔗 **LangChain + OpenRouter** (kostengünstig)
- 📝 **JSON-Fragensystem** (einfach anpassbar)
- 💻 **CLI & Python API** (Kommandozeile + programmierbar)
- 📊 **JSON/Markdown Ausgabe** (strukturierte Daten + Berichte)
- 🧠 **Unabhängige Persona-Gedächtnisse** (konsistente Antworten)
- ⚡ **Günstig** (Mistral AI über OpenRouter)

## 👥 Die 3 AI-Personas

- **🌱 Anna (20)** - Umweltbewusste Studentin der Umweltwissenschaften. Kauft Second-Hand, ist auf Social Media aktiv und kann Greenwashing erkennen.
- **🏃‍♂️ Tom (40)** - Sportlicher Marketing-Manager in der Tech-Branche. Marathon-Läufer, schätzt Qualität über Preis und ist effizienz-orientiert.
- **👨‍👩‍👧‍👦 Julia (35)** - Praktische Familienmutter mit 2 Kindern. Teilzeit-Buchhalterin, preisbewusst, budgetorientiert und vertraut auf Mundpropaganda.

## Schnell-Start

### 1. API-Schlüssel besorgen
1. Gehen Sie zu: https://openrouter.ai/mistralai/mistral-small-24b-instruct-2501:free/api
2. Erstellen Sie einen kostenlosen Account
3. Kopieren Sie Ihren API-Schlüssel (beginnt mit `sk-or-v1-...`)

### 2. Installation & Start

**Linux/macOS:**
```bash
git clone https://github.com/thetabish/ai-personas.git
cd ai-personas
chmod +x run.sh && ./run.sh
```

**Windows:**
```cmd
git clone https://github.com/thetabish/ai-personas.git
cd ai-personas
run.bat
```

```powershell
# PowerShell - Alternative
git clone https://github.com/thetabish/ai-personas.git
cd ai-personas
.\run.bat
```

Die Scripts richten automatisch alles ein und fragen nach dem API-Schlüssel.

### 3. Manuelle Installation
```bash
git clone https://github.com/thetabish/ai-personas.git
cd ai-personas
pip install -r requirements.txt

# .env erstellen und API-Schlüssel einfügen:
# OPENROUTER_API_KEY=sk-or-v1-ihr_schluessel_hier

python interview.py --questions questions.json
```

## 💻 Verwendung

### CLI
```bash
# Alle Personas, Markdown-Ausgabe
python interview.py --questions questions.json

# JSON-Format
python interview.py --questions questions.json --format json

# Eigene Ausgabedatei  
python interview.py --questions questions.json --output meine_befragung
```

### Python API
```python
from interview import run_interview

# Alle 3 Personas (Anna, Tom, Julia)
results = run_interview("questions.json")

# Einzelne Persona
results = run_interview("anna", "questions.json")

# Mit Optionen
results = run_interview("questions.json", format="json", output_file="study")
```

### Batch-Processing
```bash
# Batch-Interview
python run_batch.py --config interview_batch.json

# Spezifische Agenten
python run_batch.py --config interview_batch.json --agents anna tom

# Cron-Job (stiller Modus)
python run_batch.py --config interview_batch.json --quiet
```

**Cron-Beispiel:**
```bash
# Tägliche Interviews um 2:00 Uhr
0 2 * * * cd /path/to/ai-personas && python run_batch.py --quiet
```

### Eigene Fragen
```json
{
  "questions": [
    "Ihre erste Frage hier",
    "Ihre zweite Frage hier"
  ]
}
```

## 🏗️ Technische Architektur & Entscheidungen

**Stack:** Python 3.8+ • LangChain • OpenRouter • Mistral AI

### Warum Mistral AI?
- **Günstig**: Mistral Small über OpenRouter ist sehr kostengünstig
- **Qualität**: Hochwertiges mehrsprachiges Modell (DE/EN)
- **Performance**: Schnelle Antwortzeiten für Interviews
- **Konsistenz**: Stabile Persona-Charakteristiken

### Warum OpenRouter?
- **Kostenkontrolle**: Günstige Modelle mit transparenten Preisen
- **Einfachheit**: Ein API-Schlüssel für viele AI-Modelle
- **Zuverlässigkeit**: Professioneller API-Gateway mit hoher Verfügbarkeit
- **Flexibilität**: Einfacher Modellwechsel ohne Code-Änderungen

### LangChain Integration
```python
# Vereinfachter Workflow:
PersonaAgent → LangChain → OpenRouter → Mistral AI → Antwort
```

**Warum LangChain?**
- **Abstraktion**: Einheitliche Schnittstelle für verschiedene AI-Modelle
- **Kontext-Management**: Automatische Verwaltung von Gesprächsverläufen
- **Prompt-Engineering**: Strukturierte Prompts für konsistente Ergebnisse
- **Zukunftssicherheit**: Einfacher Wechsel zwischen AI-Anbietern

### Programm-Flow
1. **Setup**: API-Validierung → Persona-Erstellung (LangChain)
2. **Interview**: Jede Persona antwortet unabhängig (eigener Kontext)
3. **Speicherung**: Strukturierte JSON/Markdown-Ausgabe
4. **Gedächtnis**: Personas erinnern sich an eigene Antworten (konsistent)

## Anpassung

**Neue Personas hinzufügen:**
```python
def create_neue_persona():
    return PersonaAgent(
        name="Max", age=25,
        characteristics="technikaffin, innovativ",
        background="Software-Entwickler...",
        detailed_personality="Du liebst neue Technologien..."
    )
```

**AI-Modell wechseln** (in `.env`):
```
DEFAULT_MODEL=mistralai/mistral-small-24b-instruct-2501:free
```

## 🔍 Fehlerbehebung

- **API-Schlüssel fehlt**: `.env` Datei prüfen
- **Abhängigkeiten fehlen**: `pip install -r requirements.txt`
- **Windows PowerShell**: Verwenden Sie `.\run.bat` statt `run.bat`
- **Windows**: Command Prompt (cmd) empfohlen für beste Kompatibilität
- **Test**: `python agents.py`
