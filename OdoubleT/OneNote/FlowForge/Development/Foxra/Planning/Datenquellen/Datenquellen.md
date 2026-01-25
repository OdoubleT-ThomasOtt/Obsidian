|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|**Quelle_ID**|**Quellenname**|**Domain_Kategorie**|**Sub_Kategorie**|**Land**|**Raum_Genauigkeit_Mikro**|**API_Typ**|**Datenformat**|**Lizenztyp**|**Kommerzielle_Nutzung**|**Aufwand**|**Business_Value**|**Differenzierungswert**|**Kritikalitaet_MVP**|**Projektphase**|
|AT_STAT_DEMO_01|Statistik Austria – Bevölkerungsdaten|Demografie|Bevölkerung/Altersstruktur|AT|Gemeinde (über Join)|REST/Download|CSV/JSON|CC BY 4.0|Ja|2|4|3|Must-have|MVP|
|DE_DEST_DEMO_01|Destatis GENESIS – Regionaldaten|Demografie|Bevölkerung/Altersstruktur|DE|Gemeinde/Kreis|REST|JSON|dl-de/by-2.0|Ja|3|4|3|Must-have|MVP|
|OSM_POI_01|OpenStreetMap Overpass – POI (Schulen/Ärzte/Einkauf)|Infrastruktur|POI/Erreichbarkeit|DACH|Adressnah (Radius 250–1500m)|REST|JSON|ODbL|Ja (mit Bedingungen)|3|5|5|Must-have|MVP|
|OSM_ROUTING_01|OpenRouteService – Routing/Gehzeit|Infrastruktur|Fußwege/Fahrzeit|DACH|Adressgenau|REST|JSON|OSM-basiert (frei)|Ja|3|4|4|Should-have|MVP|
|AT_LAERM_01|Laerminfo.at – Strategische Lärmkarten|Umwelt|Lärm Strasse/Schiene|AT|Adressnah (Raster/Zone)|WMS/WFS|GeoTIFF/Shape|CC BY 4.0|Ja|4|4|4|Should-have|Phase 2|
|AT_HORA_01|HORA – Hochwasserüberflutungsflächen|Umwelt/Risiko|Hochwasser HQ100/HQ300|AT|Adressnah (Punkt-in-Polygon)|WFS/Download|GeoJSON/Shape|CC BY 4.0|Ja|4|5|5|Must-have|Phase 2|
|DE_UBA_AIR_01|UBA – Air Data API|Umwelt|Luftqualität|DE|Messstation/Region|REST|JSON|dl-de/by-2.0|Ja|3|3|3|Should-have|Phase 2|
|AT_GEO_BREITBAND_01|Breitbandatlas Österreich|Infrastruktur|Internet/Glasfaser|AT|Adressnah (abhängig Datensatz)|Download/REST|CSV/GeoJSON|Open Data (mit Attribution)|Ja|3|3|3|Should-have|Phase 2|
|DE_BNETZ_BREITBAND_01|Breitbandatlas DE – Verfügbarkeitsdaten|Infrastruktur|Internet/Glasfaser|DE|PLZ/Gemeinde/teils Adresslevel|REST/Download|GeoJSON/CSV|dl-de/by-2.0|Ja|3|3|3|Should-have|Phase 2|
|DE_MARKT_IND_01|Deutschlandatlas – Bauland/Preisentwicklung|Markt|Preistrends/Bauland|DE|Kreis/Region|Download|CSV/JSON|dl-de/by-2.0|Ja|2|3|3|Must-have|MVP|
|AT_MARKT_IND_01|Statistik Austria/OeNB – Immobilienpreisindex|Markt|Preisindex Land/Region|AT|Regional|Download|CSV|Open Data|Ja|2|3|3|Must-have|MVP|
|~~OPENAPI_IMMO_01~~|~~OpenAPI.de – Immobilien- & Demografie API (kommerziell)~~|~~Markt~~|~~Verkäufe/Marktpreise~~|~~DACH~~|~~PLZ/Stadtteil/Adresse~~|~~REST~~|~~JSON~~|~~proprietär (Klärung nötig)~~|Ja (vertraglich klären)|4|5|5|Should-have|Phase 2|
|HAMBURG_PKS_01|Hamburg Open Data – Polizeiliche Kriminalitätsstatistik|Sozioökonomie|Sicherheit (Stadtteil)|DE_Stadt|Stadtteil|Download|CSV|dl-de/by-2.0|Ja|3|4|3|Nice-to-have|Phase 2|
|MSTR_GRUEN_01|Stadt Münster Grünflächenkataster|Umwelt|Grünflächen/Parks|DE_Stadt|Polygon/Radius lokal|Download|GeoJSON/Shape|dl-de/by-2.0|Ja|3|3|3|Nice-to-have|Phase 3|
|OSM_LANDUSE_01|OpenStreetMap – Landnutzung|Umwelt|Grünflächen/Versiegelung|DACH|Adressnah (über Buffer)|REST/Export|GeoJSON/OSM|ODbL|Ja (mit Bedingungen)|4|4|5|Should-have|Phase 2|

Realtime search with NotebookLM oder perplexity und auswertung

|   |   |
|---|---|
|[https://www.data.gv.at/](https://www.data.gv.at/)|Website: [Datensätze - Offene Daten Österreich \| data.gv.at](https://www.data.gv.at/datasets?typeFilter%5b%5d=dataset&locale=de)￼API: [Open Government, Austria API - PublicAPI](https://publicapi.dev/open-government-austria-api)￼￼--\> doku der API für claude code [hub-repo - OpenAPI Description](https://qs.data.gv.at/api/hub/repo/)|
|[GitHub - autogluon/autogluon: Fast and Accurate ML in 3 Lines of Code](https://github.com/autogluon/autogluon)|Zur Datenauswertung|