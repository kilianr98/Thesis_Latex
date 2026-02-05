1. Einleitung
2. Sicherheit und konzeptionelle Grundlagen
    1. Einordnung Feldgeräte in die Automatisierungspyramide
        1. Aufgaben Feldgeräte
        2. Übersicht in welcher Schicht Feldgeräte agieren
            1. Mittels Automatisierungspyramide einordnen (Was ist das Purdue modell und passt das?)
            2. Kurzer Abriss über Automatisierungspyarmide bzw. wie ICS grundlegend aufgebaut sind
        3. Welche Gefahren gehen von Feldgeräten aus
            1. Bezüglich Security
            2. Kurz darauf eingehen welche Auswirkungen dass aber auch auf Safety haben kann
    2. Zentrale Schutzziele für Feldgeräte und Kommunikation ableiten
        1. Geheimhaltung (Confidentiality)
        2. Verfügbarkeit (Availability)
        3. Integrität (Integrity)
        4. Authentizität (Authentication)
        5. Autorisierung (Authorization)
    3. Stand der Technik
        1. Sichere Kommunikation und Onboading bei nicht netzwerkfähigen Geräten
            1. Situation Schutzziel Verfügbarkeit
                1. Physischer Zugangsschutz
            2. Situation Schutzziel Integrität
                1. Überprüfung Seriennummer etc.
            3. Situation Schutzziel Geheimhaltung
                1. Read/Write Schutz mittels PW/PIN
            4. Situation Schutzziel Authentizität (Authentication)
                1. Abgleich Seriennummer?
            5. Situation Schutzziel Autorisierung (Authorization)
                1. Admin privileges, geschützt mittels PW/PIN
            6. Welche Kommunikationsarten (welche Feldbusse) gibt es und beinhalten diese Security Funktionen 
                1. Analog/Feldbus
                2. -> 6X Feldbusse in Tabellenform bewerten bezogen auf Schutzziele
                3. Security Guideline 6X HART einarbeiten
        2. Sichere Kommunikation und Onboading bei netzwerkfähigen Geräten
            1. Situation Schutzziel Verfügbarkeit
                1. Physischer Zugangsschutz
            2. Situation Schutzziel Integrität
                1. Digitale Signaturen
            3. Situation Schutzziel Geheimhaltung
                1. Verschlüsselte Kommunikation
            4. Situation Schutzziel Authentizität (Authentication)
                1. Zertifikate, PKI
            5. Situation Schutzziel Autorisierung (Authorization)
                1. Admin privileges, geschützt mittels PW/PIN? 
                2. Gibt es hier Unterschiede zu non IP?
            6. Welche Kommunikationsarten (welche Feldbusse) gibt es und beinhalten diese Security Funktionen 
                1. -> Feldbusse in Tabellenform bewerten
        3. Public-Key-Infrastrukturen und Zertifikate
            1. Rolle von PKI in industriellen Kommunikationssystemen
                1. Skalierbare Authentisierung
            2. Architektur einer PKI für Feldgeräte
                1. Root CA, Sub CA , RA
                2. Vertrauensmodell
            3. Geräteidentitäten und Authentifizierung von Feldgeräten, mit Zertifikaten als Trust Anchor und IDevID Konzept
                1. Erklärung Zertifikate X.509
                2. CSR
                3. Erklärung IDevID (IEEE 802.1 AR)
                4. Wie wird IDev in der Fertigung aufgespielt?
                5. Wie sieht eine Authentifizierung mittels IDevID im Feld aus?
                6. LDEVID
                7. Welche Schutzziele können durch IDevID erzielt werden
    4. Regulatorische Anforderungen
            1. CRA
            2. IEC62443-4-2
3. Bedrohungsmodell des Ausgangssystems (Nach NIST Vorlage) *Argumentative Grundlage warum Protokoll so gestaltet ist*
4. Konzeption eines sicheren Verbindungsaufbaus (Antwort auf Kapitel 3)
    1. Wie sieht ein Konzept für einen sicheren Verbindungsaufbau aus?
        1. Erklärung ephemerer Schlüsselaustausch, Unsicherer Kanal
        2. Welche Zertifikatsbasierten Protokolle gibt es?
        3. Warum gerade TLS1.3
    2. Anforderungen an einen sicheren Verbindungsaufbau
        1. Muss die SChutzziele abdecken
        2. Halbwegs schnell sein
        3. Kryptografisch sicher
    3. Reduktion und Anpassung etablierter Sicherheitsprotokolle
        1. Erklärung TLS1.3
        2. Erklärung welche
    4. Auswahl kryptographischer Verfahren unter Beachtung der limited Resources
        1. *Recommended Curves* von Nist und BSI
        2. Dann meine Tabelle zur Auswahl der Algorithmen
    5. Konzeption eines zertifikatsbasierten Verbindungsaufbaus
        1. Annahmen bezüglich:
            1. Session Abbruch, retry falls Protokoll failt
        2. Ablauf Protokoll erklären (mit schönen Bildern), kann ich fast 1:1 aus Obsidian übertragen
    6. Integration in VVO-Kommunikation
        1. Was *darf/kann/muss* ich hier schreiben?
        2. Verschlüsselung innerhalb des Payloads, Frame bleibt VVO
5. Bedrohungsmodell
    1. Nach NIST Vorlage durchgehen (Kann auch fast 1:1 übertragen werden)
    2. Bedrohungsmodell des Systems nach Anwendung des Protokolls
    3. Restrisiken, Grenzen und Einschränkungen des Ansatzes
        1. Countermeasures
6. Schnittstellen und PKI-Integration
    5. Anforderungen an die Schnittstelle zwischen Sensor und Registration Authority
    6. Definition des Kommunikationsinterfaces
        1. Protokoll- und Nachrichtenstruktur
    7. Integration in die bestehende PKI
    8. Zertifikatsfluss zwischen Sensor und Registration Authority
7. Embedded-Umsetzung auf dem Feldgerät (Eher den Ablauf beschreibend, ein paar UML Diagramme einbinden)
    1. Zielplattform und Sicherheitsfunktionen des Mikrocontrollers
    2. Erzeugung und Speicherung kryptographischer Schlüssel auf dem Sensor
    3. Erstellung und Speicherung des Certificate Signing Request
    4. Zertifikatsmanagement auf dem Sensor
        1. Empfang und Speicherung des Zertifikats
        2. Validierung und Nutzung des Zertifikats
    5. Performance-, Energie- und Ressourcenbetrachtung
        1. CSR/IDev in Fertigung
        2. Protokollablauf
8. Diskussion und Ausblick
    1. Bewertung der Ergebnisse
    2. Mögliche Erweiterungen und Weiterentwicklungen
        1. Display mit Zertifikat austatten



---
2.1. Einordnung Feldgeräte in die Automatisierungspyramide
2.2. Zentrale Schutzziele für Feldgeräte und Kommunikation ableiten
2.3. Stand der Technik
2.3.1. Sichere Kommunikation und Onboading bei nicht netzwerkfähigen Geräten
2.3.2. Sichere Kommunikation und Onboading bei netzwerkfähigen Geräten
2.3.3. Public-Key-Infrastrukturen und Zertifikate
2.3.4. Regulatorische Anforderungen