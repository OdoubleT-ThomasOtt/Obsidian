---
created: 2026-01-29
updated: 2026-01-29
type: note
up: "[[Marktanalyse]]"
related:
  - "[[Wettbewerbsanalyse und Profilierung]]"
  - "[[Top-5 Feature Parity Matrix]]"
tags:
  - foxra
  - market
---

Verglichen mit den identifizierten Wettbewerbern deckt Ihr MVP kritische Lücken ab, die insbesondere für den deutschen Markt essentiell sind.
 
**3.1 Die Steuer-Simulations-Lücke (Deep Tax)**  
Die meisten Wettbewerber (Cluster A & C) nutzen pauschale Steuersätze (z.B. "42%"). Dies führt zu massiven Fehlkalkulationen.
 
Der MVP-Vorteil:
 
Grenzsteuersatz-Automatik: Integration der Formel nach § 32a EStG. Das Tool muss simulieren, wie sich negative Einkünfte aus V+V (z.B. durch hohe AfA oder Sanierung) auf das zu versteuernde Gesamteinkommen auswirken ("Tax Shield").
 
AfA-Variabilität: Wettbewerber rechnen oft linear mit 2%. Ihr Tool muss folgende Szenarien beherrschen:
 
Lineare AfA: Anpassung an Baujahr (2%, 2,5%, 3%).
 
Degressive AfA: Für Neubauten (5% fallend) - ein aktueller Gesetzeshebel.
 
Sonder-AfA: Nach § 7b EStG für Mietwohnungsneubau.
 
Restnutzungsdauer-Gutachten: Simulation der Verkürzung der Nutzungsdauer (z.B. auf 33 Jahre statt 50 Jahre), was den Cashflow nach Steuern massiv erhöht.
 
15%-Grenze (Anschaffungsnahe Herstellungskosten): Kein App-Wettbewerber trackt aktiv das Budget für Erhaltungsaufwendungen innerhalb der ersten drei Jahre. Ein "Warn-System" (z.B. "Noch 4.000 € Budget verfügbar bis zum Stichtag X") wäre ein massiver USP.
 
**3.2 Die Zeitverlaufs-Lücke (30-Jahres-Prognose)**  
Apps sind "Momentaufnahmen". Immobilien sind "Lebensläufe".
 
Der MVP-Vorteil:
 
Inflations-Drift: Differenzierung zwischen Mietsteigerung (z.B. 2% p.a., gekappt durch Mietspiegel) und Instandhaltungskostensteigerung (z.B. 4% p.a., Handwerkermangel). Apps rechnen oft mit einer pauschalen Inflationsrate für beides, was die Rendite im Jahr 20 schönrechnet.
 
Zinsänderungsrisiko: Simulation des "Cliffs" nach Ablauf der Zinsbindung (z.B. nach 10 oder 15 Jahren). Was passiert mit dem Cashflow, wenn der Anschlusszins bei 6% liegt? Das Visualisieren dieses Risikos ist essenziell für die Bankvorbereitung.
 
Exit-Szenarien: Berechnung der Veräußerungsgewinnsteuer (Spekulationssteuer) bei Verkauf \< 10 Jahre vs. steuerfreier Verkauf \> 10 Jahre.
 
**3.3 Die Finanzierungs-Lücke (Multi-Lender)**  
Professionelle Finanzierungen bestehen selten aus einem einzelnen Annuitätendarlehen.
 
Der MVP-Vorteil:
 
Kapital-Stacking: Die Software muss die Hierarchie abbilden:
 
Senior Loan (Bank): Erstrangig, günstiger Zins.
 
Junior Loan (KfW): Nachrangig oder förderfähig, oft tilgungsfreie Anlaufjahre.
 
Vendor Loan (Verkäuferdarlehen): Oft endfällig (Bullet) oder zinslos.
 
Mischkalkulation: Berechnung des gewichteten Gesamtzinses und des aggregierten Cashflow-Profils. Ein KfW-Kredit mit 3 tilgungsfreien Jahren verzehrt das Cashflow-Bild in Jahr 1 positiv, führt aber in Jahr 4 zu einem Schock. Einfache Rechner zeigen diesen Effekt nicht.