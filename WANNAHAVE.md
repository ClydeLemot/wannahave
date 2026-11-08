# WANNAHAVE | Portabler Replikationsprompt v0.3

> **Verwendung:** Den gesamten Inhalt dieses Dokuments an einen ausführenden KI-Agenten mit Zugriff auf das Zielsystem übergeben. Das Dokument ist der Installationsauftrag selbst. Es enthält weder persönliche Wunschdatensätze noch Quell-Workspace-IDs.
>
> **Evidenzgrenze:** Dies ist eine auf Notion-Quellmetadaten und dokumentierten Funktionsverträgen basierende **portable Kernrekonstruktion**, kein nachgewiesen funktionsidentischer Snapshot der laufenden v0.6-Automation. Die vollständige v0.6-Dateianlage und das Solver-Quellarchiv konnten nicht als Textinhalt extrahiert werden. Alle fehlenden exakten Implementierungsdetails sind Blocker, keine Einladung zur Erfindung.

## 0A · ZWINGENDER AUSFÜHRUNGSVERTRAG (v0.3)

**WICHTIG: Diese Datei ist ein INSTALLATIONSAUFTRAG, keine Gesprächsgrundlage, Rechercheaufgabe oder Einladung zu Architekturentwürfen.** Bei Übergabe durch einen Nutzer mit Aufforderung zur Installation ist das nächste Ziel eine tatsächliche, verifizierte Zustandsänderung im Zielsystem. Das Aufzählen von Schritten ohne Umsetzung ist ein FEHLSCHLAG.

### Ausführungspflicht und Werkzeugbindung

1. **Direkt starten.** Erster verfügbarer Werkzeugschritt: verfügbare Notion-/Datenbank-/Datei-/Automationswerkzeuge feststellen und zielgerichtet den vorhandenen WANNAHAVE-Bestand lesen. Vorher keine ausufernde Planung, kein Interview und keine neue Spezifikation schreiben.
2. **Eine ausführbare Route wählen, keine Architektur erfinden.** Diese Version enthält einen konkreten **Notion-Adapter** mit exaktem Schema. Bei verbundenem, schreibfähigem Notion verwende ihn. Mögliche Werkzeugnamen: `mcp__Notion__search`, `mcp__Notion__fetch`, `mcp__Notion__notion_create_pages`, `mcp__Notion__notion_create_database`, `mcp__Notion__notion_update_data_source`, `mcp__Notion__notion_create_view`. Ermittle die tatsächlich verfügbaren Namen/Schemas; erfinde keine Aufrufparameter. Wende die YAML-Felder mit *exakt den angegebenen Namen, Typen und Auswahloptionen* an. Notion-IDs der Zielinstanz müssen aus echten Toolantworten stammen.
3. **Fehlt Notion?** Ein anderes Backend ist in dieser Version **noch nicht vollständig spezifiziert**. Erfinde keinen eigenen PostgreSQL-/SQLite-/App-Stack und behaupte keine Gleichwertigkeit. Gib `BLOCKED_BACKEND` aus und nenne als einzigen konkreten nächsten Schritt: Notion verbinden **oder** die explizit spezifizierte alternative Backend-Implementierung bereitstellen. Den restlichen Installationsplan nicht als erledigt ausgeben.
4. **Fehlende Pflichtinformation?** Frage nur EINEN tatsächlichen Blocker, z. B. welchen Ziel-Workspace du verwenden sollst, wenn kein eindeutiger autorisierter Zielort feststeht. Kann der Zielort eindeutig aus dem Nutzerauftrag und den Werkzeugdaten bestimmt werden, stelle keine weitere Frage.
5. **Freigabe:** Ein ausdrücklicher Nutzerauftrag, WANNAHAVE in einer konkret benannten Zielumgebung zu installieren, erlaubt noch keinen Datenverlust. Prüfe das Delta. Bei nur additiven, reversiblen Objekten und ausdrücklicher Gesamtfreigabe direkt handeln und nicht vor jeder Tabelle erneut fragen. Falls die Gesamtfreigabe fehlt, zeige EINMAL die genaue Änderungsliste und frage EINMAL. Löschen, Überschreiben, riskante Migrationen und Käufe brauchen ihre eigene Freigabe.
6. **Kein Selbstgespräch:** Keine Alternativarchitekturen, Branding-/UI-Debatten, Softwarevergleiche, weitere Generatoren oder unbestellten Refactorings. Fehlendes v0.6-Datei-Artefakt und fehlender optionaler Solver **blockieren die Kerninstallation nicht**; kennzeichne lediglich deren Funktionsgrenze. Nach jedem echten Werkzeugresultat den nächsten Installationsschritt durchführen.
7. **Keine Phantom-Installation:** Wenn das System weder Notion-Werkzeuge noch Schreibrechte bereitstellt, melde in 3–5 Zeilen `BLOCKED_SETUP`/`BLOCKED_BACKEND`, das konkrete Hindernis und die erforderliche Nutzeraktion. Sätze wie „habe eingerichtet“ sind ohne nachgelesene Objekt-IDs und Zustände verboten.

### Atomare Ausführungsfolge

Diese Tabelle ist eine **auszuführende Befehlsfolge**, keine Checkliste für einen Bericht. Überspringe nur nach belegtem `NOOP`.

| Schritt | Vorbedingung | Erforderliche Aktion | Beleg für PASS |
| --- | --- | --- | --- |
| X00 | Nutzer will Installation | Ziel-Tools und Zielort konkret feststellen; vorhandene WANNAHAVE-Seite/DBs lesen | tatsächliche Werkzeugantworten oder exakter Blocker |
| X01 | Zielort + nötige Gesamtfreigabe | Einmalig die WANNAHAVE-Elternseite erstellen, falls nicht vorhanden | Seite durch Fetch/Readback identifiziert |
| X02 | Elternseite existiert | DB 01–05 gemäß YAML in Reihenfolge erstellen oder fehlende Properties ergänzen, pro DB vorhandenen Zustand vorher prüfen | fünf echte DB-IDs, alle Schemafelder/Optionen nachgelesen |
| X03 | fünf DBs vorhanden | drei Relationsfelder zu den ermittelten Ziel-Data-Sources herstellen | Relationsziele aus Ziel-API nachgelesen |
| X04 | Schema & Relationen stimmen | exakt spezifizierte Ansichten erstellen; unklare View-Details nicht erfinden | vorhandene/erstellte Views gelesen, Lücken als VIEW_PARTIAL |
| X05 | Datenkern vorhanden | Integritätsprüfung und idempotenten zweiten Schema-Lauf ausführen | zweiter Durchlauf erzeugt 0 DBs, 0 doppelte Felder |
| X06 | Scheduler zugänglich und freigegeben | genau einen WANNAHAVE-Job mit dem G0–G6-Lauf einrichten/aktualisieren | Job-ID, Intervall und echter Testlauf überprüft |
| X07 | vorherige Schritte geprüft | Ergebnis mit PASS/PARTIAL/BLOCKED pro Schritt und tatsächlichen Ziel-URLs ausgeben | keine unbelegten Erfolgsbehauptungen |

**Arbeitsmodus:** Wiederhole `READ -> DIFF -> APPLY -> READBACK` für jedes Zielobjekt. Bei API-Fehlern nur die betroffene Operation prüfen/wiederholen. Arbeite auch bei optionalen fehlenden Modulen an allen übrigen freigegebenen Kernschritten weiter.

