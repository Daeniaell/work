# work

## REA – Reverse Engineer Anything

[REA](https://github.com/morluto/rea) (npm-Paket `rea-agents`, MIT-Lizenz) ist in
diesem Repo für Claude Code eingerichtet:

- `.mcp.json` registriert den REA-MCP-Server, fest auf Version 6.7.0
  (`npx -y rea-agents@6.7.0 mcp`). Beim Sitzungsstart lädt `npx` das Paket
  automatisch; eine globale Installation ist nicht nötig.
- `.claude/settings.json` gibt den Server frei (`enabledMcpjsonServers`).
- `.claude/skills/reverse-engineer-anything/` enthält die passende
  Arbeitsanleitung (Skill) aus REA 6.7.0.

Voraussetzungen: Node.js 22.x (>= 22.19), 24.x (>= 24.11) oder 26+, npm und unter
Linux ein procps-kompatibles `ps`.

### Was ohne weitere Werkzeuge geht

JavaScript-/Electron-Apps, .NET-Assemblies, Go-/Rust-Build-Infos, Webseiten
(Chrome-Browser), HAR-Mitschnitte, Pakete/Ressourcen und Offline-ELF/PE-Analyse
mit GNU objdump.

### Was ein Analyse-Werkzeug braucht

- Native Binaries (Pseudocode, Aufrufe): Ghidra 12.1.x (`GHIDRA_INSTALL_DIR`,
  JDK 21) oder Hopper bzw. IDA
- Android-APKs: JADX headless (`REA_JADX_MCP_JAR`)
- Firmware: Binwalk/Unblob; Paketmitschnitte: TShark

### Terminal

```bash
npx -y rea-agents@6.7.0 --help
npx -y rea-agents@6.7.0 doctor --json
npx -y rea-agents@6.7.0 analyze-javascript-application /absoluter/pfad/zur/app --json
```

### Aktualisieren

Version in `.mcp.json` anheben und den Skill neu kopieren
(`npx -y rea-agents@<version> setup --client claude_code --yes` installiert ihn
nach `~/.claude/skills/reverse-engineer-anything`).

Nur für legale Analysen von Software, die uns gehört oder für die wir berechtigt
sind (siehe REA `DISCLAIMER.md`).
