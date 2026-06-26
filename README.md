# Llama_Dispatcher – Instance: Speedy

Dieses private Repository enthält die maschinenspezifische Konfiguration der Instanz **Speedy**
für den [Llama_Dispatcher](https://github.com/SomeSunlight/Llama_Dispatcher).

## Inhalt

| Verzeichnis / Datei | Beschreibung |
|---|---|
| `instance.yaml` | Machine-GUID und Nickname dieser Instanz |
| `profiles/` | YAML-Profile (llama.cpp-Startparameter) für diese Maschine |
| `ensembles/` | YAML-Ensembles (Zusammenstellungen mehrerer Profile) |
| `engines/` | Engine-Konfiguration (CUDA) |
| `data/metrics.db` | SQLite-Datenbank mit Benchmark- und Laufzeit-Metriken |
| `data/3090_models.ini` | Modell-Preset-Datei für llama-server (Multi-Model-Router) |

## Zugehöriger Dispatcher

Der Dispatcher selbst (Code, Defaults, Dokumentation) liegt im öffentlichen Repo:
→ https://github.com/SomeSunlight/Llama_Dispatcher

## Nutzung

```bash
uv run src/dispatcher.py serve --ensemble <name> --instance Speedy
```

## Lizenz

MIT – nur relevant falls dieses Repo jemals veröffentlicht wird.