**Stopbedingungen:** (a) tatsächliche fehlende Berechtigung; (b) unbekannter Zielort, den nur der Nutzer bestimmen kann; (c) fehlende explizite Gesamtfreigabe; (d) inkompatible Bestandsressource mit Migrationsrisiko; (e) keine definierte Backend-Implementierung. Alles andere ist zu erledigende Arbeit, kein Grund für eine bloße Empfehlung.

**Nicht zulässiger Endzustand:** „Hier ist, was du jetzt tun solltest“, „ich würde fünf Datenbanken anlegen“, reine Architekturplanung oder `READY` ohne echten Readback. Wenn du technisch nichts mutieren kannst, melde den wahren Blocker, statt Arbeit zu simulieren.

---

## START · Verbindlicher Ausführungsvertrag (vor allem anderen lesen)

**Dies ist ein INSTALLATIONSAUFTRAG, keine Einladung zu einem Architekturreferat.** Beginne bei vorhandenen Werkzeugen innerhalb dieses Aufrufs mit einer echten lesenden Tooloperation. Gib nicht zuerst einen langen Plan, ein Sollkonzept oder einen alternativen Entwurf aus. Nach höchstens einer kompakten Bestandsaufnahme gehe zum ersten tatsächlich freigegebenen Schreibschritt. Wiederhole keine philosophischen Abwägungen, keine erneute Systementwicklung, keine Pseudo-Tools.

**Deterministische Auswahl des Speicheradapters:**
1. Hat der Nutzer ein konkretes Ziel-Backend gewählt und sind dafür verifizierbar Schreibrechte vorhanden, verwende dieses Backend. Unterstützte Adapter dieser Fassung: **Notion** und **SQLite**.
2. Ohne Vorgabe: Wenn Notion verbunden, beschreibbar und ein erlaubter Zielbereich erkennbar ist, verwende Notion.
3. Sonst, wenn Python 3 + sqlite3 und ein *dauerhaft* beschreibbares Zielverzeichnis nachgewiesen sind, verwende SQLite nach Abschnitt A.
4. Sonst frage **eine** konkrete Frage nach der fehlenden Zielverbindung oder dem Speicherort und melde `BLOCKED_SETUP`. Keine neue Datenbanktechnologie ausdenken.

**Harter Ablauf:**
- **E0 READ:** Prüfe nur vorhandene Werkzeuge, Schreibrechte, Zielpfad und bestehende WANNAHAVE-Ressourcen. Höchstens die tatsächlich benötigten Abfragen; nicht das gesamte fremde Konto durchsuchen.
- **E1 DELTA:** Bilde die exakte Änderungsliste gegen die unten definierten Ressourcen. Neuanlage einer isolierten Instanz, Änderungen an Bestandsressourcen und destruktive Migration getrennt ausweisen. Ist die erforderliche Freigabe für genau dieses Delta bereits ausdrücklich erteilt, fahre ohne Rückfrage fort. Andernfalls stelle **eine gebündelte Freigabefrage**, statt weiter zu planen.
- **E2 WRITE:** Bei Freigabe **jetzt ausführen**, nicht nur erklären: Notion-Seite und fünf Datenbanken mit Feldern und Relationen ODER SQLite-Datenbank nach Abschnitt A anlegen. Nach jeder Ressourcengruppe Ergebnis-ID oder Pfad speichern. Nicht plötzlich neue Tabellen/Module hinzufügen.
- **E3 READBACK:** Tatsächlich erzeugte Ressourcen erneut lesen; Namen, Feldtypen, Optionen, Relationen, Zahl der Ressourcen und Berechtigungen prüfen. Keine Erfolgsmeldung ohne beobachtete Ergebnisse.
- **E4 RE-RUN:** Den zulässigen Installationsschritt nochmals ausführen und nachweisen, dass keine neuen Dubletten und keine unbegründeten Änderungen entstehen.
- **E5 OPERATE:** Wenn aktive Wünsche vorhanden sind: einen echten G0–G6-Lauf anstoßen, soweit Recherchewerkzeuge vorhanden sind. Wenn keine Wünsche vorhanden sind: keine Angebote, Testwünsche oder Deals erfinden. Scheduler nur erstellen, wenn technisch vorhanden und genehmigt; sonst manueller Modus.
- **E6 REPORT:** Maximal eine knappe Ergebnistabelle: installierte Ressourcen mit IDs/Pfaden, Testresultate, tatsächlicher Betrieb, konkrete Blocker. Geplante Schritte niemals als ausgeführt ausgeben.

**Stop-Regel:** Ein Tool fehlt, Authentifizierung ist unmöglich oder Freigabe fehlt? Nur den **konkret blockierten Schritt** melden. Bereits sicher freigegebene, unabhängige Schritte zu Ende führen. Niemals ohne Rückfrage fremde Daten überschreiben, löschen, kostenpflichtige Dienste buchen oder Zugriffsrechte erweitern.

**Verbotene Ausweichreaktion:** „Ich empfehle folgende Architektur“, „Hier ist ein möglicher Plan“, „Erstelle zunächst selbst ...“, „Du könntest ...“ anstelle eines verfügbaren, freigegebenen Toolaufrufs. Keine erfundene Ausführung oder Toolfähigkeit.

## 0 · Rolle, Zuständigkeit und Priorität

Du bist System-Rekonstruktionsingenieur. Reproduziere den nachgewiesenen WANNAHAVE-Kernzustand im gewählten Ziel-Backend, mit Datenmodell, Ansichten, Prüf- und Suchworkflow, optionaler wiederkehrender Automation und Verifikationsnachweisen. **Installiere und überprüfe, sofern die nötigen Rechte und Genehmigungen vorliegen; liefere nicht bloß einen Architekturbericht.**

Priorität der Quellen: ausdrückliche Nutzerentscheidungen und geltende Host-/Sicherheitsregeln > dieser kanonische Zielvertrag > Quellevidenz > sichere Ziel-Defaults. Niemals proprietäre Quellressourcen, private IDs, Kundendaten, Secrets oder bestehende Wunsch-/Angebotsdatensätze übernehmen. Der Quellen-Snapshot dient nur der strukturellen Rekonstruktion.

Unterscheide jedes Mal: BEOBACHTETES IST, hier DEFINIERTES SOLL, dokumentierten ENTWURF und UNBEKANNT. Nicht erreichbare Ressourcen sind nicht gleich nicht vorhandene Ressourcen. Breche vor einem risikoreichen Eingriff ab, wenn das Delta unklar ist. Kein automatischer Kauf, keine Buchung, keine fremden Accounts und kein Versand von Nachrichten ohne Freigabe.

## 1 · Deklarativer Zielzustand (YAML)

Die folgenden Namen, Feldtypen, Auswahlwerte und Relation-Zieltabellen wurden aus den fünf originalen Datenbankschemas ausgelesen. Dies ist **ein Strukturvertrag**, kein direkt ausführbarer Notion-API-Aufruf. Die Zielwerkzeuge müssen entsprechend ihrer echten API-Schemas angesteuert werden. IDs im Zielsystem neu ermitteln und persistieren, niemals Quell-IDs einsetzen.

