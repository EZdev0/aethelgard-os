# AETHELGARD OS

Ein modular aufgebautes, hochsicheres Android-OS mit klar getrennten Schichten für Installation,
Boot-Validierung und Klon-OS-Experimente.

## Struktur (Phase 1 – Foundation)

```
guardian/         THE GUARDIAN Installer (C++)
 gate/            THE GATE Boot-Wächter (C++)
 kontrollzentrum/ System-App (Kotlin/Gradle)
 mainos/          Main OS-Assets & Overlay-Definitionen
 config/          Zentrale Gerätekonfigurationen
 docs/            Architektur- und Prozessdokumentation
 tools/           Build- und Test-Utilities
```

## Build-Übersicht

### Guardian (CMake)

```bash
cmake -S guardian -B build/guardian
cmake --build build/guardian
```

### Gate (CMake)

```bash
cmake -S gate -B build/gate
cmake --build build/gate
```

### Kontrollzentrum (Gradle)

```bash
cd kontrollzentrum
./gradlew :app:assembleDebug
```

> Hinweis: Das Gradle-Wrapper-Script folgt in Phase 1. Bis dahin kann eine lokale Gradle-Installation verwendet werden.

## Zentrale Konfigurationen

Geräteprofile liegen unter `config/devices/` und definieren Mindestvoraussetzungen,
Partitionstypen und Ziel-Android-Versionen.
