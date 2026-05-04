# OpenCode Configuration

Konfiguracja niestandardowych agentów i strategii dla OpenCode.

## Opis projektu

Projekt definiuje konfigurację dla OpenCode - narzędzia CLI wspomagającego programistów w zadaniach inżynierii oprogramowania. Konfiguracja obejmuje niestandardowe agenty, ich zachowania i uprawnienia.

## Wymagania

- Node.js
- OpenCode CLI (`npm install -g opencode`)
- Plugin: `@opencode-ai/plugin` v1.14.33

## Struktura projektu

```
opencode-config/
├── agents/                  # Definicje agentów ładowane przez OpenCode
│   ├── Agent.md
│   ├── Project-explorer.md
│   ├── Docs-writer.md
│   └── Docs-updater.md
├── commands/              # Placeholder dla poleceń
├── skills/                # Placeholder dla umiejętności
├── package.json           # Zależności projektu
└── .gitignore            # Ignorowane pliki
```

## Agendy

### Agent (główny)

Główny agent odpowiedzialny za implementację funkcji, naprawę błędów i refaktoryzację. Używa wzorca subagenta - najpierw eksploruje projekt, następnie proponuje warianty implementacji.

**Właściwości:**
- `mode`: primary
- `temperature`: 0.2
- `steps`: 28
- `permission`: edit, bash, webfetch, websearch, question, task

### Project-explorer

Subagent do rozpoznawania projektu - analizuje typ repozytorium, stack, strukturę, punkty wejścia i sugeruje lokalizacje zmian.

**Właściwości:**
- `mode`: subagent
- `temperature`: 0.1
- `steps`: 10

### Docs-writer

Agent do tworzenia dokumentacji technicznej w formacie Markdown dla GitHub.

**Właściwości:**
- `mode`: primary
- `temperature`: 0.3
- `steps`: 15

### Docs-updater

Agent do aktualizacji istniejącej dokumentacji.

## Użycie

Konfiguracja jest automatycznie pobierana przez OpenCode, jeśli katalog jest używany jako `OPENCODE_CONFIG_DIR` albo skopiowany do `~/.config/opencode`.
W markdownowych agentach OpenCode używa frontmatter YAML dla konfiguracji, a instrukcje agenta są treścią pliku po drugim separatorze `---`.

Aby użyć:
```bash
# Bash/Zsh
export OPENCODE_CONFIG_DIR=~/Pulpit/Projekty/opencode-config
opencode --agent Agent
```

```fish
# Fish
set -x OPENCODE_CONFIG_DIR ~/Pulpit/Projekty/opencode-config
opencode --agent Agent
```

## Development

```bash
# Instalacja zależności
npm install
```

## Licencja

MIT