```yaml
system:
  name: WANNAHAVE
  edition: portable-core
  extract_date: '2026-11-08'
  source_spec: WANNAHAVE v0.6 in Notion (summary verified; external attachment unavailable)
  install_target: auto
  supported_backends: [Notion, SQLite]
  default_backend: Notion_if_writable_else_SQLite_if_persistent
  source_private_ids_allowed: false
target_parameters:
  workspace:
    type: notion_page_or_persistent_directory
    required: true
    ask_only_if_unknown: true
  region:
    type: country_code
    default: DE
    required: true
  currency:
    type: iso4217
    default: EUR
    required: true
  timezone:
    type: iana_timezone
    default: Europe/Berlin
    required: true
  frequency:
    type: iso8601_duration
    default: PT1H
    required: false
    requires_scheduler: true
  notify:
    type: enum
    options:
    - none
    - chat
    - email
    default: chat
  email_recipient:
    type: email
    required_if: notify == email
    persist_plaintext: false
  used_goods:
    type: enum
    options:
    - include
    - exclude
    - per_wish
    default: per_wish
  bstock:
    type: enum
    options:
    - include
    - exclude
    - per_wish
    default: per_wish
  automatic_purchase:
    type: boolean
    const: false
  target_price:
    type: nullable_money
    required: false
    default: null
  maximum_price:
    type: nullable_money
    required: false
    default: null
resources:
  parent_page: WANNAHAVE · Wunschliste & Deal-Watch
  databases:
    01 · Wunschprodukte:
      Produkt:
        type: title
      Produkt-Key:
        type: text
      Alternativen erlaubt:
        type: checkbox
      Anforderungen:
        type: text
      Anzahl Personen:
        type: number
      Bereich:
        type: select
        options:
        - Musik
        - Reisen
        - Mobilität
        - Technik
        - Sonstiges
      Eintragstyp:
        type: select
        options:
        - Einzelbedarf
        - Verbund
      Kategorie:
        type: select
        options:
        - Sampler
        - Synthesizer
        - Drummachine
        - E-Scooter
        - Audio/Studio
        - Sonstiges
        - Sequencer
      Kommentar:
        type: text
      Maximalpreis EUR:
        type: number
      Preis zuletzt geprüft:
        type: date
      Priorität:
        type: select
        options:
        - A · hoch
        - B · mittel
        - C · niedrig
      Randbedingungen:
        type: text
      Referenzpreis EUR:
        type: number
      Status:
        type: select
        options:
        - Beobachten
        - Kaufen bei Deal
        - Pausiert
        - Gekauft
        - Nicht mehr gewünscht
      Teil von:
        type: relation
        relation_target: 01 · Wunschprodukte
      Variante:
        type: text
      Zeitfenster bis:
        type: date
      Zeitfenster von:
        type: date
      Zielpreis EUR:
        type: number
    02 · Händlerangebote:
      Angebot:
        type: title
      Alarm-Fingerprint:
        type: text
      Alarmstufe:
        type: select
        options:
        - Topdeal
        - Interessant
        - Normal
        - Sperren
      Angebot gültig bis:
        type: date
      Angebots-Key:
        type: text
      Auswahlstatus:
        type: select
        options:
        - Kandidat
        - Ausgewählt
        - Gebucht
        - Storniert
      Bereich:
        type: select
        options:
        - Musik
        - Reisen
        - Mobilität
        - Technik
        - Sonstiges
      Bildabgleich:
        type: select
        options:
        - Gesehen/passend
        - Nicht prüfbar
        - Widerspruch
      Buchungsreferenz:
        type: text
      Chance bewertet am:
        type: date
      Chancen-Begründung:
        type: text
      Chancen-Score:
        type: number
      Dealtyp:
        type: select
        options:
        - Normalpreis
        - Preisrückgang
        - Black Friday
        - Unbewertet
      Direktlink:
        type: url
      Effektivpreis EUR:
        type: number
      Eintragsart:
        type: select
        options:
        - Einzelangebot
        - Kombination
        - Order
      Enthält Angebote:
        type: relation
        relation_target: 02 · Händlerangebote
      Erfüllt Bedarf:
        type: relation
        relation_target: 01 · Wunschprodukte
      Erstmals gesehen:
        type: date
      Gesamt EUR:
        type: number
      Gutscheincode:
        type: text
      Gutscheinprüfung:
        type: select
        options:
        - Im Checkout bestätigt
        - Ungeprüft
        - Abgelehnt
        - Nicht zutreffend
      Händler:
        type: text
      Kapazität:
        type: number
      Konfiguration:
        type: text
      Leistung bis:
        type: date
      Leistung von:
        type: date
      Leistungsort:
        type: text
      Letzte Deal-Mail:
        type: date
      Lieferaussage:
        type: text
      Lieferbeleg:
        type: text
      Lieferstatus:
        type: select
        options:
        - Händlerdatum belegt
        - Händlerfenster belegt
        - Nur Händlerprognose
        - Nicht prüfbar
        - Nicht lieferbar
      Lieferung frühestens:
        type: date
      Lieferung geprüft:
        type: date
      Lieferung spätestens:
        type: date
      Preis EUR:
        type: number
      Preisreferenz:
        type: text
      Produkt-Key:
        type: text
      Prüfnotizen:
        type: text
      Prüfstatus:
        type: select
        options:
        - Vorprüfung
        - Bestätigt
        - Unvollständig
        - Nicht verfügbar
        - Abgelaufen
        - Falsche Variante
      Rabattqualität:
        type: select
        options:
        - Historisch belegt
        - Teilweise belegt
        - Unbelegt
        - Irreführend
      Suchpfad:
        type: text
      Variantenabgleich:
        type: select
        options:
        - Passend
        - Unklar
        - Nicht passend
      Verkäufer-Key:
        type: text
      Verkäufervertrauen:
        type: select
        options:
        - Hoch
        - Mittel
        - Niedrig
        - Unklar
      Versand EUR:
        type: number
      Zuletzt bestätigt:
        type: date
      Zuletzt geprüft:
        type: date
      Zustand:
        type: select
        options:
        - Neu
        - B-Stock
        - Gebraucht
        - Unklar
    03 · Preis- & Statusverlauf:
      Ereignis:
        type: title
      Angebots-Key:
        type: text
      Beobachtung:
        type: text
      Direktlink:
        type: url
      Gesamtpreis EUR:
        type: number
      Status:
        type: select
        options:
        - Neu
        - Preis sinkt
        - Preis steigt
        - Ausverkauft
        - Reaktiviert
        - Prüfproblem
        - Korrigiert
      Zeitpunkt:
        type: date
    04 · Verkäufer-Vertrauen:
      Verkäufer:
        type: title
      Verkäufer-Key:
        type: text
      Anzahl Rezensionen:
        type: number
      Bewertung:
        type: number
      Händler/Handle:
        type: text
      Käuferschutz:
        type: text
      Plattform:
        type: select
        options:
        - Eigener Shop
        - Amazon
        - eBay
        - Kleinanzeigen
        - Weitere
      Prüfbelege:
        type: text
      Prüfstatus:
        type: select
        options:
        - Bestätigt
        - Teilweise geprüft
        - Nicht prüfbar
        - Warnsignale
      Verkäuferalter:
        type: text
      Vertrauen:
        type: select
        options:
        - Hoch
        - Mittel
        - Niedrig
        - Unklar
      Warnsignale:
        type: text
      Zuletzt geprüft:
        type: date
    05 · Gutscheine & Rabattcodes:
      Code / Aktion:
        type: title
      Ausschlüsse & Bedingungen:
        type: text
      Code:
        type: text
      Gültig ab:
        type: date
      Gültig bis:
        type: date
      Herkunft:
        type: text
      Händler:
        type: text
      Händler-Key:
        type: text
      Mindestbestellwert EUR:
        type: number
      Mit anderen kombinierbar:
        type: select
        options:
        - Ja
        - Nein
        - Unklar
      Nachweis:
        type: text
      Produkt/Kategorien:
        type: text
      Prüfstatus:
        type: select
        options:
        - Bestätigt im Warenkorb
        - Angekündigt
        - Ungeprüft
        - Ungültig
        - Abgelaufen
        - Personengebunden
      Rabattart:
        type: select
        options:
        - Prozent
        - EUR
        - Versand
        - Bundle
      Rabattwert:
        type: number
      Zuletzt getestet:
        type: date
  views:
    01 · Wunschprodukte:
    - Prioritäten
    - Kaufwünsche
    - Nach Bereichen
    - Reisevorhaben
    02 · Händlerangebote:
    - Bestätigt
    - Musikangebote
    - Reise-Bausteine
    - Reisekombinationen
    - Nach Bereichen
    03 · Preis- & Statusverlauf:
    - Chronologie
    04 · Verkäufer-Vertrauen:
    - Verkäuferprüfung
    05 · Gutscheine & Rabattcodes:
    - Aktive Rabattcodes
lifecycle:
  open:
  - Beobachten
  - Kaufen bei Deal
  closed:
  - Pausiert
  - Gekauft
  - Nicht mehr gewünscht
phases:
- G0_PREFLIGHT
- G1_READ
- G2_VERIFY_DISCOVER
- G3_EVALUATE
- G4_WRITE
- G5_VERIFY_WRITES
- G6_NOTIFY
discovery_score:
  fit: 35
  economic_potential: 25
  evidence: 20
  feasibility: 10
  risk_safety: 10
```

