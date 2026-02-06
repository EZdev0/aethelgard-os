# Systemübersicht

AETHELGARD OS besteht aus klar getrennten Schichten, die zusammen eine sichere Installation,
verlässliche Boot-Validierung und eine isolierte Spielwiese für Custom ROMs ermöglichen.

## Komponenten und Aufgaben

- **THE GUARDIAN (L0):** Paranoider Installer mit Zustandsmaschine, Backup und atomarem A/B-Flash.
- **THE GATE (L1):** Boot-Wächter mit Integritätsprüfungen und Recovery-Entscheidungslogik.
- **MAIN OS (L2):** Unveränderliches Android-System mit OverlayFS-Schutz.
- **KLON OS (L3):** DSU-basierte Sandbox für Root/Custom ROMs.
- **KONTROLLZENTRUM (L4):** System-App zum Laden, Prüfen und Starten von Klon-ROMs.

## Interaktionsfluss (vereinfacht)

```mermaid
sequenceDiagram
    participant User as Nutzer
    participant Guardian as THE GUARDIAN
    participant Gate as THE GATE
    participant MainOS as MAIN OS
    participant Ctrl as Kontrollzentrum
    participant Dsu as DSU/Klon OS

    User->>Guardian: Installation starten
    Guardian->>Guardian: Hardware/Backup/Checksummen
    Guardian->>Gate: Gate installieren
    Guardian->>MainOS: Main OS flashen (inaktiver Slot)
    Guardian->>User: Neustart

    User->>Gate: Boot
    Gate->>Gate: Integritätsprüfung
    Gate->>MainOS: Boot freigeben
    MainOS->>User: System bereit

    User->>Ctrl: Klon-ROM auswählen
    Ctrl->>Ctrl: ROM prüfen (Signatur/Hash)
    Ctrl->>Dsu: DSU initialisieren
    Dsu->>User: Klon OS aktiv
```

## Sicherheits- und Datenfluss-Highlights

- **Kein Brick:** Schreibvorgänge erfolgen nur im inaktiven Slot mit Verifikation.
- **Daten-Schutz:** OverlayFS isoliert Systemänderungen; Benutzerdateien bleiben getrennt.
- **Self-Healing:** Fehlgeschlagene Boots lösen Gate-Recovery oder Rollback aus.

## Erweiterbarkeit

Die Schichtenstruktur erlaubt es, neue Geräteprofile, ROM-Validierer oder Test-Tools
unabhängig einzubringen, ohne die Sicherheitsgrenzen zu verwässern.
