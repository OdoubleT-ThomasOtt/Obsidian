---
created: 2026-01-29
updated: 2026-01-29
type: note
up: "[[Facility Management]]"
related:
  - "[[Gesprächsleitfaden Verkauf Erstgespräch]]"
---

**Prozess 1: Störfall- und Reparaturmanagement**

- **Beschreibung:** Hausmeister oder Techniker meldet per Sprachaufnahme einen Defekt (z. B. „Heizung im 3. OG Heizungsausfall“).
- **Ablauf:**
    1. **Sprach­eingabe** über Retell-App.
    2. **Transkription** auf Server (automatisch in Textform).
    3. **n8n-Workflow**
        - Zuordnung des Texts zu Objekt- und Standortdaten im CAFM/CRM.
        - Extraktion wichtiger Parameter (Dringlichkeit, Gerätetyp).
        - Automatisches Erstellen eines Tickets im Ticketsystem.
        - Triggern eines Bestellprozesses für Ersatzteile im ERP, falls Lagerbestand unter Grenzwert.
        - Nachricht an verantwortlichen Servicepartner per E-Mail/Chat.
    4. **Status-Updates** und Abschlussmeldung zurück an den Meldenden.
- **ROI:**
    - **Reaktionszeit** sinkt um bis zu 50 % (statt manuellem Erfassen und Weiterleiten).
    - **Ausfallkosten** (z. B. Heizungsausfall) verkürzen sich typischerweise um 20 %–30 %.
    - Für einen Betrieb mit 20 Störmeldungen/Monat und durchschnittlich 2 h Bearbeitungs­aufwand (€/h Personalkosten):
        - **Einsparung:** 20 Meldungen × 1 h Ersparnis × 60 €/h ≈ 1 200 € pro Monat.
   

**Prozess 2 erweiterung : Standard-Tätigkeiten (z. B. Reinigung) protokollieren**  
**1. Prozessbeschreibung**

1. **Sprach- oder Freitexteingabe**
    - Mitarbeiter startet Retell und wählt „Routine-Tätigkeit“
    - Offene Eingabe („Reinigung Büro 3 abgeschlossen“) oder geführte Fragen (Was wurde gereinigt? Wo? Zeitpunkt?)
2. **Transkription & Extraktion**
    - Automatische Transkription auf Server
    - n8n erkennt Parameter:
        - **Tätigkeitstyp** (Reinigung, Inspektion, Müllentsorgung…)
        - **Ort** (z. B. Büro-Nr., Stockwerk, GPS-Koordinaten)
        - **Zeitstempel**
3. **n8n-Workflow**
    1. **Datenpersistenz**: Speichern in zentraler Log-Datenbank oder CAFM/CRM
    2. **Validierung**: Pflichtfelder prüfen, fehlende Infos per Retell-Nachfrage ergänzen
    3. **Dash­board-Update**: Live-Übersicht „Welche Räume wurden wann gereinigt?“
    4. **Folgeaktionen** (optional):
        - Erinnerung, falls Reinigungsintervall überschritten
        - Eskalation, wenn z. B. Reinigung nicht erfolgt ist
 
**2. Technische Umsetzung**

- **Retell-App**: Neuer Workflow-Typ „Routine“ mit konfigurierbaren Fragen
- **n8n**:
    - **HTTP-Trigger** empfängt Transkript + Metadaten
    - **Mapping-Node** ordnet Felder zu (Tätigkeit, Ort, Zeit)
    - **Datenbank-Node** schreibt in SQL/NoSQL oder CAFM-API
    - **Dashboard-Node** (z. B. auf Grafana, Power BI) aktualisiert Übersicht
    - **Scheduler-Node** für Intervall-Checks und Erinnerungen
 
**3. Messbarer Mehrwert (ROI)**
 
|   |   |   |
|---|---|---|
|**Vorteil**|**Wirkung**|**Beispielrechnung**|
|**Transparenz & Nachvollziehbarkeit**|Vollständige Audit-Logs ohne manuelle Nachträge|Auditvorbereitung ↓ um 50 % (1 h ↘ 0,5 h) → 30 € Ersparnis pro Audit|
|**Termintreue**|Automatische Interval-Erinnerungen|5 Reinigungsintervalle × 0,5 h Erinnerung = 2,5 h gesparte Koordination (150 €)|
|**Qualitätssicherung**|Schnelle Identifikation von Ausreißern|Verminderte Reklamationen um 20 % (200 € p. M.)|
|**Gesamtersparnis**||ca. 380 € pro Monat je Objekt|
    
**Prozess 2: Compliance- und Audit-Reporting**

- **Beschreibung:** Regelmäßige Checklisten (Brandschutz, Arbeitssicherheit) werden während der Begehung per Sprache abgefragt.
- **Ablauf:**
    1. **Geführte Sprach-Checkliste** in Retell (z. B. „Rauchmelder prüfen? Ja/Nein, Datum?“).
    2. **Transkription** und Validierung (fehlende Antworten werden automatisch nachgefragt).
    3. **n8n-Workflow**
        - Aggregation aller Antworten.
        - Erzeugung eines PDF-Reports (inkl. Datum, Unterschriftfeld).
        - Versand an Management und Archivierung in Dokumenten-Repository.
    4. **Alarm** bei kritischen „Nein“-Antworten: Sofortige Eskalation und Aufgabenvergabe.
- **ROI:**
    - **Zeitersparnis** im Reporting: statt 4 h manuell nur 30 Minuten automatisiert.
    - Für vierteljährliche Audits (4× jährlich) bei 3 h Stundenverrechnungssatz 60 €/h →
        - Früher: 4 × 4 h × 60 € = 960 €
        - Jetzt: 4 × 0,5 h × 60 € = 120 €
        - **Ersparnis** ≈ 840 € jährlich.
      

**Prozess 3: Predictive Maintenance & Planung**

- **Beschreibung:** Techniker gibt bei routinemäßigen Begehungen Messwerte (Druck, Temperatur) per Sprach- oder Freitexteingabe ein.
- **Ablauf:**
    1. **Gesteuerte Befragung** durch Retell (Fragen zu Messwerten, Zustand).
    2. **Transkription** und **Extraktion** der Zahlenwerte.
    3. **n8n-Workflow**
        - Vergleich mit historischen Soll-Kennwerten.
        - KI-basierte Analyse: Erkennung von Abweichungen oder Trends.
        - Planung von Wartungs­inspektionen via Kalender-Integration (Outlook/Google).
        - Automatische Erinnerung an Techniker 24 h vor Termin.
    4. **Reporting:** Dashboard-Update für Facility Manager.
- **ROI:**
    - **Ungeplante Ausfälle** reduzieren sich um bis zu 25 % (weniger Notfälle und Eilreparaturen).
    - **Planungssicherheit** erhöht Auslastung der Techniker um ~15 %.
    - Bei jährlichen ungeplanten Ausfallkosten von 100 000 € → Einsparpotenzial ≈ 25 000 €.