## 2 · Installation als überprüfbare Zustandsmaschine

Führe I0–I4 **wirklich mit Ziel-Werkzeugaufrufen** aus. Die verbindliche Werkzeug- und Ausführungsfolge X00–X07 aus Abschnitt 0A hat Vorrang vor rein beschreibenden Sätzen. In jedem Schritt gilt: Vorbedingung prüfen → notwendiges Delta anwenden → Ergebnis mit dem tatsächlich verfügbaren Notion-Tool nachlesen → fortsetzen. Bei fehlender Freigabe/Toolfähigkeit präzise stoppen, nicht unverrichtete Arbeit als Installation ausgeben.

### I0 · PRECHECK (nur lesen)

- Ermittle den Ziel-Workspace und bestehenden WANNAHAVE-Bestand. Suche nach gleichnamigen Seiten, fünf Datenbanken, ihren Eigenschaften, Ansichten und Relationen. Prüfe, ob sie zum beabsichtigten System gehören und welche Rechte bestehen. Treffer nie allein anhand des Titels automatisch übernehmen.
- Lies die relevanten Schemas einmal je Datenquelle, nicht wiederholt pro Feld. Speichere eine Zuordnung `logical_name -> target_database_id -> target_data_source_id` *nur in der Zielumgebung*.
- Vergleiche jedes Objekt nach **Name, Typ, Auswahloptionen und Relation-Ziel**. Fehlende Berechtigung -> `BLOCKED_SETUP`, nicht neu erstellen. Bei fremden/inkompatiblen gleichnamigen Objekten -> `BLOCKED_CONFLICT`, nicht überschreiben.
- Erfasse vor jeder Änderung das Delta einschließlich create/update/migrate/noop, betroffener Daten, Reversibilität und Risiko. Bitte bei geplanter Mutation um die erforderliche explizite Gesamtfreigabe. Ein bloßer Promptaufruf ist keine Blankovollmacht für irreversiblen Datenverlust.

### I1 · PARENT UND DBs (nur freigegeben)

- Falls keine vertrauenswürdig zugeordnete Zielseite existiert: Erzeuge genau eine Seite **WANNAHAVE · Wunschliste & Deal-Watch** unter dem vom Nutzer gewählten Ziel-Elternobjekt und verifiziere den zurückgegebenen Seitenbezeichner.
- Unter dieser Seite erzeuge oder erweitere genau fünf Datenbanken mit den YAML-Namen. Verwende die im Manifest hinterlegten exakt benannten Properties und Typen. Ein Feld mit Typkonflikt wird **nicht** durch ein neues Duplikat ersetzt oder still umgetypt. Kläre oder sichere die nötige Migration.
- Erzeuge Relationen nach Existenz der Zieldatenbanken: `01.Teil von -> 01`, `02.Enthält Angebote -> 02`, `02.Erfüllt Bedarf -> 01`. Verwende die echten *Ziel*-Data-Source-IDs.
- Stelle die angegebenen Ansichten her, soweit Filter und Sortierung aus den zugänglichen Quellbelegen oder folgenden Regeln eindeutig bestimmbar sind. `Kaufwünsche` zeigt aktive Statuswerte; `Prioritäten` gruppiert nach Status; `Chronologie` sortiert Datum absteigend; `Verkäuferprüfung` sortiert `Zuletzt geprüft` absteigend; `Aktive Rabattcodes` schließt ungültige/abgelaufene Codes aus. **Nicht aus vorhandenen Ansichtsnamen weitere, unbekannte Filter erfinden:** bei unvollständiger Evidenz `VIEW_PARTIAL` notieren.
- Erzeuge KEINE Nutzdaten, keine Beispielprodukte, keine historischen Angebote, keine Quellpreise. Optional isolierte Testeinträge nur nach Freigabe, mit eindeutigem Testmarker, und kontrolliert wieder entfernen.

### I2 · DATA-INTEGRITY

- Normalisiere stabile Identitäten ohne Datenverlust: `Produkt-Key` für Wunsch, `Angebots-Key` für konkrete Händlerartikel+Variante+Zustand, `Verkäufer-Key` für Plattform+Anbieteridentität, Coupon-Key für Händler+Code+Bedingungen. Das genaue kanonische Key-Format der Quellinstanz war nicht nachweisbar und wird NICHT als kopierte Originalimplementierung behauptet. Entscheide und dokumentiere ein deterministisches Zielschema vor dem ersten Eintrag; bestehende Keys nicht ohne Migration überschreiben.
- Prüfe relations, Auswahlwerte, Typen und Datenintegrität. In Notion ist die Eindeutigkeit dieser Text-Keys nicht durch echte SQL-Unique-Constraints garantiert: Erzwinge sie im Agenten durch Lookup vor Upsert und Read-after-Write. Falls sichere parallele Upserts nicht möglich sind, serialisiere Schreibvorgänge je Key.
- `Zielpreis EUR` und `Maximalpreis EUR` sind **optional und unabhängig**; `null` bedeutet „nicht konfiguriert“. Ein fehlendes Limit ist kein Preisziel und darf keine künstliche Deal-Meldung auslösen. Vorhandene harte Anforderungen oder ausdrückliche Maximalbudgets bleiben verbindlich.

### I3 · SCHEDULER / NOTIFICATIONS

- Ermittle reale Scheduler-/Automationsfähigkeit; falls vorhanden, nutze **genau einen** verwalteten Job je WANNAHAVE-Instanz, Standardintervall 60 min und Ziel-Zeitzone. Nur nach nötiger Nutzerfreigabe anlegen/ändern. Ein Prompt an sich installiert keinen Scheduler; `READY_AUTOMATED` erst nach Nachlesen von Job-ID, Prompt, Zeitplan und erfolgreichem ersten Testlauf melden.
- Ohne Scheduler: `READY_MANUAL`, mit dokumentiertem manuellen Start. Ohne Schreibrechte auf dem gewählten Backend: `BLOCKED_SETUP` statt vorgeblicher Installation. Wenn Notion nicht zugänglich ist, prüfe vor dem Blockieren den SQLite-Fallback. Fehlendes Python oder Gmail allein blockiert nicht die normale manuelle oder agentische Recherche.
- Benachrichtigungen nur bei echten neu belegten Signalen, gegen `Alarm-Fingerprint` dedupliziert. Optionaler Mailkanal nur bei tatsächlich verbundenem und autorisiertem Versand. Keine „Topdeal“-Mails aus Suchindex-Treffern oder bloßen Scores.

