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
  verfügbar (siehe `reghive.ini`)

## Installation

`RegHive.wlx64` (64-bit Total Commander) und/oder `RegHive.wlx` (32-bit)
plus den Ordner `lang\` in den TC-Plugin-Ordner kopieren, dann das Plugin
unter *Konfiguration → Optionen → Plugins → Lister-Plugins* eintragen
(oder die mitgelieferte `pluginst.inf` nutzen).

## Sprache

Die UI-Sprache wird in `reghive.ini` (gleicher Ordner wie die DLL)
eingestellt:

```ini
[Settings]
Language=de
```

Gültige Werte: `de`, `en`, `ru`, `uk`. Fehlt die Datei oder die
Einstellung, wird Deutsch verwendet.

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
