Styles:  
- [x] • Cosmic space  
• Nature  
- [x] • Futuristic  
- [x] • Minimalistic  
- [x] • Liquid  
- [x] • Glassmorphic  
- [x] • Skeuomorphic  
- [x] • Tactile  
- [x] • Claymorphic  
- [x] • Neumorphic  
- [x] • Geometric  
- [x] • Pop art  
- [x] • Cyberpunk  
- [x] • Embroidery  
- [x] • Dreamy  
- [x] • Isometric
      

✨ Google Gemini Prompt:  
A ui for Foxra webapplication with the speciifcations:  
Real Estate Investment Analyzer (DACH) mit dem Namen Foxra  
Projektziel: Entwicklung einer C#-basierten Desktop-Software ("Rich Client") für die professionelle Investitionsanalyse von Immobilien in der DACH-Region (Fokus Deutschland). Die Software positioniert sich als "Digitales Family Office" für Privatinvestoren und ersetzt fehleranfällige Excel-Tabellen durch typsichere, validierte Finanzmathematik.
 
Das Kernproblem (Why): Der Markt teilt sich in simple "Taschenrechner-Apps" (zu ungenau) und komplexe Enterprise-Lösungen (zu teuer). Ambitionierte Privatinvestoren (1–50 Einheiten) benötigen jedoch institutionelle Berechnungstiefe (komplexe Steuergesetze, Finanzierungsstrukturen), kombiniert mit lokaler Datensicherheit.  
Domänen-Logik & Kernfunktionen:  
Deep Tax Simulation (Steuer-Engine):  
Abbildung des deutschen Steuerrechts (§21 EStG).  
Dynamische Berechnung des Grenzsteuersatzes und der Auswirkungen auf das Gesamteinkommen ("Tax Shield").  
Simulation verschiedener Abschreibungsarten (AfA): Linear, Degressiv (Neubau), Sonder-AfA.  
Tracking der 15%-Grenze für erhaltungsnahe Aufwendungen in den ersten 3 Jahren.  
Multi-Lender Finanzierung (Kapital-Stack):  
Fähigkeit, mehrere Darlehensbausteine pro Objekt zu schichten (nicht nur ein Annuitätendarlehen).  
Hierarchie: Senior Loans (Bank), Junior Loans (Förderbanken/KfW mit tilgungsfreien Jahren), Vendor Loans.  
Berechnung des Mischzinses und der Cashflow-Effekte bei Ablauf von Zinsbindungen.  
30-Jahres-Prognose (Zeitmaschine): Langzeitsimulation von Cashflow und Vermögensentwicklung.  
Differenzierte Inflations-Drift: Trennung von Mietsteigerung (Mietspiegel) und Kostensteigerung (Instandhaltung).  
Exit-Szenarien: Spekulationssteuer (Verkauf \< 10 Jahre) vs. steuerfreier Verkauf.  
Reporting & Output: Generierung von bankfähigen Exposés und PDFs (hochwertige Visualisierung statt Excel-Ausdruck).  
Transparenz ("White Box"): Drill-Down-Erklärungen, wie sich Ergebnisse zusammensetzen.  
Zielgruppe (User Persona): Der "Prosumer"-Investor. Er/Sie legt Wert auf Datenschutz, versteht finanzielle Hebeleffekte und möchte Szenarien ("Was wäre wenn?") lokal simulieren, ohne Daten in eine Cloud hochzuladen.  
Design: Als Design Element soll ein stilisierter Fuchs und die Farbe #E65100 bei Designelementen zum Einsatz kommen
 
MainAreas:  
### 1. Das "Deal-Cockpit" (Akquise & Basisdaten)  
**Benutzersicht:** "Hier gebe ich die harten Fakten des Exposés und meine Kaufnebenkosten ein."  
Dies ist der Einstiegspunkt für jedes neue Projekt.
 
* **Funktionen:**  
* **Kaufpreis-Kalkulator:** Eingabe von Kaufpreis und automatische Berechnung der Nebenkosten (Grunderwerbsteuer je Bundesland, Notar 1.5-2.0%, Makler).  
* **Investitions-Bedarfs-Check:** Unterscheidung zwischen "Kaufpreis" und "Gesamtinvestitionsbedarf" (inkl. sofortiger Modernisierungskosten/CAPEX).  
* **Ertrags-Eingabe:** Aktuelle Kaltmiete vs. Marktmiete (Soll-Miete) und Quadratmeter-Preise.  
* **Bewirtschaftungskosten:** Eingabe der nicht-umlagefähigen Kosten (Instandhaltungsrücklage, Verwaltung, Mietausfallwagnis).  
* **Ziel:** Ermittlung des reinen **Objekt-Einkaufspreises** und des **Net Operating Income (NOI)** vor Finanzierung und Steuer.
 