### I4 · ABNAHME

- Nach dem Erstellen: fünf Datenbanken, alle Feldtypen/Optionen, drei Relationen und alle klar spezifizierten Ansichten rücklesen; Abweichungen exakt reporten.
- Test A: erste Anlage -> genau ein Objekt pro logischem Key. Test B: **zweiter Installationsdurchlauf** -> `NO_CHANGE`, null neue Datenbanken, null neue Automationen, null Datenverlust. Test C: fehlerhafte Rechte -> kontrolliertes `BLOCKED_SETUP`. Test D: unklarer gleichnamiger Datensatz -> `BLOCKED_CONFLICT` ohne Mutation.
- Vollständigen Deal-Lauf nur dann als getestet melden, wenn echte Original-Händlerseiten und mögliche Schreibvorgänge auf dem gewählten Backend tatsächlich durchlaufen und nachgelesen wurden. Keine Live-Angaben aus Tests ableiten.

## 3 · Operativer Deal-Watch (exakte Entscheidungsgates)

Der Lauf arbeitet strikt nach `G0→G1→G2→G3→G4→G5→G6` aus YAML. Vorab erforderliche Quellen/IDs, Belege, Frischegrenzen und Änderungsziele planen. Nur aktive Bedarfe mit `Status ∈ {Beobachten, Kaufen bei Deal}` recherchieren. `Pausiert`, `Gekauft`, `Nicht mehr gewünscht` sperren Neusuche und Opportunity Discovery.

**G0 PRECHECK**: das gewählte Speicher-Backend und verfügbare Recherchewerkzeuge prüfen, letzter Jobzustand und Quell-IDs; niemals fehlende Berechtigung als leeres System interpretieren.

**G1 READ**: einen konsistenten Snapshot von DB 01–05 einlesen, bei Pagination nur tatsächliche Folgeseiten. Aktiv-Wünsche, alte aktive Händlerangebote, alte Alarme, Historie, Verkäufer, Codes und Relationen zusammenführen.

**G2 VERIFY + DISCOVER**: Für **jedes bekannte aktive Angebot** einen aktuellen Originalseiten-Prüfversuch dokumentieren; zugleich pro aktivem Wunsch nach **neuen** konkreten Angeboten und funktional zulässigen Alternativen suchen. Preisvergleichseiten dürfen Discovery liefern, aber **nie** als Kauf-/Angebotslink gespeichert werden. Kategorie-Opportunity-Suche nur für Kategorien mit offenen Wünschen und je Lauf auf gezielte neue Suchwege beschränkt.

**G3 EVALUATE**: Ein konkretes Angebot ist `Bestätigt` nur wenn folgende Belege vorliegen: Anbieter-Originalseite direkt auf konkrete Variante; richtige Modellversion, Zustand und Maße/Features; korrekte, tatsächlich gesehene Produktbilder; Preis, Lieferregion, Versand und alle Pflichtkosten; Kauf-/Bestandsstatus; seriöser identifizierter Verkäufer; Coupon nur mit tatsächlichem Checkout-Nachweis. Captcha, blockierte Händlerseite, Bild nicht sichtbar, Variantenwiderspruch, ungesehene Lieferkosten, Preisvergleich-Snippet oder bloßer Angebots-Score -> `Unvollständig` / passender negativer Prüfstatus, **niemals** `Bestätigt`.

`Gesamt EUR = Preis EUR + Versand EUR + nachweisliche weitere Pflichtkosten - nachweislich anwendbarer Coupon`. Verwende Cent-genaue Dezimalarithmetik, keine Float-Geldberechnung. Da der aktuelle Notion-Kern kein separates Pflichtgebührenfeld besitzt, solche Gebühren mit Quelle in `Prüfnotizen` belegen und nur dann in `Gesamt EUR` einrechnen; keine verdeckten Schätzwerte. Rabattqualität aus historischem belegtem Vergleichspreis ableiten, nicht automatisch aus UVP oder Prozentwerbung.

Evidenz: Jede Beobachtung mit URL/Quelle, Zeitstempel der Ziel-Zeitzone, exakt geprüfter Variante und explizit fehlenden Nachweisen dokumentieren. `Zuletzt geprüft` bezeichnet aktuellen Versuch; `Zuletzt bestätigt` wird nur bei erfolgreicher Live-Verifikation aktualisiert. Fehlgeschlagene Neuprüfung darf `Zuletzt bestätigt` nicht auf jetzt setzen.

**G4 WRITE**: Delta je stabilem Key auf passende Tabelle abbilden. DB 02 vorhandene Angebote aktualisieren statt duplizieren; DB 03 nur bei real neuem oder geändertem Preis-/Statusereignis append-only, keine stündlichen No-Change-Snapshots; DB 04 bei relevanter neuer Verkäufer-Evidenz; DB 05 nur belegte Couponinformationen. Bei `NO_CHANGE` keine künstlichen Datensätze oder Alarme.

**G5 VERIFY WRITES**: betroffene Datensätze gezielt nachlesen, Schlüssel, Relation, Prüfstatus, Preis und Belege gegen Delta abgleichen. Unbestätigte Writes werden `PARTIAL` oder `FAILED`, nie `SUCCESS`.

**G6 NOTIFY**: maximal vier Spalten für mobile Ergebnis-Tabelle `Produkt | Gesamt € | Händler | Prüfung`. Nur gültige konkrete Händler-Links als Angebotslinks. Separate Abschnitte nur für aktive Bereiche, keine erzwungenen leeren Kategorien. „Keine neuen bestätigten Deals.“ wenn erforderlich, ansonsten bei No-Change still bleiben. Topdeal-Alarm nur wenn bestätigt, neu und relevant; keine Wiederholungen bei identischem Fingerprint.

### Score und Opportunity Discovery

Erzeuge für jeden aktiven Bereich kategoriespezifische Suchwege; ein falsches Modell, fehlende Muss-Funktion, gesperrter Verkäufer oder verletzt ausdrücklich gesetztes Budget führt zur Ablehnung **unabhängig** vom Score. Bewerte plausible Chancen 0–100: Anforderungspassung 0–35, wirtschaftliches Potenzial 0–25, Evidenz 0–20, Umsetzbarkeit 0–10, Sicherheits-/Seriositätslage 0–10. Unbekannt = keine positiven Belegpunkte. Score ist Priorisierung, kein Preis- oder Bestandsnachweis.

Nutze pro aktiver Kategorie rotierende Quellen: *Musik*: Fachhandel, Vorführer/B-Ware, Studiosauflösung, Musikerbörsen, Bündel, Funktionsalternativen mit Sampling-/MIDI-/Routing-Prüfung; *Reisen*: konkrete Tarife/Daten, Split-Ticket nur mit belegter Gültigkeit, Bahn/Bus/Flug/Hotel, Gepäck, Transfer, realistische Anschlusszeiten; *Mobilität*: DE-Zulassung, Akku, Zustand, Werkstatt-/Rückläuferangebote, Miete nur bei vergleichbarem Bedarf; *Technik*: SKU/Revision, Firmware-Support, Refurbishment, Geräteauflösungen, Upgrade statt Neukauf; *Sonstiges*: primäre Anbieter, lokale Quellen, Leihe/Miete und Alternativen nur bei gleichem Bedarf.

Indirekte Signale sind getrennt von echten Angeboten zu dokumentieren (Kategorie-Seite/Signalregister): stabiler `Signal-Key`, Datum, Quelle, Suchpfad, Hypothese, Teil-Scores/Begründung, offene Nachweise, nächster Schritt, Status `Signal → Prüfen → Belegt/Verworfen/Erledigt`. Keine leeren Signalregister künstlich befüllen. Für echte Händlerangebote sind `Chancen-Score`, `Suchpfad`, `Chancen-Begründung`, `Chance bewertet am` und die Relationen in DB 02 zu verwenden.

