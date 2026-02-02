**Titel**: Sicherer Verbindungsaufbau für nicht netzwerkfähige Feldgeräte auf Basis von Zertifikaten
**Titel englisch:** Secure Connection Establishment for Non-Network-Enabled Field Devices Based on Certificates
## 0. Ausgangslage und Zielsetzung
Aktuell ist der Vega 6X der einzige Sensor, der mit einer [[IDevID]] in der Produktion ausgestattet wird. Thema der Thesis ist es, auch Sensoren die **keine** Netzwerkschnittstelle haben, mit einem IDevID Zertifikat auszustatten und auf Basis dessen eine sichere Verbindung zwischen Sensor und Bedieneinheit aufzubauen.

---
## 1. Sicherheit und konzeptionelle Themen
- Stand der Technik
	- PKI, Zertifikate
	- Sichere Verbindung für nicht-netzwerkfähige Geräte
	- Sichere Verbindung für netzwerkfähige Geräte
	- Authentizierung von Feldgeräten
	- Zertifikate -> Überblick PKI, Zertifikate als Trust Anchor, IDevID, 
	- Regulatorische Anforderungen (CRA)
- Usecases
- Ableitung Zentraler Schutzziele
---
## 2. Sichere Kommunikation über nicht IP-basierte Kanäle
### 2.1 Konzipierung einer sicheren Verbindung für nicht IP-basierte Kommunikationsprotokolle
- Entwicklung eines Bedrohungsmodells für die Kommunikation über end to end Schnittstellen (Seriell)
- Analyse, welche Elemente etablierter Sicherheitsprotokolle für eingebettete Szenarien unverzichtbar sind und welche reduziert oder angepasst werden können
- Auswahl geeigneter kryptographischer Verfahren unter Berücksichtigung verfügbarer Hardware‑Funktionen des Feldgeräts
- Vergleichende Bewertung zwischen etablierten Netzwerkprotokollen und einem angepassten Ansatz hinsichtlich Sicherheitsniveau, Energiebedarf und Performance
- Konzeptionelle Erstellung eines Protokolls zum sicheren Verbindungsaufbau mittels Zertifikaten und anschließender Verschlüsselter Kommunikation über unsicheren Kanal.
---
## 3. Umsetzung Embedded
### 3.1 Schlüssel- und Zertifikatsgenerierung
- Erzeugung eines Schlüsselpaares direkt auf dem Sensor. 
- Sicheres Speichern des privaten Schlüssels in Hardware (STM32U3).
- Erstellung eines [[Certificate Signing Request (CSR)]] mit Metadaten und öffentlichem Schlüssel und 
- Speicherung des CSR im Flash-Speicher.
### 3.2 Zertifikatsmanagement auf dem Sensor
- Integration von Flash-Speicher zur Ablage von CSR und Zertifikat.
- Übertragung des CSR an die [[Registration Authority (RA)]].
- Empfang des ausgestellten Zertifikats von der RA.
- Speicherung und Validierung des Zertifikats auf dem Sensor.
---
## 4. Schnittstellen und Kommunikation
### 4.1 Interface-Definition
- Entwicklung einer Schnittstelle zwischen RA und Sensor für Geräte ohne Netzwerkschnittstelle.
- Anforderungen an die Schnittstelle.
- Definition eines [[VVO]]-Interfaces.
### 4.2 RA-Integration
- RA-Software: Interaktion mit [[Enterprise JavaBeans Certificate Authority (EJBCA) ]]([[Public Key Infrastructure (PKI)]]-Software in der IT).
- Mechanismus zur Übertragung des Zertifikats vom RA zum Sensor.
---
## 5. Diskussion und Ausblick

---

