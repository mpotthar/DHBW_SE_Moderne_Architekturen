# ADR_01: Verwendung einer Microservices-Architektur

## Inhaltsverzeichnis
1. [Status](#status)  
2. [Kontext](#kontext)  
3. [Entscheidung](#entscheidung)  
4. [Konsequenzen](#konsequenzen)  
5. [Compliance](#compliance)  
6. [Notizen](#notizen)  

---

## Status
**Akzeptiert**  

---

## Kontext
Die Telemedizin-App wird von berufstätigen Menschen genutzt, die eine schnelle Krankschreibung benötigen. Aufgrund der steigenden Nachfrage und des erwarteten Wachstums von 200 % innerhalb der nächsten 12 Monate muss das System skalierbar sein, um Lastspitzen standzuhalten und eine zuverlässige Performance zu gewährleisten. Gleichzeitig ist es notwendig, die verschiedenen Funktionen der App (z. B. Videosprechstunden, E-Rezepte, Terminverwaltung) unabhängig voneinander zu entwickeln und zu aktualisieren, ohne die gesamte Plattform zu beeinträchtigen.

---

## Entscheidung
Wir haben uns entschieden, eine **Microservices-Architektur** zu implementieren. Jeder Kernservice (z. B. Terminverwaltung, Video-Chat, Zahlungsabwicklung) wird als eigenständiger Microservice betrieben. Diese Services werden in Kubernetes-Clustern orchestriert und durch serverlose Funktionen ergänzt, um eine hohe Skalierbarkeit und Flexibilität zu gewährleisten. Ein API-Gateway wird eingesetzt, um die Kommunikation zwischen den Services zu steuern und externe Schnittstellen bereitzustellen.

---

## Konsequenzen

### Vorteile
- **Skalierbarkeit:** Jeder Service kann unabhängig voneinander skaliert werden, basierend auf seiner spezifischen Last.
- **Modularität:** Neue Features können einfach hinzugefügt werden, ohne bestehende Services zu beeinträchtigen.
- **Ausfallsicherheit:** Ein Fehler in einem Service beeinträchtigt nicht die gesamte Plattform.
- **Integration:** Einfachere Integration mit externen Systemen durch standardisierte APIs.

### Nachteile
- **Komplexität:** Höhere Komplexität bei der Entwicklung und Wartung der Architektur.
- **Kosten:** Erhöhte Kosten für die initiale Einrichtung der Infrastruktur und Schulung des Teams.
- **API-Gateway:** Erfordert ein API-Gateway zur Verwaltung der Kommunikation zwischen den Services.
- **Debugging:** Fehler können über mehrere Services verteilt auftreten, was Debugging erschwert.  

---

## Compliance
### Automatisierte Tests
- **Skalierbarkeit:** Lasttests mit Tools wie JMeter (Simulation von 10.000 parallelen Nutzern pro Service).
- **Modularität:** Fitness-Funktionen testen, ob jeder Service unabhängig deploybar ist.

### Manuelle Überprüfung
- **Sicherheitsaudits:** Quartalsweise Sicherheitsaudits durch externe Penetrationstester zur Überprüfung der Architektur auf Schwachstellen.
- **Datenschutzprüfung:** Prüfung der Einhaltung von Datenschutzrichtlinien (z. B. DSGVO) durch regelmäßige interne Audits und Zertifizierungen (bspw. ISO 27001).

---

## Notizen
- **Autor:** Dominik, Thorge, Marcel, Luis
- **Genehmigt von:** Gruppe XYZ 
- **Datum:** 01.04.2025  
- **Letzte Änderung:** Keine Änderungen bisher - Version 0.1 
- **Code-Repository:** nicht vorhanden