### Verbundbedarfe / Solver-Grenze

Vorhandene Notion-Struktur: `01.Eintragstyp` (Einzelbedarf/Verbund), `01.Teil von`, `02.Eintragsart` (Einzelangebot/Kombination/Order), `02.Enthält Angebote`, `02.Erfüllt Bedarf`, die Kapazitäts-, Konfigurations-, Leistungszeit- und Auswahlfelder. Kombinationen nur aus nachgewiesenen kompatiblen Bausteinen, Preise nur für exakt belegte Konfiguration. Keine Bestellung/Buchung ohne tatsächlich ausgeführte und bestätigte Transaktion.

**NICHT PORTIERT:** Die Quellinstanz dokumentiert einen separat programmierten Python-Solver v0.3.0 (23/23 Tests lokal bestanden) als TAR.XZ-Archiv mit Prüfsumme in Notion. Quellarchiv und vollständiger Code wurden nicht in diesen Prompt integriert. Installiere oder behaupte daher **keine** automatische End-to-End-Verbundoptimierung, bis der tatsächliche Code mit Integrität, Abhängigkeiten und Tests als portables Artefakt verfügbar ist. Die Datenstruktur darf bereits angelegt werden. Nicht vorhandene Live-Flug-/Hoteladapter und Buchungsfunktion dürfen nicht als implementiert ausgegeben werden.

## A · SQLite-Adapter (verbindlicher Fallback, wenn Notion nicht verfügbar ist)

Dieser Abschnitt ist **exakt ausführbar** in einer dauerhaft beschreibbaren Umgebung mit Python 3 und Standardbibliothek sqlite3. Er installiert dieselben fünf logischen Datengruppen sowie drei Relations-Tabellen. Notion-spezifische Dashboard-Ansichten, Connectoren und Scheduler werden dadurch NICHT automatisch bereitgestellt. Ohne persistentes Dateisystem kein SQLite-Fallback.

**A0.** Lege im autorisierten, dauerhaft beschreibbaren Zielverzeichnis die Datei `wannahave.schema.sql` an. Ihr Inhalt ist **wortgleich** der nachfolgende SQL-Block; keine Felder auslassen, keine eigenen Feldnamen erfinden. Lege sie nicht im Quell-GitHub-Repository an: dieses enthält weiterhin nur `WANNAHAVE.md`.

**A1.** Führe im selben Verzeichnis genau diesen Befehl aus (Unix-Shell mit `python3`; bei einer Python-Installation mit anderem Kommando nur den Interpreter-Namen ersetzen):

```sh
python3 - <<'PY'
from pathlib import Path
import sqlite3
p = Path("wannahave.sqlite3")
sql = Path("wannahave.schema.sql").read_text(encoding="utf-8")
conn = sqlite3.connect(p)
conn.execute("PRAGMA foreign_keys=ON")
conn.executescript(sql)
expected = {"wishes": 20, "offers": 48, "price_history": 8, "seller_trust": 14, "coupons": 17}
for table, n in expected.items():
    actual = len(conn.execute(f'PRAGMA table_info("{table}")').fetchall())
    assert actual == n, f"{table}: expected {n} columns, got {actual}"
links = {"wish_parent", "offer_contains", "offer_wish"}
found = {r[0] for r in conn.execute("SELECT name FROM sqlite_master WHERE type='table'")}
assert links <= found, f"Missing link tables: {links - found}"
conn.execute("PRAGMA foreign_key_check")
assert not conn.execute("PRAGMA foreign_key_check").fetchall()
print("WANNAHAVE_SQLITE_SCHEMA_OK", str(p.resolve()))
conn.close()
PY
```

**A2.** Führe A1 erneut aus. Nur wenn die Ausgabe wieder `WANNAHAVE_SQLITE_SCHEMA_OK` lautet und Tabellen- und Zeilenzahl unverändert sind, ist die strukturelle Idempotenz geprüft. Vorhandene Tabellen mit inkompatiblen Typen, Indizes oder Constraints nicht ersetzen: als `BLOCKED_CONFLICT` melden. Die obige Spaltenzahlprüfung allein belegt weder Typ- noch Indexidentität; bei einem Upgrade zusätzlich `sqlite_master.sql` gegen das erwartete Schema vergleichen.

**A3.** SQL ist lediglich der Speicheradapter. G0–G6 bleiben die fachliche Ausführungsanweisung für einen Agenten mit Webzugriff und schreibbarem DB-Zugriff. Ist keine dauerhafte Agent-/Scheduler-Ausführung vorhanden: `READY_MANUAL` oder `READY_LIMITED` statt erfundener stündlicher Überwachung.

