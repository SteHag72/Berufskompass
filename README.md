# Berufskompass

Eine kleine, offline-fähige WebApp (reines HTML/JS, kein Backend) zur Berufsorientierung.
24 Fragen, drei Auswertungsachsen: **Beschäftigungsform**, **Umfeld & Branche**, **Interessen (Holland-Modell/RIASEC)**.

## Nutzung
Einfach `index.html` öffnen (lokal per Doppelklick oder über GitHub Pages).
Die Fragen werden aus `config.json` geladen.

## Antwort-Logging (Google Form)
Jede Antwort sowie das Endergebnis werden anonym an ein Google Form gesendet
(`fetch(..., {mode:"no-cors"})`), das in ein Google Sheet schreibt:
- **Timestamp**: einheitlicher Start-Zeitpunkt der Befragung (ISO 8601), gleich für alle Zeilen eines Durchlaufs
- **Frage-Nr**: Nummer der Frage (1–24) bzw. Achsen-Nr (1–3) für Ergebniszeilen
- **Frage**: Fragetext bzw. Name der Ergebnis-Richtung (z. B. „Wissenschaftler/in")
- **Antwort**: gewählte Options-Antwort bzw. Prozentwert (z. B. „37%")

Die Form-Action-URL und Entry-IDs stehen in `index.html` (`FORM_ACTION`, `FORM_FIELDS`).

## Eigene Fragen / Config anpassen
Auf der Startseite über **„Eigene Fragen laden …“** lässt sich eine eigene `config.json`
per Datei-Upload oder Copy&Paste importieren (wird im Browser lokal gespeichert, `localStorage`).

### Struktur von `config.json`

```json
{
  "meta": { "title": "...", "tag": "...", "intro": "...", "durationNote": "..." },
  "axes": [
    {
      "id": "roles",
      "title": "Beschäftigungsform",
      "color": "var(--axis1)",
      "categories": {
        "U": ["Unternehmer/in", "Beschreibung ..."]
      }
    }
  ],
  "questions": [
    {
      "nr": 1,
      "section": "Arbeitsweise & Werte",
      "text": "Was ist dir bei einer Stelle am wichtigsten?",
      "options": [
        { "label": "Sicherheit und ein planbarer Lebensweg", "weights": { "B": 2, "A": 1 } }
      ]
    }
  ]
}
```

- **`nr`** bestimmt die Reihenfolge der Fragen (aufsteigend sortiert).
- **`weights`** referenziert die Kategorie-Keys aus `axes[].categories`.
- Beliebig viele Achsen und Kategorien möglich — die App berechnet Scores generisch.

## GitHub Pages
Repo-Settings → Pages → Branch `main`, Root `/` → die App ist dann unter
`https://<user>.github.io/<repo>/` erreichbar.

## Hinweis
Der Berufskompass ist eine Orientierungshilfe, kein geprüfter psychologischer Test.