### 2. Das "Financial Engineering Lab" (Finanzierungs-Struktur)  
**Benutzersicht:** "Hier baue ich mir meinen Finanzierungsmix zusammen, um das Eigenkapital zu schonen."  
Hier wird der USP "Multi-Lender" sichtbar. Der Nutzer sieht nicht nur *einen* Kredit, sondern einen "Stack".
 
* **Funktionen:**  
* **Multi-Loan Stacking:** Hinzufügen beliebig vieler Kreditbausteine (z.B. 1. Baustein Sparkasse, 2. Baustein KfW, 3. Baustein Verkäuferdarlehen).  
* **Parameter-Konfiguration:** Einstellung von Zinsbindung (5, 10, 15 Jahre), Tilgungssatz (in % oder absolut) und **tilgungsfreien Anlaufjahren**.  
* **Eigenkapital-Hebel:** Eingabe des gewünschten Eigenkapitals und automatische Berechnung der Finanzierungslücke ("Loan-to-Cost" vs. "Loan-to-Value").  
* **Ziel:** Berechnung der **Rate (Annuität)** und des **Cashflow vor Steuern**.
 
### 3. Die "Tax Engine" (Steuerliche Simulation)  
**Benutzersicht:** "Hier optimiere ich meine Steuerlast und prüfe Abschreibungsmöglichkeiten."  
Das Herzstück für den deutschen Markt und der größte Unterschied zu US-Apps.
 
* **Funktionen:**  
* **AfA-Konfigurator:** Auswahl der Abschreibungsmethode (Linear alt, Linear neu 3%, Degressiv 5%, Sonder-AfA Mietwohnungsneubau).  
* **Gebäudeanteil-Schieber:** Manuelle oder pauschale Festlegung, wie viel vom Kaufpreis auf das Gebäude (abschreibbar) und wie viel auf den Boden (nicht abschreibbar) entfällt.  
* **Persönliches Steuer-Profil:** Eingabe des zu versteuernden Einkommens (Grenzsteuersatz-Logik).  
* **15%-Tracker:** Ein "Budget-Monitor" für erhaltungsnahe Aufwendungen in den ersten 3 Jahren (Warnsystem).  
* **Ziel:** Berechnung des **Steuereffekts (Erstattung oder Nachzahlung)** und des **Cashflow nach Steuern**.
 
### 4. Die "Time Machine" (30-Jahres-Projektion)  
**Benutzersicht:** "Ich will sehen, was passiert, wenn die Zinsbindung ausläuft oder ich verkaufe."  
Der Bereich für Langzeitstrategie und Risikoanalyse.
 
* **Funktionen:**  
* **Inflations-Split:** Getrennte Regler für Mietsteigerung (z.B. 2% p.a.) und Kostensteigerung (z.B. 4% p.a.).  
* **Zinsänderungs-Simulator:** Visualisierung des "Zinsschocks" nach Ende der Zinsbindung (Anschlussfinanzierung mit z.B. 6% statt 3.5% simulieren).  
* **Exit-Szenario:** Berechnung des Verkaufserlöses nach X Jahren abzüglich Restschuld und ggf. Spekulationssteuer.  
* **KPI-Entwicklung:** Verlaufskurven für Eigenkapitalrendite und kumulierten Cashflow.  
* **Ziel:** Validierung der **Langzeit-Rentabilität** und **Risikobewertung**.
 
### 5. Das "Exposé Studio" (Reporting)  
**Benutzersicht:** "Ich brauche ein professionelles PDF für den Banktermin."  
Der Output-Kanal, um externe Stakeholder zu überzeugen.
 
* **Funktionen:**  
* **One-Pager:** Zusammenfassung der wichtigsten KPIs auf einer Seite.  
* **Bank-Dossier:** Detaillierter Report mit Vermögensaufstellung, Cashflow-Planung und Renovierungsstau.  
* **Export:** PDF-Generierung.  
* **Ziel:** **Professionalisierung** des Anlegers gegenüber Dritten.
 
---
 
Show the full home screen design. unique and innovative ui design. award winning ui and interaction. full front view design not a mockup. full screen ui design for project handoff. each element should have a purpose for the user interaction and satisfaction. no annotations. the theme should be Neumorphic.
 
✨ UX Pilot Prompt: A ui for [idea]. Create the home page. unique and innovative ui design. award winning ui and interaction. the style should be [style] (Select web or mobile + Deep & Max Design)
 
Neumorphic:

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223704-0.png)  

Cosmic space:

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223708-1.png)  

Skeuomorphic

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223712-2.png)  

Tactile:

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223715-3.png)  

Glassmorphic:

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223717-4.png)  

Claymorphic:

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223719-5.png)  

Futuristic:

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223722-6.png)  

Liquid :

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223726-7.png)  

Geometric:

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223732-8.png)  

Pop art:

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223735-9.png)   
Cyberpunk

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223736-10.png)  

Embroidery:

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223739-11.png)  

Dreamy :

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223742-12.png)  

Isometric:

![Exported image](90%20Extras/Attachments/Exported%20image%2020260127223745-13.png)