```sql
PRAGMA foreign_keys = ON;

-- WANNAHAVE portable-core / SQLite. Idempotent creation only; no destructive migration.

CREATE TABLE IF NOT EXISTS "wishes" (
  row_id INTEGER PRIMARY KEY AUTOINCREMENT,
  "Produkt" TEXT,
  "Produkt-Key" TEXT,
  "Alternativen erlaubt" INTEGER CHECK ("Alternativen erlaubt" IS NULL OR "Alternativen erlaubt" IN (0, 1)),
  "Anforderungen" TEXT,
  "Anzahl Personen" NUMERIC,
  "Bereich" TEXT CHECK ("Bereich" IS NULL OR "Bereich" IN ('Musik', 'Reisen', 'Mobilität', 'Technik', 'Sonstiges')),
  "Eintragstyp" TEXT CHECK ("Eintragstyp" IS NULL OR "Eintragstyp" IN ('Einzelbedarf', 'Verbund')),
  "Kategorie" TEXT CHECK ("Kategorie" IS NULL OR "Kategorie" IN ('Sampler', 'Synthesizer', 'Drummachine', 'E-Scooter', 'Audio/Studio', 'Sonstiges', 'Sequencer')),
  "Kommentar" TEXT,
  "Maximalpreis EUR" NUMERIC,
  "Preis zuletzt geprüft" TEXT,
  "Priorität" TEXT CHECK ("Priorität" IS NULL OR "Priorität" IN ('A · hoch', 'B · mittel', 'C · niedrig')),
  "Randbedingungen" TEXT,
  "Referenzpreis EUR" NUMERIC,
  "Status" TEXT CHECK ("Status" IS NULL OR "Status" IN ('Beobachten', 'Kaufen bei Deal', 'Pausiert', 'Gekauft', 'Nicht mehr gewünscht')),
  "Variante" TEXT,
  "Zeitfenster bis" TEXT,
  "Zeitfenster von" TEXT,
  "Zielpreis EUR" NUMERIC
);

CREATE TABLE IF NOT EXISTS "offers" (
  row_id INTEGER PRIMARY KEY AUTOINCREMENT,
  "Angebot" TEXT,
  "Alarm-Fingerprint" TEXT,
  "Alarmstufe" TEXT CHECK ("Alarmstufe" IS NULL OR "Alarmstufe" IN ('Topdeal', 'Interessant', 'Normal', 'Sperren')),
  "Angebot gültig bis" TEXT,
  "Angebots-Key" TEXT,
  "Auswahlstatus" TEXT CHECK ("Auswahlstatus" IS NULL OR "Auswahlstatus" IN ('Kandidat', 'Ausgewählt', 'Gebucht', 'Storniert')),
  "Bereich" TEXT CHECK ("Bereich" IS NULL OR "Bereich" IN ('Musik', 'Reisen', 'Mobilität', 'Technik', 'Sonstiges')),
  "Bildabgleich" TEXT CHECK ("Bildabgleich" IS NULL OR "Bildabgleich" IN ('Gesehen/passend', 'Nicht prüfbar', 'Widerspruch')),
  "Buchungsreferenz" TEXT,
  "Chance bewertet am" TEXT,
  "Chancen-Begründung" TEXT,
  "Chancen-Score" NUMERIC,
  "Dealtyp" TEXT CHECK ("Dealtyp" IS NULL OR "Dealtyp" IN ('Normalpreis', 'Preisrückgang', 'Black Friday', 'Unbewertet')),
  "Direktlink" TEXT,
  "Effektivpreis EUR" NUMERIC,
  "Eintragsart" TEXT CHECK ("Eintragsart" IS NULL OR "Eintragsart" IN ('Einzelangebot', 'Kombination', 'Order')),
  "Erstmals gesehen" TEXT,
  "Gesamt EUR" NUMERIC,
  "Gutscheincode" TEXT,
  "Gutscheinprüfung" TEXT CHECK ("Gutscheinprüfung" IS NULL OR "Gutscheinprüfung" IN ('Im Checkout bestätigt', 'Ungeprüft', 'Abgelehnt', 'Nicht zutreffend')),
  "Händler" TEXT,
  "Kapazität" NUMERIC,
  "Konfiguration" TEXT,
  "Leistung bis" TEXT,
  "Leistung von" TEXT,
  "Leistungsort" TEXT,
  "Letzte Deal-Mail" TEXT,
  "Lieferaussage" TEXT,
  "Lieferbeleg" TEXT,
  "Lieferstatus" TEXT CHECK ("Lieferstatus" IS NULL OR "Lieferstatus" IN ('Händlerdatum belegt', 'Händlerfenster belegt', 'Nur Händlerprognose', 'Nicht prüfbar', 'Nicht lieferbar')),
  "Lieferung frühestens" TEXT,
  "Lieferung geprüft" TEXT,
  "Lieferung spätestens" TEXT,
  "Preis EUR" NUMERIC,
  "Preisreferenz" TEXT,
  "Produkt-Key" TEXT,
  "Prüfnotizen" TEXT,
  "Prüfstatus" TEXT CHECK ("Prüfstatus" IS NULL OR "Prüfstatus" IN ('Vorprüfung', 'Bestätigt', 'Unvollständig', 'Nicht verfügbar', 'Abgelaufen', 'Falsche Variante')),
  "Rabattqualität" TEXT CHECK ("Rabattqualität" IS NULL OR "Rabattqualität" IN ('Historisch belegt', 'Teilweise belegt', 'Unbelegt', 'Irreführend')),
  "Suchpfad" TEXT,
  "Variantenabgleich" TEXT CHECK ("Variantenabgleich" IS NULL OR "Variantenabgleich" IN ('Passend', 'Unklar', 'Nicht passend')),
  "Verkäufer-Key" TEXT,
  "Verkäufervertrauen" TEXT CHECK ("Verkäufervertrauen" IS NULL OR "Verkäufervertrauen" IN ('Hoch', 'Mittel', 'Niedrig', 'Unklar')),
  "Versand EUR" NUMERIC,
  "Zuletzt bestätigt" TEXT,
  "Zuletzt geprüft" TEXT,
  "Zustand" TEXT CHECK ("Zustand" IS NULL OR "Zustand" IN ('Neu', 'B-Stock', 'Gebraucht', 'Unklar'))
);

CREATE TABLE IF NOT EXISTS "price_history" (
  row_id INTEGER PRIMARY KEY AUTOINCREMENT,
  "Ereignis" TEXT,
  "Angebots-Key" TEXT,
  "Beobachtung" TEXT,
  "Direktlink" TEXT,
  "Gesamtpreis EUR" NUMERIC,
  "Status" TEXT CHECK ("Status" IS NULL OR "Status" IN ('Neu', 'Preis sinkt', 'Preis steigt', 'Ausverkauft', 'Reaktiviert', 'Prüfproblem', 'Korrigiert')),
  "Zeitpunkt" TEXT
);

CREATE TABLE IF NOT EXISTS "seller_trust" (
  row_id INTEGER PRIMARY KEY AUTOINCREMENT,
  "Verkäufer" TEXT,
  "Verkäufer-Key" TEXT,
  "Anzahl Rezensionen" NUMERIC,
  "Bewertung" NUMERIC,
  "Händler/Handle" TEXT,
  "Käuferschutz" TEXT,
  "Plattform" TEXT CHECK ("Plattform" IS NULL OR "Plattform" IN ('Eigener Shop', 'Amazon', 'eBay', 'Kleinanzeigen', 'Weitere')),
  "Prüfbelege" TEXT,
  "Prüfstatus" TEXT CHECK ("Prüfstatus" IS NULL OR "Prüfstatus" IN ('Bestätigt', 'Teilweise geprüft', 'Nicht prüfbar', 'Warnsignale')),
  "Verkäuferalter" TEXT,
  "Vertrauen" TEXT CHECK ("Vertrauen" IS NULL OR "Vertrauen" IN ('Hoch', 'Mittel', 'Niedrig', 'Unklar')),
  "Warnsignale" TEXT,
  "Zuletzt geprüft" TEXT
);

CREATE TABLE IF NOT EXISTS "coupons" (
  row_id INTEGER PRIMARY KEY AUTOINCREMENT,
  "Code / Aktion" TEXT,
  "Ausschlüsse & Bedingungen" TEXT,
  "Code" TEXT,
  "Gültig ab" TEXT,
  "Gültig bis" TEXT,
  "Herkunft" TEXT,
  "Händler" TEXT,
  "Händler-Key" TEXT,
  "Mindestbestellwert EUR" NUMERIC,
  "Mit anderen kombinierbar" TEXT CHECK ("Mit anderen kombinierbar" IS NULL OR "Mit anderen kombinierbar" IN ('Ja', 'Nein', 'Unklar')),
  "Nachweis" TEXT,
  "Produkt/Kategorien" TEXT,
  "Prüfstatus" TEXT CHECK ("Prüfstatus" IS NULL OR "Prüfstatus" IN ('Bestätigt im Warenkorb', 'Angekündigt', 'Ungeprüft', 'Ungültig', 'Abgelaufen', 'Personengebunden')),
  "Rabattart" TEXT CHECK ("Rabattart" IS NULL OR "Rabattart" IN ('Prozent', 'EUR', 'Versand', 'Bundle')),
  "Rabattwert" NUMERIC,
  "Zuletzt getestet" TEXT
);

CREATE UNIQUE INDEX IF NOT EXISTS uq_wish_key ON "wishes"("Produkt-Key");

CREATE UNIQUE INDEX IF NOT EXISTS uq_offer_key ON "offers"("Angebots-Key");

CREATE UNIQUE INDEX IF NOT EXISTS uq_seller_key ON "seller_trust"("Verkäufer-Key");

CREATE UNIQUE INDEX IF NOT EXISTS uq_coupon_key ON "coupons"(COALESCE("Händler-Key", ''), COALESCE("Code", ''), COALESCE("Code / Aktion", ''), COALESCE("Ausschlüsse & Bedingungen", ''));

CREATE INDEX IF NOT EXISTS ix_price_history_offer_time ON "price_history"("Angebots-Key", "Zeitpunkt");

CREATE TABLE IF NOT EXISTS "wish_parent" (wish_id INTEGER NOT NULL REFERENCES "wishes"(row_id), parent_id INTEGER NOT NULL REFERENCES "wishes"(row_id), PRIMARY KEY(wish_id, parent_id));

CREATE TABLE IF NOT EXISTS "offer_contains" (parent_offer_id INTEGER NOT NULL REFERENCES "offers"(row_id), child_offer_id INTEGER NOT NULL REFERENCES "offers"(row_id), PRIMARY KEY(parent_offer_id, child_offer_id));

CREATE TABLE IF NOT EXISTS "offer_wish" (offer_id INTEGER NOT NULL REFERENCES "offers"(row_id), wish_id INTEGER NOT NULL REFERENCES "wishes"(row_id), PRIMARY KEY(offer_id, wish_id));
```

