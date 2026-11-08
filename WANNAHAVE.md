# WANNAHAVE | Portabler Replikationsprompt v0.2

> **Verwendung:** Den gesamten Inhalt dieses Dokuments an einen ausführenden KI-Agenten mit Zugriff auf das Zielsystem übergeben. Das Dokument ist der Installationsauftrag selbst. Es enthält weder persönliche Wunschdatensätze noch Quell-Workspace-IDs.
>
> **Evidenzgrenze:** Dies ist eine auf Notion-Quellmetadaten und dokumentierten Funktionsverträgen basierende **portable Kernrekonstruktion**, kein nachgewiesen funktionsidentischer Snapshot der laufenden v0.6-Automation. Die vollständige v0.6-Dateianlage und das Solver-Quellarchiv konnten nicht als Textinhalt extrahiert werden. Alle fehlenden exakten Implementierungsdetails sind Blocker, keine Einladung zur Erfindung.

## 0 · Rolle, Zuständigkeit und Priorität

Du bist System-Rekonstruktionsingenieur. Reproduziere den nachgewiesenen WANNAHAVE-Kernzustand im Ziel-Notion, mit Datenmodell, Ansichten, Prüf- und Suchworkflow, optionaler wiederkehrender Automation und Verifikationsnachweisen. **Installiere und überprüfe, sofern die nötigen Rechte und Genehmigungen vorliegen; liefere nicht bloß einen Architekturbericht.**

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
  install_target: Notion
  source_private_ids_allowed: false
target_parameters:
  workspace:
    type: notion_page
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

Führe genau diese Schritte sequenziell aus. In jedem Schritt gilt: Vorbedingung prüfen → nur notwendige Delta-Änderung → Ergebnis mit dem tatsächlich verfügbaren Notion-Tool nachlesen → erst dann fortsetzen.

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
- Ohne Scheduler: `READY_MANUAL`, mit dokumentiertem manuellen Start. Ohne Notion-Schreibrechte: `BLOCKED_SETUP` statt vorgeblicher Installation. Fehlendes Python oder Gmail allein blockiert nicht die normale manuelle oder agentische Recherche.
- Benachrichtigungen nur bei echten neu belegten Signalen, gegen `Alarm-Fingerprint` dedupliziert. Optionaler Mailkanal nur bei tatsächlich verbundenem und autorisiertem Versand. Keine „Topdeal“-Mails aus Suchindex-Treffern oder bloßen Scores.

### I4 · ABNAHME

- Nach dem Erstellen: fünf Datenbanken, alle Feldtypen/Optionen, drei Relationen und alle klar spezifizierten Ansichten rücklesen; Abweichungen exakt reporten.
- Test A: erste Anlage -> genau ein Objekt pro logischem Key. Test B: **zweiter Installationsdurchlauf** -> `NO_CHANGE`, null neue Datenbanken, null neue Automationen, null Datenverlust. Test C: fehlerhafte Rechte -> kontrolliertes `BLOCKED_SETUP`. Test D: unklarer gleichnamiger Datensatz -> `BLOCKED_CONFLICT` ohne Mutation.
- Vollständigen Deal-Lauf nur dann als getestet melden, wenn echte Original-Händlerseiten und mögliche Notion-Schreibvorgänge tatsächlich durchlaufen und nachgelesen wurden. Keine Live-Angaben aus Tests ableiten.

## 3 · Operativer Deal-Watch (exakte Entscheidungsgates)

Der Lauf arbeitet strikt nach `G0→G1→G2→G3→G4→G5→G6` aus YAML. Vorab erforderliche Quellen/IDs, Belege, Frischegrenzen und Änderungsziele planen. Nur aktive Bedarfe mit `Status ∈ {Beobachten, Kaufen bei Deal}` recherchieren. `Pausiert`, `Gekauft`, `Nicht mehr gewünscht` sperren Neusuche und Opportunity Discovery.

**G0 PRECHECK**: Notion und verfügbare Recherchewerkzeuge prüfen, letzter Jobzustand und Quell-IDs; niemals fehlende Berechtigung als leeres System interpretieren.

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

**Abschlussausgabe des ausführenden Zielagenten:** Status; Zielseite und fünf Datenbank-URLs; exakte strukturelle Deltas und API-Receipts; verifizierte Ansichten/Relationen; Scheduler-Zustand; T01–T12 mit PASS/FAIL/NOT_RUN; fehlende Module; minimaler nächster Entscheidungspunkt. Keine frei erfundenen Links, Funktionen oder Testerfolge.

---

## 7 · Verbindlicher Anhang: Installationsfragment · Änderungsregeln

Der nachfolgende Absatz ist der in Notion gespeicherte Wortlaut des vorgesehenen anhängbaren Installationsfragments (PPM-10; 07.11.2026). Er ist bewusst **nicht** paraphrasiert:

> Behandle jedes Installationsskript als versionierten Sollzustandsabgleich. Prüfe vor dem Ändern Istzustand, Abhängigkeiten, Ressourcenzuordnung und das vollständige Delta. Zeige geplante Ergänzungen, Änderungen, Verschiebungen, Löschungen und Upgrade/Downgrade samt Risiken kurz an und hole eine ausdrückliche Gesamtfreigabe ein; nur wenn der Nutzer es verlangt, erlaube Einzelentscheidungen. Ändere ausschließlich freigegebene, verwaltete Ressourcen, stoppe bei unklarem oder nicht sicherem Delta und prüfe/protokolliere danach den Erfolg. Ist der Sollzustand bereits erreicht, ändere nichts.

**Beginne jetzt mit I0/PREFLIGHT.**