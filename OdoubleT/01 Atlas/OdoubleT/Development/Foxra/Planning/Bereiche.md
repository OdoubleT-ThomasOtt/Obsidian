---
created: 2026-01-29
updated: 2026-01-29
type: note
up: "[[Planning]]"
related:
  - "[[Styling]]"
  - "[[Marktanalyse]]"
tags:
  - foxra
  - features
---

**1. Das "Deal-Cockpit" (Akquise & Basisdaten)**  
**Benutzersicht:** "Hier gebe ich die harten Fakten des Exposés und meine Kaufnebenkosten ein." Dies ist der Einstiegspunkt für jedes neue Projekt.

- **Funktionen:**
    - **Kaufpreis-Kalkulator:** Eingabe von Kaufpreis und automatische Berechnung der Nebenkosten (Grunderwerbsteuer je Bundesland, Notar 1.5-2.0%, Makler).
    - **Investitions-Bedarfs-Check:** Unterscheidung zwischen "Kaufpreis" und "Gesamtinvestitionsbedarf" (inkl. sofortiger Modernisierungskosten/CAPEX).
    - **Ertrags-Eingabe:** Aktuelle Kaltmiete vs. Marktmiete (Soll-Miete) und Quadratmeter-Preise.
    - **Bewirtschaftungskosten:** Eingabe der nicht-umlagefähigen Kosten (Instandhaltungsrücklage, Verwaltung, Mietausfallwagnis).
- **Ziel:** Ermittlung des reinen **Objekt-Einkaufspreises** und des **Net Operating Income (NOI)** vor Finanzierung und Steuer.

**2. Das "Financial Engineering Lab" (Finanzierungs-Struktur)**  
**Benutzersicht:** "Hier baue ich mir meinen Finanzierungsmix zusammen, um das Eigenkapital zu schonen." Hier wird der USP "Multi-Lender" sichtbar. Der Nutzer sieht nicht nur _einen_ Kredit, sondern einen "Stack".

- **Funktionen:**
    - **Multi-Loan Stacking:** Hinzufügen beliebig vieler Kreditbausteine (z.B. 1. Baustein Sparkasse, 2. Baustein KfW, 3. Baustein Verkäuferdarlehen).
    - **Parameter-Konfiguration:** Einstellung von Zinsbindung (5, 10, 15 Jahre), Tilgungssatz (in % oder absolut) und **tilgungsfreien Anlaufjahren**.
    - **Eigenkapital-Hebel:** Eingabe des gewünschten Eigenkapitals und automatische Berechnung der Finanzierungslücke ("Loan-to-Cost" vs. "Loan-to-Value").
- **Ziel:** Berechnung der **Rate (Annuität)** und des **Cashflow vor Steuern**.

**3. Die "Tax Engine" (Steuerliche Simulation)**  
**Benutzersicht:** "Hier optimiere ich meine Steuerlast und prüfe Abschreibungsmöglichkeiten." Das Herzstück für den deutschen Markt und der größte Unterschied zu US-Apps.

- **Funktionen:**
    - **AfA-Konfigurator:** Auswahl der Abschreibungsmethode (Linear alt, Linear neu 3%, Degressiv 5%, Sonder-AfA Mietwohnungsneubau).
    - **Gebäudeanteil-Schieber:** Manuelle oder pauschale Festlegung, wie viel vom Kaufpreis auf das Gebäude (abschreibbar) und wie viel auf den Boden (nicht abschreibbar) entfällt.
    - **Persönliches Steuer-Profil:** Eingabe des zu versteuernden Einkommens (Grenzsteuersatz-Logik).
    - **15%-Tracker:** Ein "Budget-Monitor" für erhaltungsnahe Aufwendungen in den ersten 3 Jahren (Warnsystem).
- **Ziel:** Berechnung des **Steuereffekts (Erstattung oder Nachzahlung)** und des **Cashflow nach Steuern**.

**4. Die "Time Machine" (30-Jahres-Projektion)**  
**Benutzersicht:** "Ich will sehen, was passiert, wenn die Zinsbindung ausläuft oder ich verkaufe." Der Bereich für Langzeitstrategie und Risikoanalyse.

- **Funktionen:**
    - **Inflations-Split:** Getrennte Regler für Mietsteigerung (z.B. 2% p.a.) und Kostensteigerung (z.B. 4% p.a.).
    - **Zinsänderungs-Simulator:** Visualisierung des "Zinsschocks" nach Ende der Zinsbindung (Anschlussfinanzierung mit z.B. 6% statt 3.5% simulieren).
    - **Exit-Szenario:** Berechnung des Verkaufserlöses nach X Jahren abzüglich Restschuld und ggf. Spekulationssteuer.
    - **KPI-Entwicklung:** Verlaufskurven für Eigenkapitalrendite und kumulierten Cashflow.
- **Ziel:** Validierung der **Langzeit-Rentabilität** und **Risikobewertung**.

**5. Das "Exposé Studio" (Reporting)**  
**Benutzersicht:** "Ich brauche ein professionelles PDF für den Banktermin." Der Output-Kanal, um externe Stakeholder zu überzeugen.

- **Funktionen:**
    - **One-Pager:** Zusammenfassung der wichtigsten KPIs auf einer Seite.
    - **Bank-Dossier:** Detaillierter Report mit Vermögensaufstellung, Cashflow-Planung und Renovierungsstau.
    - **Export:** PDF-Generierung.
- **Ziel:** **Professionalisierung** des Anlegers gegenüber Dritten.