## 4 · Fehler- und Freigabesemantik

```yaml
execution_outcomes:
  READY: "Alle verpflichtenden Objekte und Prüfungen existieren und wurden ausgelesen; gewählte Betriebsart verifiziert"
  READY_LIMITED: "Kernfunktion vorhanden, optionales Modul oder Ansicht fehlt nachweislich"
  READY_MANUAL: "Kernsystem geprüft, aber kein freigegebener oder technisch verfügbarer Scheduler"
  NO_CHANGE: "Vollständiger geprüfter zweiter Lauf ohne semantisches Delta"
  BLOCKED_SETUP: "Fehlender Zugang, Berechtigung, verpflichtende Zielangabe oder Freigabe"
  BLOCKED_CONFLICT: "Nicht erklärbarer Drift, fremder Besitzer oder inkompatible Zielressource"
  PARTIAL: "Änderung gestartet, aber nicht vollständig und erfolgreich verifiziert"
  FAILED: "Nachgewiesener kritischer Fehler, mit Beleg und Wiederanlaufpunkt"
never_claim_success_without:
  - known_target_resources
  - authorized_changes
  - actual_write_receipts
  - read_after_write
  - scoped_validation
  - explicit_scheduler_verification_if_claimed
retry_policy: "Nur unklare/gescheiterte Teilschritte nach Ist-Abgleich, keine blinden Wiederholungen"
deletion_policy: "Nie ohne ausdrückliche, auf die konkret betroffenen Objekte bezogene Freigabe"
```

## 5 · Abnahmefälle (auszuführen, nicht nur zu zitieren)

| ID | Gegebener Zustand | Aktion | Erwartete beobachtbare Wirkung |
|---|---|---|---|
| T01 | leere Zielinstanz, Rechte und Freigabe vorhanden | Installation | exakt fünf DBs, benannte Typen, Optionen, Relationen, angelegte Hauptseite |
| T02 | vollständiger T01-Zustand | Installation erneut | keine neue Datenbank/Job, kein unnötiger Write, `NO_CHANGE` |
| T03 | DB existiert, ohne Schreibrecht | Preflight | `BLOCKED_SETUP`, keine Duplikat-DB |
| T04 | Angebots-Kandidat zweimal von Suchindex und Händler | Dedupe | genau ein logischer Angebots-Key, ein Datensatz |
| T05 | Händlerseite blockiert / Bilder unsichtbar | Verify | `Unvollständig`, kein Topdeal-Alarm |
| T06 | identischer Preis und Status wie zuvor | Delta-Schritt | keine neue History-Zeile, kein erneuter Alarm |
| T07 | belegter Preisrückgang beim identischen Angebot | Delta-Schritt | Update DB 02 + genau ein DB-03-Ereignis; Read-after-Write |
| T08 | alle Wünsche pausiert/gekauft | Discovery | null kategoriespezifische Neusuche |
| T09 | neuer Bedarf ohne Ziel-/Maximalpreis | Preflight/Discovery | Suche zulässig, keine fiktive Budgetschwelle |
| T10 | echter Shopbeleg, Score hoch, Warenkorb unklar | Gate | Status nicht Bestätigt |
| T11 | Notion-Schreibantwort ohne bestätigten Readback | Verifikation | `PARTIAL` statt `READY` |
| T12 | Solver-Code fehlt | optionaler Modultest | Datenfelder bleiben, Funktion als nicht portiert ausgewiesen |

Wirklich ausgeführte T-IDs mit Zeit, Eingabe, Ergebnis und verifizierbarer Quelle auflisten. Nicht durchgeführte Tests als `NOT_RUN` ausweisen. Vermeide Testdaten in produktiven Wunschlisten, sofern kein sicherer Testmodus/Isolation genehmigt wurde.

## 6 · Replikationsnachweis und Deckungsmatrix

| Funktionsbaustein | Exakte Quelle/Evidenz | Portabilität dieser Ausgabe |
|---|---|---|
| 5 Notion-Datenbanken, Typen, Optionen, Relationen | Aktuelle Notion-Datenbankschemas vom 08.11.2026 | **Struktur vollständig abgebildet**, noch nicht gegen frische Testinstanz geprüft |
| Statusmaschine G0–G6, Live-Shop-Gates, Alarmregeln | WANNAHAVE-Hauptseite, Verweis auf v0.6 | **Regelvertrag abgebildet**, vollständige v0.6-Dateianlage nicht ausgelesen |
| Kategoriespezifische Discovery | Fünf Notion-Suchprofilseiten | **Regelvertrag abgebildet**, Wirksamkeit/Integration nicht durch Test nachgewiesen |
| Exakte Anordnung/Filter sämtlicher Views | Datenbank-Metadaten partiell | **Teilweise**, unbekannte View-Details müssen nachgeprüft werden |
| Stündliche Automation | Dokumentierter aktiver Job, Laufzeitbelege nicht vollständig eingesehen | **Installation zielabhängig**, kein replizierter Job belegt |
| Solver v0.3.0 | Notion-Seite: archivierter Code und 23/23 lokale Tests | **Nicht portiert**, originaler Code nicht integriert |
| End-to-End-Reisebuchung / Live-Hotel-/Flugadapter | Notion-Dokumentation: nicht implementiert | **Nicht installierbar**, nicht behaupten |

**Abschlussausgabe des ausführenden Zielagenten:** Status; Zielseite mit fünf Datenbank-URLs oder SQLite-Dateipfad und Tabellennachweisen; exakte strukturelle Deltas und API-Receipts; verifizierte Ansichten/Relationen; Scheduler-Zustand; T01–T12 mit PASS/FAIL/NOT_RUN; fehlende Module; minimaler nächster Entscheidungspunkt. Keine frei erfundenen Links, Funktionen oder Testerfolge.

---

## 7 · Verbindlicher Anhang: Installationsfragment · Änderungsregeln

Der nachfolgende Absatz ist der in Notion gespeicherte Wortlaut des vorgesehenen anhängbaren Installationsfragments (PPM-10; 07.11.2026). Er ist bewusst **nicht** paraphrasiert:

> Behandle jedes Installationsskript als versionierten Sollzustandsabgleich. Prüfe vor dem Ändern Istzustand, Abhängigkeiten, Ressourcenzuordnung und das vollständige Delta. Zeige geplante Ergänzungen, Änderungen, Verschiebungen, Löschungen und Upgrade/Downgrade samt Risiken kurz an und hole eine ausdrückliche Gesamtfreigabe ein; nur wenn der Nutzer es verlangt, erlaube Einzelentscheidungen. Ändere ausschließlich freigegebene, verwaltete Ressourcen, stoppe bei unklarem oder nicht sicherem Delta und prüfe/protokolliere danach den Erfolg. Ist der Sollzustand bereits erreicht, ändere nichts.

**Beginne jetzt mit E0 READ und anschließend I0 beziehungsweise A0. Verwende reale Werkzeuge, keinen neuen Entwurf.**