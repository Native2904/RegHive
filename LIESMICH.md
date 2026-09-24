<img width="1132" height="995" alt="2026-09-12_065525" src="https://github.com/user-attachments/assets/4cd51d13-746a-419f-ac74-fdbea5345715" />

# RegHive

Ein Total-Commander-Lister-Plugin (WLX), das **rohe, offline vorliegende
Windows-Registry-Hive-Dateien** liest — also genau die Dateien, die man
sonst nicht einfach öffnen kann, weil Windows die laufende Registry
gesperrt hält. Rein lesend; RegHive verändert die geöffnete Datei nie.

Typischer Anwendungsfall: eine Kopie von `NTUSER.DAT`, `SOFTWARE`,
`SYSTEM` usw. aus einem Backup, einer alten Festplatte oder einem
eingebundenen Image — Dateien, für die man sonst erst per `reg load` in
eine laufende Registry einhängen müsste, nur um reinzuschauen.

## Was das Plugin leistet

- Erkennt und parst rohe Hive-Dateien: `SYSTEM`, `SOFTWARE`, `SAM`,
  `SECURITY`, `DEFAULT`, `NTUSER.DAT`, `UsrClass.dat`, `*.hiv`
- Baumansicht der Schlüssel links, Werte-Tabelle (Name / Typ / Daten /
  Hinweis) rechts — Klick auf einen Schlüssel zeigt seine Werte
- Dekodiert alle gängigen Werttypen: `REG_SZ`, `REG_EXPAND_SZ`,
  `REG_MULTI_SZ`, `REG_DWORD`, `REG_QWORD`; `REG_BINARY` als
  Hex-Vorschau
- Zeigt den Zeitstempel der letzten Änderung pro Schlüssel
- **Hinweis-Spalte für Übertragbarkeit**: markiert Werte, die
  vermutlich nicht einfach auf einen anderen Rechner/Account übertragbar
  sind — SID-Referenzen, fest codierte Laufwerkspfade oder Pfade mit
  Umgebungsvariablen
- Rechtsklick auf einen Wert kopiert Name, Daten, "Name = Daten", oder
  öffnet eine **vollständige Hex+ASCII-Ansicht** in einem eigenen Fenster
  (mit Esc schließbar)
- **Suche** (Strg+F im Lister) ist an TCs eigenen Suchdialog angebunden —
  durchsucht Schlüsselnamen, Wertenamen und String-Wertinhalte;
  respektiert "Groß-/Kleinschreibung" und "Rückwärts", setzt immer an der
  aktuellen Baum-Auswahl an
- **Alt+F3** (nächste/vorherige Datei) nutzt dasselbe Fenster weiter,
  statt ein neues zu öffnen
- **Vergleichsmodus**: Rechtsklick auf den Baum → "Mit Datei
  vergleichen..." vergleicht zwei Hive-Dateien. Schlüssel/Werte werden
  markiert mit `[+]` (nur in Datei B), `[-]` (fehlt in Datei B), `[~]`
  (irgendwo darunter geändert), oder unmarkiert (identisch)
- Benutzeroberfläche auf Deutsch, Englisch, Russisch und Ukrainisch
  verfügbar; folgt automatisch der TC-Sprache (siehe *Sprache*)

## Installation

`RegHive.wlx64` (64-bit Total Commander) und/oder `RegHive.wlx` (32-bit)
plus `reghive.lng` in den TC-Plugin-Ordner kopieren, dann das Plugin
unter *Konfiguration → Optionen → Plugins → Lister-Plugins* eintragen
(oder die mitgelieferte `pluginst.inf` nutzen).

## Sprache

Die Oberflächensprache folgt automatisch Total Commander. `reghive.lng`
(gleicher Ordner wie die DLL) enthält pro Sprache einen Abschnitt;
RegHive verwendet den Abschnitt, dessen Name dem letzten Teil des Namens
der aktuellen TC-Sprachdatei entspricht — `WCMD_DEU.LNG` wählt `[deu]`,
`WCMD_RUS.LNG` wählt `[rus]`. Enthalten sind `[eng]`, `[deu]`, `[rus]`
und `[ukr]`. Fehlt der Abschnitt, ein Schlüssel oder die Datei, wird
Englisch verwendet.

Um eine Sprache unabhängig von TC festzulegen, in `reghive.ini`
(gleicher Ordner wie die DLL) eintragen:

```ini
[Settings]
Language=de
```

Gültige Werte: `auto` (Standard) oder ein Sprachcode wie `eng`, `deu`,
`rus`, `ukr` (die Kurzformen `en`, `de`, `ru`, `uk` funktionieren
ebenfalls).

### 

## Bekannte Einschränkungen

- Sehr große Hives (typischerweise `SOFTWARE`/`SYSTEM` auf lange
  genutzten Systemen) können ein indirektes Subkey-Listenformat
  (`ri`-Records) verwenden, das noch nicht geparst wird — betroffene
  Teilbäume werden dann einfach ausgelassen statt einen Absturz zu
  verursachen.
- Der Vergleichsmodus erkennt umbenannte Schlüssel nicht als
  "umbenannt" — ein umbenannter Schlüssel erscheint als ein entfernter
  und ein neuer Eintrag.
- Suche und Hex-Ansicht sind im Vergleichsmodus nicht verfügbar.
- Bewusst rein lesend — eine Editier-Funktion ist nicht geplant.

## Lizenz

MIT.