| Abkürzung | Bezeichnung                                |
| --------- | ------------------------------------------ |
| BLE       | Bluetooth Low Energy                       |
| CSR       | Certificate Signing Request                |
| EJBCA     | Enterprise JavaBeans Certificate Authority |
| PKI       | Public Key Infrastructure                  |
| PKI       | Public Key Infrastructure                  |
| RA        | Registration Authority                     |
| REST API  | Representational State Transfer API        |
| TLS       | Transport Layer Security                   |
| VVO       | Vega Visual Operating; Parameterdatei      |

## Zeitplan
[[Zeitplan]]

## Aufgabenstellung

### Beschreibung
Produktionsumgebungen stehen zunehmend im Fokus von Cyberangriffen. Eine zentrale Sicherheitsfrage lautet: Wie kann verlässlich festgestellt werden, ob ein Gerät tatsächlich die behauptete Identität besitzt?
Auch der Cyber Resilience Act der Europäischen Union, formuliert klare Anforderungen an zukünftige Feldgeräte.
So müssen beispielsweise Kontrollmechanismen implementiert werden die einen Schutz vor unbefugtem Zugriff bieten und eine Authentifizierung ermöglichen.
Aktuell werden nur Sensoren mit Netzwerkschnittstelle mit einer eindeutigen Geräteidentität (IDevID) ausgestattet. Für Sensoren ohne Netzwerkanbindung existiert kein vergleichbares Verfahren.
Dadurch fehlt ein kryptografisch Identitätsnachweis, was Angriffsflächen eröffnet und die Resilienz der Produktionsumgebung schwächt.
Aufgrund dessen ist im späteren Einsatz im Feld kein Aufbau einer sicheren Verbindung möglich, da die Identifikation des Geräts nicht erfolgen kann.
Ziel dieser Arbeit ist die Konzeption und exemplarische Umsetzung eines Verfahrens, das auch nicht netzwerkfähige Feldgeräte im Produktionsprozess mit einem IDevID‑Zertifikat ausstattet und dieses zur Absicherung der Kommunikation über nicht IP-basiertes Kommunikationsprotokoll einsetzt.


### Tätigkeitsumfang
- **Literaturrecherche & Grundlagen**:
	- Einarbeitung in die Themenbereiche **Sicherer Verbindungsaufbau, PKI, Zertifikate**, **Geräteidentitäten**
- **Embedded‑Umsetzung:** 
	- Schlüsselpaar auf dem Sensor generieren, privaten Schlüssel sicher ablegen, CSR mit Metadaten im Flash speichern sowie Mechanismen zum Empfang, Speichern und Validieren von Zertifikaten implementieren.
- **Schnittstellen & Kommunikation:**  
	- Schnittstelle zur Übertragung von CSR und Zertifikat zwischen Sensor und RA entwickeln, VVO‑Interface definieren, Integration in die bestehende PKI-Struktur und gesamter Zertifikatsfluss konzipieren.
- **Sichere Kommunikation über nicht IP-basierte Kanäle**
	- Erstellung eines Bedrohungsmodells und Ableitung Schutzziele
	- Konzipierung eines Protokolls zur sicheren Verbindung
	- Auswahl und Bewertung kryptographischer Verfahren unter Berücksichtigung verfügbarer Hardware-Funktionen des Feldgeräts
	- Abschließende Bewertung zwischen etablierten Netzwerkprotokollen und angepassten Ansatz hinsichtlich Sicherheitsniveau, Energiebedarf und Performance


Herausforderungen zu Thema 5
1. **Ressourcenbeschränkungen**
	- Eingeschränkte Rechenleistung, Speicher und Energie erfordern eine sorgfältige Auswahl und Anpassung kryptographischer Verfahren
	- Abwägung zwischen Sicherheits-, Laufzeit- und Energieanforderungen
2. **Sicherheitsmodellierung im Offline‑Kontext**
	- Untersuchung neuer Angriffsvektoren, die sich aus der Nutzung von end to end Schnittstellen, sowie angepassten Protokoll für ressourcenarme Geräte ergeben
	- Entwicklung geeigneter Gegenmaßnahmen zur Wahrung der Schutzziele